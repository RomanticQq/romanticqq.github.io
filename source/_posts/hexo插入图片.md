---
title: hexo插入图片
tags:
  - hexo
  - next
  - 图床
categories: hexo
abbrlink: 16600
date: 2021-01-05 17:13:17
---
#### 方法一
1. 在blog的本地文件的根目录中打开git Bash，然后执行
`    npm install hexo-asset-image --save`

2. 打开blog根目录下的配置文件_config.yml，修改
`post_asset_folder: true  //由false改为true`
此时，当执行`hexo n 文章名`的时候，会在_post目录下新建同名的一个文件夹和一个后缀名为`.md`的文件
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105173654.png)
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105173920.png)
3. 打开`/node_modules/hexo-asset-image/index.js` 用下面代码替换
```
'use strict';
var cheerio = require('cheerio');

// http://stackoverflow.com/questions/14480345/how-to-get-the-nth-occurrence-in-a-string
function getPosition(str, m, i) {
  return str.split(m, i).join(m).length;
}

var version = String(hexo.version).split('.');
hexo.extend.filter.register('after_post_render', function(data){
  var config = hexo.config;
  if(config.post_asset_folder){
        var link = data.permalink;
    if(version.length > 0 && Number(version[0]) == 3)
       var beginPos = getPosition(link, '/', 1) + 1;
    else
       var beginPos = getPosition(link, '/', 3) + 1;
    // In hexo 3.1.1, the permalink of "about" page is like ".../about/index.html".
    var endPos = link.lastIndexOf('/') + 1;
    link = link.substring(beginPos, endPos);

    var toprocess = ['excerpt', 'more', 'content'];
    for(var i = 0; i < toprocess.length; i++){
      var key = toprocess[i];
 
      var $ = cheerio.load(data[key], {
        ignoreWhitespace: false,
        xmlMode: false,
        lowerCaseTags: false,
        decodeEntities: false
      });

      $('img').each(function(){
        if ($(this).attr('src')){
            // For windows style path, we replace '\' to '/'.
            var src = $(this).attr('src').replace('\\', '/');
            if(!/http[s]*.*|\/\/.*/.test(src) &&
               !/^\s*\//.test(src)) {
              // For "about" page, the first part of "src" can't be removed.
              // In addition, to support multi-level local directory.
              var linkArray = link.split('/').filter(function(elem){
                return elem != '';
              });
              var srcArray = src.split('/').filter(function(elem){
                return elem != '' && elem != '.';
              });
              if(srcArray.length > 1)
                srcArray.shift();
              src = srcArray.join('/');
              $(this).attr('src', config.root + link + src);
              console.info&&console.info("update link as:-->"+config.root + link + src);
            }
        }else{
            console.info&&console.info("no src attr, skipped...");
            console.info&&console.info($(this));
        }
      });
      data[key] = $.html();
    }
  }
});
```
4. 把自己想用的图片放在新建的文件夹(文章名的文件夹)中，在`test.md`中引用是`![](图片的文件名)`
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105183827.png)

#### 方法二
1. 在`\blog\source`目录下新建`image`文件夹
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210105184557.png)
2. 把想要插入的图片都放入`image`文件夹下
3. 在插入图片的位置引用`![](/image/图片名)`即可
**注**：按照这种方式插入可能会在本地图片加载不出来，上传后就可以加载出来了；若上传后还加载不出来，检查blog根目录下的配置文件`_config.yml`的`post_asset_folder:`是否为`false`

#### 方法三
用图床实现插入图片，也是最推荐的一种，具体见[hexo+PicGo+gitee图床](https://romanticqq.top/2021/01/05/hexo-PicGo-gitee%E5%9B%BE%E5%BA%8A/)