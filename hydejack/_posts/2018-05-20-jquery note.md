---
layout: post
title: jQuery实用方法记录
description: 分享
tags: jQuery
---


***
以下是一些个人做的学习jquery所用到的方法(部分)，仅限参考！
***

$('p ~ div') 选中p后面同级的div
$('div + p') 选中紧跟着div的一个元素p
$('li:not(:first)') 选中除了第一个的li
$('li:even') 选中奇数位索引的li
$('li:odd') 选中偶数位索引的li
$('li:contains(text)') 选中li里包含此文本(text)的li
$('li:has(selector)') 选中li里包含此元素的li
$('div:empty') 选中div里为空(包括换行空格。也可以说是无节点)的div
$('div:parent') 和:empty相反，选中有节点的div

:hidden 选中隐藏的元素
:visible 选中可见的元素

$('ul[class]') 选中有class属性的ul(注意属性选择器只可以放class id属性)
$('ul[class = list]') 选中有class为list的ul
$('ul[class != list]') 选中非class为list的ul
$('li[class ^= f]') 选中有class为f开头的li

:first-child
:last-child
:first-of-type
:last-of-type
nth-child()

$(fn)
$(selector, [context]) 选中符合content的selector

data 存取数据
清除data数据 removeData

index 取索引值

get([index]) 根据索引取元素







$('div').attr('class')
$('div').attr('class', 'box1 box2');
$('div').attr({'data':'num', 'age':19});
$('div').attr('class',function (index,value) {
    console.log(index,value);
    return 'list';
})
$('div').removeAttr('data');

prop removeProp

addClass removeClass

toggleClass 切换class类名 有变无 无变有

html 可解析标签 可读写
text 不可解析标签 可读写



offset 相对于视口的距离值
position 偏移值

height 就是height本身
innerHeight 加上padding的height
outerHeight 加上padding和border的height
outerHeight(true) 加上padding和border和margin的height

内部插入 区别就是：append插入在内部最后，prepend插入在内部最前面
append  appendTo  要注意的是两者之间的返回值不同
prepend prependTo

外部插入
after before  在。。。后面/前面插入
insertAfter insertBefore  把。。。插入在。。。后面/前面

包裹
wrap 给。。。添加个包裹
unwrap 给。。。不添加包裹

替换
replaceWith 把。。。替换成。。。
replaceAll 顺序和上面的是相反的

删除
empty 删除所有子元素
remove 彻底移除选中的元素以它所有的子元素
detach 移除dom元素，但是绑定的事件还在

克隆
clone 克隆一个完全一样的副本

过滤
eq(index)
hasClass 会返回一个布尔值,只能通过class判断
is 也会返回一个布尔值，但能通过许多条件判断，如表达式、class、id等
filter 返回一个jquery对象，并且能进行多个筛选，彼此之间用逗号隔开

查找
children 查找自身子元素
closest 从自身开始向上查找符合条件的，并且只会返回一个dom元素
find 从自身开始向下查找符合条件的，并且有多少符合条件的就会返回多少
next 返回自身同级下一个元素
nextAll 返回自身同级下所有元素
prev prevAll 和上面的同理
siblings 返回自身同级所有元素
parent 只返回自身的父级元素
parents 返回自身的所有祖先元素

串联
$('li').add('div').css()  add在这里的作用就是让li加上div一起施加css属性,返回的是所有li及div
$('li a').parent().end() end在这里类似于回退，返回的是a。但如果直接选中某元素end，他会返回constructor

$.merge(arr, arr1) 合并两个数组，并且把合并的数组赋给arr
$.parseHTML('<div><span>',false) 转换成html元素.
如果是$.parseHTML('<div><script>',true),true/false决定了是否能转换script元素,最后返回的是数组形式的
$.extend  $.fn.extend,合并对象.主要用$.fn.extend扩展插件.
$.extend(true,{},obj,obj1) true or false决定了是否采用深度拷贝,第二个参数是用来存储合并的结果，
第三个和第四个参数是你要合并的对象







ready(fn) dom加载完执行   onload 文档全部加载完执行
on绑定事件 off解绑
trigger 主动触发事件
one 只绑定一次
自定义注册事件， 如下：形参里必须要加e接收注册的事件对象
$('body').on('play', function (e,data) {
    console.log(e, data);
})
$('body').trigger('play', 'hahaha');
hover 和css的hover功能类似，可以传两个回调函数，分别代表移入移出
toggle 切换当前元素是否显示，参数true显示，false和不填隐藏
blur 失去焦点
change 文本内容的改变
dblclick 双击
focus 聚焦
keydown 键盘按下
keyup 键盘抬起
keypress 按下之后瞬间发生的操作
mousedown 鼠标按下
mouseup 鼠标抬起
click 鼠标抬起后触发

e.pageX e.pageY 距离浏览器视口(包含滚动条)的距离
e.clientX e.clientY 距离浏览器视口(不包含滚动条)的距离
scroll 滚动条滚动触发
e.target 被触发的事件源对象
e.type 事件类型

show 显示
hide 隐藏  hide('slow') 缓藏

滑动
slideDown
slideUp
slideToggle

淡入淡出
fadeIn
fadeOut
fadeToggle

自定义动画
animate
delay  延迟
stop  停止动画
第一个参数：是否停止后续所有运动   false：不停止，继续运动； true：停止后续所有运动
第二个参数：是否立即到达当前目标点   false：不到达； true：到达
stop(),阻止当前运动继续后续运动;
stop(true), 阻止当前及后续所有运动;
stop(true, true),阻止当前运动并立即到当前运动目标点
stop(false, true),立即到当前运动目标点并继续下一次运动





$.type 判断当前数据类型
$.trim 去掉字符串两边的空格
$.makeArray 类数组转换为数组
$.inArray 判断当前数值是否在数组中，在的话返回对应索引，不在返回-1
$.noConflict 将$权限交出
$.extend 对象合并/扩展插件
$.fn.extend 实例方法
$.Callbacks 回调队列
    ==> add 添加回调函数到回调队列; fire 可以传你需要的实参，并触发回调函数; remove 去掉回调队列里的回调函数
    $.Callbacks() 里可以传参数. unique 相同的回调函数只执行一次; once 只触发回调队列里的函数一次(也就是只执行一次fire)
    stopOnFalse 触发回调队列里的函数时，如果遇到函数里有return false的，下面的函数就不执行;
    memory 如果触发函数fire之后还有添加到队列的函数，那么此时会连同它一起执行

    function fn1(str){
        console.log(str);
        return false;
    }
    function fn2(num){
        console.log(++num);
    }
    var cb = $.Callbacks('stopOnFalse');
    cb.add(fn1, fn2);
    cb.fire('1');
    cb.remove(fn1);
    cb.fire('1');  
