# 饿了么点餐系统
    vue2.0、vuex、vue-router、axios、webpack、eslint、better-scroll
## 演示
[在线演示戳我][1]（请使用chrome开发者手机演示模式预览）

  [1]: http://alphazhangnan.applinzi.com/sellapp/index.html#/goods
## 组件

 -  购物车
 -  购买物品小球飞入动画
 -  评价star组件
 -  商品添加、删除组件
 -  优惠图标组件
 -  目录、列表联动滚动
 -  画廊
 -  评论的是否满意和内容筛选
 -  商品列表页面
 -  店铺评价页面
 -  商家介绍页面
 -  优惠活动页面
 -  商品详情页面
 
## 构建
vue有自己的脚手架构建工具vue-cli,使用起来非常方便，使用webpack来集成各种开发便捷工具，比如：

 - 代码热更新，修改代码之后网页无刷新改变，对前端开发来说非常的方便
 - bable，ES2015出来已经有一段时间了，但是不少浏览器还没有兼容ES6.有了bable，放心使用ES6语法，它会自动转义成ES5语法。
 - Stylus，类似于SASS/SCSS，但是可以不写{}和“：”，使用起来还是很方便的

除此之外，vue-cli已经使用node配置了一套本地服务器和安装命令等，本地运行和打包只需要一个命令就可以搞定，非常的方便
##开发
vue非常好的融合了react的组件化思想和angular的指令思想。 一个vue的组件将HTML、CSS、JS代码写在一个文件里面，这样既方便编写，也方便管理和修改

###Axios
在vue1.x的时候，vue的官方推荐HTTP请求工具是vue-resource，但是在vue2.0的时候将推荐工具改成了axios。

使用方式都差不多，但需要注意的是：接口返回的res并不直接是返回的数据，而是经过axios本身处理过的json对象。真正的数据在res.data里：
