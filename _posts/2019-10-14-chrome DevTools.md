---
title: Chrome DevTools 
teaser: 你不知道的 Chrome 调试技巧
category: browser
tags: [tool]
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

   ```[ctrl]``` + ```[c]```也是okkk的

## 快捷键和通用技巧
1. 切换DevTools面板
    * 按下 ```ctrl``` + ```[``` 和 ```ctrl``` + ```]``` 可以从当前面板的分别向左和向右切换面板。
    * 按下 ```ctrl``` + ```1``` 到 ```ctrl``` + ```9```可以直接转到编号1...9的面板

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
* ```ctrl``` + ```shift``` + ```p```
* run command

1. 截屏

    选中节点，打开command
    ![](/i/images/chromeDevTools/screenshot.png)
2. 切换主题

    搜索theme可以更换主题

## 代码块Snippets

1. Snippets

   允许你存放js代码到devtools, 这东西真的🐂🍺

   sources->snippets->new snippet->右键run|ctrl+enter
2. command使用

   直接```ctrl``` + ```P```，键入!,可以直接搜索到对应的snippets的名字，直接运行

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

## 异步的console
1. console 默认被async包裹
   ```javascript
   await(ajax)
   // 利用await衍生了许多操作
   await navigator.storage.estimate()
   //查看Storage系统的占用数和空闲数
   //还有等等等
   ```

## 断点
1. 条件断点

   当在for循环中打了断点时，只需要监控第x次时，我们可以添加条件断点

   * 右击行号，选择```Add conditional breakpoint...(添加条件断点)```
   * 或者右击一个已经设置的断点并且选择 ```Edit breakpoint(编辑断点)```
   * 然后输入一个执行结果为 true 或者 false 的表达式（它的值其实不需要完全为 true 或者 false 尽管那个弹出框的描述是这样说的）。

2. console.log

   将```console.log```写入条件断点的表达式中，当应用执行到这一行的时候进行判断，输出，在不需要的时候可以方便地去除
   ![](/i/images/chromeDevTools/console.gif)

## 自定义格式转换器

   前提：开启功能```Enable custom formatters```
   直接上个作者的实践
   ```javascript
   window.devtoolsFormatters = [{
    header: function(obj){
      if (!obj.__clown) {
        return null;
      }
      delete obj.__clown;
      const style = `
        color: red;
        border: dotted 2px gray;
        border-radius: 4px;
        padding: 5px;
      `
      const content = `🤡 ${JSON.stringify(obj, null, 2)}`;

      try {
        return ['div', {style}, content]
      } catch (err) { // for circular structures
        return null;  // use the default formatter
      }
    },
    hasBody: function(){
        return false;
    }
}]

console.clown = function (obj) {
  console.log({...obj, __clown: true});
}

console.log({message: 'hello!'});   // normal log
console.clown({message: 'hello!'}); // a silly log
   ```
   ![](/i/images/chromeDevTools/formatter.jpg)
程序员的苦中作乐

## 对象 & 方法

1. ```queryObjects(param)``` 对象查询方法 

    param: 构造函数名

    作用: 查询在 **特定的时刻** + **特定的执行上下文** 有哪些对象

   （占了内存空间的对象，被回收的对象和不可用的对象不会计算）

2. ```monitor(param)``` 监听方法
   
    param: 函数名

    作用: 在该函数运行时，我们会在控制台得到输出```function xx called with arguments: params```

3. ```monitorEvents(param1, param2)``` 监听事件 

    param1: 元素

    param2: 事件

    作用: 监听某个元素上发生的某个事件

## console的骚操作
1. ```console.assert```

    ```javascript
    console.assert(assertion, obj1 [, obj2, ..., objN]);
    console.assert(assertion, msg [, subst1, ..., substN]); // c-like message formatting
    // 传入第一个参数为假时，打印跟在这个参数后的值
    ```
2. 增强```log```的阅读体验
    ```javascript
    // 通过将变量放在一个{}里，可以可以得到打印出的键值对
    var me = 'denghuan', age = 20;
    console.log({denghuan,age})
    //////以下是打印结果
    {me: "denghuan", age: 20}
      age: 20
      me: "denghuan"
    // 这个真的解决了我很多问题！！！！！赞它
    ```
3. ```console.table(param1 [,param2)```

    param1: 数组对象名

    param2: 数组形式，要打印的列名

    将数组对象等以表格的形式打印出来，这些列的宽度可以缩放，甚至可以排序，一句卧槽送给它
4. table 和 {} 的配合
    ```javascript
    console.table({})
    // 你们懂会打出啥的，就是让格式好看了，简洁明了
    ```
5. ```console.dir```
    将一个节点的相关属性等等一并打印出来，就是一个dom元素
6. 给logs加上时间戳

    run command(之前说过的)打开timestamps
7. 监测执行时间
    ```javascript
    console.time(param) //开启一个计时器
    console.timeEnd(param) //结束计时并且将结果在 console 中打印出来
    param: 用来标识的别名
    ```
8. 给console 加上css样式
   ```javascript
   console.log(str [, style1, [style2)
   在要打印的字符串中，加入'%c', 后面的参数会匹配字符串，成为该段字符串的样式
   ```
   ![](/i/images/chromeDevTools/css.png)
9. 在函数回调中直接写```console.log```可以直接将参数输出来
10. 使用实时表达式

    这个功能是我一直想找但是没找到的！！！！

    live expression: 在console面板按下眼睛符号，就可以定义任何javascript表达式，并且会实时显示该表达式值的变化

## network的骚操作
1. 自定义请求表

   要自定义显示哪些列，右键单击请求表标题上的任意位置。
2. 重新发送XHR的请求

    请求行右键->replar XHR
3. XHR断点
    ![](/i/images/chromeDevTools/network.png)

## 元素面板技巧集合
1. ```h```

    点击元素面板中的元素节点，可以按下h来控制该元素的显示和隐藏
2. ```ctrl``` + ```↑```和```ctrl``` + ```↓```
    
    将选中的元素往上或往下移动，当然这个是可以通过拖拽来实现的
3. 阴影编辑器

   在box-shdow或者text-shdow属性的阴影方形符号来打开它，会出现可视化界面使你能很方便的编辑阴影属性

   那么，其实transparent,颜色等属性也会出现符号，点击后出现可视化界面
4. 定时函数编辑器
    
    类似的，在设置动画时可以可视化编辑timing属性
5. 在元素面板中展开所有的子节点
    
    * 选中父节点，右键```expand recursively```
    * 按住```alt```再点击父节点
6. dom 断点

    监听节点被移除或者添加/属性被改变的事件

    * ```subtree modifications```: 监听它内部节点被移除或添加的事件
    * ```attribute modifications```: 监听任何当前选中的节点被 添加，移除 或者 被修改值的事件
    * ```node removal```: 监听被选中的元素被 移除 的事件

## drawer
在command菜单栏搜索drawer可以看到它有哪些功能

下面是小册里说到的且我觉得能用到的
1. 控制传感器

    ```sensors```: 可以让你模拟特定的位置，甚至模拟在3D空间中的位置
2. 模拟网络状态

    ```Network conditions```: 模拟特定的用户代理
3. 检查代码 coverage

   ```coverage```: 可以跟踪当前加载的 JS 和 CSS 文件的 哪些行正在被执行 ，并显示 未使用字节的百分比 。

   它用 绿色 的线条标记 运行 和用 红色 的线条标记 未运行
4. 检查修改的内容

    ```Changes```: 将 已更改的内容 与 最初加载的样式表 进行比较， 它不仅会使用差异形式的变化（像 Git 这样的源控制工具一样）向你展示，同时还可以撤销它们。

## Workspace
这个我觉得是真的🐂🍺！！！！

1. 将js或者html文件拖到source面板，此时浏览器就变成了你的编辑器，```ctrl``` + ```s```后,你的本地文件也会修改，并且能够将修改立即体现在页面中

    那么没有厚此薄彼，当设置好了workspace之后，在element面板编辑css，本地文件也会立即同步修改！！！！

    通过New Style Rule按钮，可以看到所有css文件，进而可以选择新增的样式保存的地方
2. 



[《你不知道的 Chrome 调试技巧》]:https://juejin.im/book/5c526902e51d4543805ef35e