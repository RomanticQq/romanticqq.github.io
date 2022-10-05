---
title: 对dataframe数据的读取、处理和保存
tags:
  - dataframe
categories: dataframe
abbrlink: 52233
date: 2022-08-24 09:21:02
---

```python
# pkl、csv、xlsx等文件都可使用pandas进行读取，读取后都为dataframe数据类型
import pandas as pd
# 读取文件
df = pd.read_pickle('data/WM-811K-simple-test.pkl')
# 新增一列 列名为failureNum 并把原先列名为failureType的数据赋值给新列
df['failureNum'] = df.failureType
mapping = {'Center': 0, 'Donut': 1, 'Edge-Loc': 2, 'Edge-Ring': 3,
           'Loc': 4, 'Near-full': 5, 'Random': 6, 'Scratch': 7, 'none': 8}
# 根据mapping映射关系对新列的数据内容进行修改
df = df.replace({'failureNum': mapping})
# 通过条件获取筛选过后的列
df = df[(df['failureNum'] >= 0) & (df['failureNum'] <= 8)]
# 对某一列进行删除
df = df.drop(['failureType'], axis=1)
# 对处理过后的数据进行保存
df.to_pickle('./data/WM-811K-torch.pkl')
```

