---
title: laravel8路由
tags:
  - laravel
  - php
categories: 后端
abbrlink: 30139
date: 2021-06-03 22:28:38
---
1. get请求
    ```php
    Route::get('/aaa',function (){
        echo 'aaa';
    });
    
    Route::get('/aaa',[TestController::class,'form']);
    ```

2. post请求
    ```php
    Route::post('/aaa',function (){
    echo 'aaa';
    });
    
    Route::post('/aaa',[TestController::class,'form']);
    ```

3. 一个路由响应多个http请求动作
    ```php
       Route::match(['get', 'post'], 'foo', function () {
           return 'This is a request from get or post';
       });
    ```

4. 一个路由来响应所有 HTTP 请求动作
    ```php
    Route::any('bar', function () {
    return 'This is a request from any HTTP verb';
    });
    ```

5. 重定向路由
    ```php
    Route::redirect('/here','/aaa');
    ```
6. 视图路由
    ```php
    Route::view('hello', 'hello', ['name' => '学院君']);
    <h1>
        Hello, {{ $name }}!
    </h1>
    注：在view中第一个参数为URL，第二个参数为视图名称，第三个参数可选为需要传到视图文件的值


7. 路由参数
    ```php
    //必选参数
    Route::get('user/{id}', function ($id) {
        return 'User ' . $id;
    });
    //可选参数  可以设置默认值
    Route::get('user/{id？}', function ($id=1) {
        return 'User ' . $id;
    });
    //多个参数
    Route::get('posts/{post}/{comment}', function ($postId, $commentId) {
        return $postId . '-' . $commentId;
    });


8. 正则约束
   ```php
   //判断一个值
   Route::get('user/{id}', function ($id) {
       // $id 必须是数字
   })->where('id', '[0-9]+');
   //判断多个值
   Route::get('user/{id}', function ($id) {
       // $id 必须是数字
   })->where('id', '[0-9]+');

9. 全局约束

   ```php
   //需要在 RouteServiceProvider 类的 boot 方法中定义这种约束模式
   public function boot()
   {
       Route::pattern('id', '[0-9]+');
   }
   Route::get('user/{id}', function ($id) {
       // 只有当 {id} 是数字时才会被调用
   });


10. 分组前缀
    ```php
    Route::prefix('sss')->group(function (){
    Route::get('index',function (){
    return 33;
    });
    Route::get('welcome',function (){
    return 44;
    });
    });
    //访问时路由为/sss/index或/sss/welcome

