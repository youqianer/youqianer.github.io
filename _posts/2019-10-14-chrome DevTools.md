---
title: Chrome DevTools 
teaser: 你不知道的 Chrome 调试技巧
category: browser
tags: [compatibility]
---

###### 掘金小册[《你不知道的 Chrome 调试技巧》]的学习总结
## copying & saving
1. copy()<br>
  可以复制任何能拿到的资源```copy(location)```
2. Store as global<br>
  复制打印出来的数据，转换成全局变量，创建一个名为temp+i的变量（深拷贝）
3. 保存堆栈信息<br>
  报错信息右键->save as, 可以将堆栈跟踪的信息保存为一个文件
4. copy HTML<br>
  [ctrl]+[c]也是okkk的

## 快捷键和通用技巧
1. 切换DevTools面板<br>
    * 按下 ctrl + [ 和 ctrl + ] 可以从当前面板的分别向左和向右切换面板。
    * 按下 ctrl + 1 到 ``ctrl + 9可以直接转到编号1...9的面板

       DevTools>>Settings >>Preferences>>*Appearance*打开第二组快捷键使用设置
2. 增加和减少<br>
    * ```↑``` increment value
    * ```↓``` decrement value
    * ```PgUp``` + ```shift``` + ```↑``` increment by 10
    * ```PgDn``` + ```shift``` + ```↓``` decrement by 10    
    * ```PgUp``` + ```shift``` increment by 100
    * ```PgDn``` + ```shift``` decrement by 100
    * ```↑``` + ```alt``` increment by 0.1
    * ```↓``` + ```alt``` decrement by 0.1
3. 查找<br>
    * ```ctrl``` + ```p```
    * ```ctrl``` + ```f```

## 使用Command
* ctrl + shift + p
* run command

1. 截屏

   选中节点，打开command
   ![](/i/images/chromeDevTools/screenshot.png)
  







[《你不知道的 Chrome 调试技巧》]:https://juejin.im/book/5c526902e51d4543805ef35e