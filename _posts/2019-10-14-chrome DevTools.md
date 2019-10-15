---
title: Chrome DevTools 
teaser: 你不知道的 Chrome 调试技巧
category: browser
tags: [compatibility]
---

###### 掘金小册[《你不知道的 Chrome 调试技巧》]的学习总结
###### 只要一分钱，学到了很多，血赚不亏
## copying & saving
1. copy()

   可以复制任何能拿到的资源```copy(location)```
2. Store as global

   复制打印出来的数据，转换成全局变量，创建一个名为temp+i的变量（深拷贝）
3. 保存堆栈信息

   报错信息右键->save as, 可以将堆栈跟踪的信息保存为一个文件
4. copy HTML

   [ctrl]+[c]也是okkk的

## 快捷键和通用技巧
1. 切换DevTools面板
    * 按下 ctrl + [ 和 ctrl + ] 可以从当前面板的分别向左和向右切换面板。
    * 按下 ctrl + 1 到 ``ctrl + 9可以直接转到编号1...9的面板

       DevTools>>Settings >>Preferences>>*Appearance*打开第二组快捷键使用设置
2. 增加和减少
    * ```↑``` increment value
    * ```↓``` decrement value
    * ```PgUp``` + ```shift``` + ```↑``` increment by 10
    * ```PgDn``` + ```shift``` + ```↓``` decrement by 10    
    * ```PgUp``` + ```shift``` increment by 100
    * ```PgDn``` + ```shift``` decrement by 100
    * ```↑``` + ```alt``` increment by 0.1
    * ```↓``` + ```alt``` decrement by 0.1
3. 查找

    * ```ctrl``` + ```p```
    * ```ctrl``` + ```f```

## 使用Command
* ctrl + shift + p
* run command

1. 截屏

    选中节点，打开command
    ![](/i/images/chromeDevTools/screenshot.png)
2. 切换主题

    搜索theme可以更换主题

 ## 代码块
1. Snippets

   允许你存放js代码到devtools, 这东西真的🐂🍺

   sources->snippets->new snippet->右键run|ctrl+enter
2. command使用

   直接ctrl+P，键入!,可以直接搜索到对应的snippets的名字，直接运行

## console中的```$```
1. $0

   $0 是对我们当前选中的 html 节点的引用。
  
   理所当然，$1 是对上一次我们选择的节点的引用，$2 是对在那之前选择的节点的引用，等等。一直到 $4
   ![](/i/images/chromeDevTools/$1.png)
   ```javascript
    // 先选中你不知道的Chrome调试技巧，再选中WebGL入门与实践
     $0.appendChild($1)
    // 实用性不说，很炫酷就是了
   ```
   ![](/i/images/chromeDevTools/$0.png)
2. $和$$

   前提：没有在App中定义过$变量
   ```javascript
     document.querySelector === $
     Array.from(document.querySelectorAll('div')) === $$('div')
   ```

3. $_

   对上次结果的引用

4. $i

   在 DevTools 里面来使用npm插件！需要安装Console Importer
   
   功能很炫酷，但是俺应当是不会用，不记了


[《你不知道的 Chrome 调试技巧》]:https://juejin.im/book/5c526902e51d4543805ef35e