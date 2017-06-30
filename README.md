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

### Axios
在vue1.x的时候，vue的官方推荐HTTP请求工具是vue-resource，但是在vue2.0的时候将推荐工具改成了axios。

使用方式都差不多，但需要注意的是：接口返回的res并不直接是返回的数据，而是经过axios本身处理过的json对象。真正的数据在res.data里：
```js
axios.get(url).then((res)=>{
  this.data = res.data
})
```
### Vue-Router
vue-router是vue的路由系统，可以用来创建单页应用。基本思想是在主页面中引入标签，然后定义路由，把router挂在到app上，然后把各个子页面渲染到view里面。使用起来还是很方便的， 跳转页面只需要
```js
router.push('test')
```
### 获取元素节点
vue2.0废除了v-el指令，所有的节点指令修改为ref，然后通过ref来获取元素节点，如
```
<div ref="testHook">test</div>
this.$ref.testHook
```
### 组件间的通信
如果是和子组件通信，则使用ref就可以实现，如：
```
<test ref="testHook"></test>
this.$ref.testHook.add() //调用test子组件的add方法
```
使用emit来发送广播
vue2提供了一套广播机制，即一边发送广播，一边接收广播来执行相应操作。使用方法如下：

比如想要给test组件发送一个“相加”广播:
```js
export default {
  method:{
  	click(){
  	  Vue.$emit('add',{}) //第二个参数可作为传递数据传送到监听端口，不需要则传空对象
  	}
  }
}
```
那么test组件中就需要监听，在created方法里写
```js
export default {
  created(){
   Vue.$on('add',this.add)
  },
  method:{
  	add(){
  	  this.count++
  	}
  }
}
```
除了以上总结的这点小的知识点以外，还有很多vue的知识想要和大家分享，以后会陆续写出来，大家感兴趣的也可以来我的GitHub一起来写这个项目（觉得不错的给个star Hah）
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
