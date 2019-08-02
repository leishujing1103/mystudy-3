## vue 是单页面应用，index.html是一个总的入口文件，挂在id为app的div下然后动态渲染路由模板。
- 单页面应用是和多页面应用相对而言的。多页面应用是在每次页面跳转的时候，后台服务器都重新生成一张html页面，首屏时间快（只需要加载一次html），搜索引擎优化效果好（html内容都在），但是切换慢（每次页面切换都需要发出一次http请求）。单页面应用首次加载时会请求一次html，随后的页面渲染都依靠js动态的将当前页面的内容清除掉（原理：js可以感知url的变化），然后将下一个页面的内容挂载到当前页面上（前端实现，不是后端，无http发送时延），首屏慢，搜索引擎优化效果差，但是切换快。
- 总结：vue的出现代替传统的多页面切换，用户在切换页面时不需要http请求，提升了用户体验。

## index.html main.js   app.vue的关系
- index.html 文件 ，首页入口。
- App.vue是一个组件，App.vue中可以写 <template> 、js、<style>， 其中必须要有export default 来表示对外输出本模块
- main.js是初始化vue实例并使用需要的插件
- app: './src/main.js'，所以当你运行npm run dev的时候就从main.js这个入口文件开始执行了

## vue加载页面过程
- 浏览器访问项目，最先访问的是index.html文件
-  在index.html中, <div id="app"></div> ,上面有一个id为app的挂载点，之后我们的Vue根实例就会挂载到该挂载点上.
-  在main.js中，新建了一个Vue实例，在Vue实例中，通过 new Vue({ el: '#app',})  告诉该实例要挂载的地方；（即实例装载到index.html中的位置)
-  接着，实例中注册了一个局部组件App，这个局部组件App来自于哪儿呢？ import App from './App.vue'
-  这个局部组件是当前目录下的App.vue,而起模板是什么呢？模板就是组件App.vue中的template中的内容。（template会替代原来的的挂载点处的内容）,所以Vue这个实例就是的是App.vue这个组件的内容。
- 不要在main.js中乱加注释，会报错。