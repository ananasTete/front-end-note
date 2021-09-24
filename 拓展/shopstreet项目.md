## src目录结构

```js
 assets                       /
    ├── css
    ├── img
    └── logo.png
 common                       
    ├── utils.js 
    └── mixin.js
 components                   //放置可复用组件的目录
    ├── common                               //放置任何项目中都可复用的组件
    └── content                              //放置本项目中可复用的组件
 network                   //网络请求目录，每个视图的网络请求都在目录下封装一个js文件
    └── request.js                      //在request.js中将axios封装成request()
 router                       //路由配置目录
    └── index.js                           //将视图映射到路径                 
 store                         //状态管理目录
    ├── index.js
    └── modules                   //每种数据都封装成一个js文件到该目录下合并到index
 views                        //视图目录
    └── view                           //每个视图都有一个目录
         ├── childComps                     //只在该视图使用的组件的目录
         └── view.vue                       //视图组件
 App.vue                      //
 main.js                      //根组件，webpack打包的入口文件
 package.json                 //包管理文件，包含npm run命令，包的名称及版本
 vue.config.js                //路径别名文件
```



## 项目经验

1. 项目结构：知道各个目录是干什么的。各种文件该放到哪里。
2. 网络请求：由视图进行网络请求并将数据保存到视图中，子组件通过自定义属性获取视图中需要的数据进行展示。
3. 功能需求：大多子组件以父组件为桥梁调动兄弟组件，有时候需要考虑到异步数据的加载问题。
4. 视图通信：动态路由、vuex
5. 其它小点：防抖、封装到全局的toast、组件根据不同的视图显示或隐藏、两种tab组件、混入





1. 每个视图中放置 n个组件；由视图进行网络请求并将数据保存到视图中，子组件通过自定义属性获取视图中需要的数据。
2. 当视图中一个相对独立内容块需要多个组件组合嵌套时，将这些组件挂载到一个组件上再挂载到视图中，使视图模板更加简洁。
3. vue-router 和 vuex在任何组件中都可以通过 `$router $route  $store` 来访问。



### 1. 网络请求

由视图进行网络请求并将数据保存到视图中，子组件通过自定义属性获取视图中需要的数据。



如何请求及保存到本地？

```js
 //network目录结构
network    
   ├── xxx.js
   ├── ...
   └── request.js
```

将 axios请求服务器根地址封装到 request.js的 request()方法中。在调用 request()方法时传入不同的具体地址就能访问到不同的数据。

为了方便维护，每个需要进行网络请求的视图都在 network下定义一个 js文件用于定义所有的网络请求。需要一种数据时在 js文件中定义并导出一个方法，方法返回一个 request()，我们给 request传入具体地址就能按指定的地址进行网络请求并返回一个promise对象。也就是说返回 request()即返回一个 promise。在视图中引入并调用这个方法。在调用方法后接 `.then`就能获取请求到的数据 `result`。

请求到的数据的作用域在函数体内，所以需要在视图中定义数据去接收请求到的数据。



请求过程中需要注意的一些问题？

1. 视图中接收网络请求的数据结构的问题

如：定义一个类来接收服务器中的数据

如果请求到的数据只是简单的一个对象或数组什么的直接定义一个空对象或数组获取即可。但如果子组件需要的数据分布在一个对象的多个子对象或子数组中呢？

第一种结构：视图定义一个空对象，直接接收并传给子组件这个大对象，视图中方便了但在子组件中使用数据时，就避免不了使用每个数据时会有多层的路径；

所以我们在 `/network/detail.js` 中定义一个类，把所有需要的数据直接定义为类的**直接属性**。视图中网络请求后新建一个类的实例把 `res`中每一个需要的数据作为参数传入，返回子组件这个对象。子组件使用时需要的数据都是对象的直接属性，子组件中就不会有多层路径问题了。需要注意的是把每一个需要的数据作为参数传给对象构造器时每个数据也是多个路径的，这里可以将一些公共路径。

其它数据结构如 home视图中的goodslist、category视图中的goodslist。

2. 视图中定义一个对象用于接收服务器来的**对象**数据时，不能定义为 `xxx: null` 而是 `xxx: {}`

自定义属性获取数据进行渲染是同步事件，而网络请求是异步事件。所以子组件的渲染包含两个阶段：1.将视图中数据的初始值传给自定义属性。2.网络请求完成后将值再次传给自定义属性。

在子组件中自定义属性期待为 Object类型但实际上传过去的是 null，而null无法转为 object类型就会报错

```
Error in render: "TypeError: Cannot convert undefined or null to object
```

数组也是一样。

3. 子组件获取到的自定义属性值为对象A，在模板中使用到了 A.b.c类型的数据，控制台报错但页面正常显示。数组也是一样

原因：见2中先传过来的是 {}即空对象，所以其属性是 undefined；而网络请求完成后传来了数据，子组件就进行了对应的渲染。所以控制台报错但页面显示正常。

```
Error in render: "TypeError: Cannot read property 'c' of undefined"
```

解决：在组件的根 div中判断如果传来的对象为空则不渲染即可。

```html
<div class="base-info" v-if="Object.keys(goodsInfo).length !== 0">
```

但为什么如果在模板中只使用 A.b类型的数据即对象的直接属性就没问题？只有 A.b.c这种属性的属性才有这种问题？



如何知道网络请求来的数据渲染完成？

网络请求到的数据渲染到组件中或传递并渲染到子组件中的时间都是不确定的。所以当数据渲染不完成就不能实现的功能需要一些方法监听渲染完成。

如监听图片的加载完成

```css
<img :src="" @load="imageLoad"/>    
```



### 2. 功能需求



子组件调动父组件：自定义属性、自定义事件、组件原生事件

父组件调动子组件：$refs，

子组件调动兄弟组件：父组件作为桥梁。



自定义属性：在父组件中获取数据。

自定义事件：组件触发事件时在父组件中进行事件处理，操作父组件中的数据，还可以向父组件传递数据；

组件的原生事件：组件触发事件时在父组件中进行事件处理，操作父组件的数据，但不需要传递数据且事件为原生事件时，可以使用，更加方便

$refs：父组件获取子组件对象，可以**调用或更新**子组件的数据和方法。

与原生获取dom对象的方式( document.querySlecter()通过选择器获取 )不同的是：组件可能会进行各种嵌套，选择器可能会重复导致出错。而$refs不会出现这种问题。获取的只是本组件的ref对应的对象。

注意不能在 `created(){}`  生命周期函数中获取。因为此时还没有挂载模板

```vue
this.$refs.xxx                 //拿到的是组件对象
this.$refs.xxx.$el             //拿到的是组件对象模板中的根元素div
```







## 初始化项目



1. vue-CLI4创建项目结构  
2. 连接到GitHub
3. 在 `src/assets` 下新建 

   - css目录 `css/base.css  css/normalize.css`

   - img目录

4. 新建 `src/network/request.js` 用于配置网络请求
5. 新建 `/vue.config.js` 配置文件别名



1. 封装tabbar，挂载到 app.vue 上
2. 创建4个视图，连接到tabbar 的4个选项，并在 app.vue 显示



一个 maintabbar挂载到 app.vue，n个视图映射到 url并将 router-view放置到 app.vue，通过 maintabbar切换视图。



## home视图



#### 封装网络请求

封装 home 页面的网络请求到 `/network/home.js` 以后将 home 页面的网络请求全部写到home.js中，会返回一个promise对象，在视图中后接 `.then()`**将拿到的结果转存到home视图的数据中**。

其它视图也是一样。



需求1：改变页面返回时保留状态

实现：默认情况下切换路由时，视图会销毁。再次进去时会重新创建一个新视图，所以原视图的状态就不能保留了。添加 

```vue
<keep-alive></keep-alive>
```





#### maintabbar组件

![image-20210425093035529](images/image-20210425093035529.png)

**结构设计：** **`Tabbar.vue  TabbarItem.vue  MainTabbar.vue`**

首先要有一个 `Tabbar.vue` ，复用此组件时可能有任意个选项，所以在模板中放置一个插槽，有几个选项就放几个，在样式中通过固定定位到底部；每个选项都是相同的结构：上图下字。所以构造一个组件，添加两个插槽一个放图一个放文字即可，形成 `TabbarItem.vue`；再封装一个 `MainTabbar.vue` ,令两者成为它的子组件，这样直接把 `MainTabbar` 挂载到 `home` 中使用即可，可以让 home 页看起来更加简洁

**需求1：点击哪个选项，跳转到对应的视图**

实现： item组件点击事件中 `this.$router.push()`即可，这样每个组件都可以触发点击事件跳转。每一个组件对象如何获取自己的跳转路径？给 item组件设置自定义属性 path作为push()的目标，创建 item组件对象时传入路径即可。

需求2：点击哪个选项，该选项应用选中状态样式

实现：定义一个中间数据 isActive，判断当前页面的路径是否和每个 item组件本身的 path一致，一致则为 true。定义一个选中状态css样式 active，通过 v-bind的class语法绑定到 isActive，isActive为真时应用此选中样式。

这个组件主要用到了自定义属性 + 路由跳转







#### scroll组件

结构设计：将第三方滚动组件 better-scroll封装到一个scroll组件中，使用到滚动区时引入自己封装的这个组件。

在创建 scroll组件时需要给组件一个固定高度。

封装了一个 scrollTo方法用于将滚动区跳转到指定的高度

发射了两个自定义事件 scroll和 pullingUp，前者滚动时触发可以动态获取滚动区的高度，后者在滚动区底部上拉时触发



#### tabcontrol组件

![image-20210506151330500](images/image-20210506151330500.png)

结构设计：这里跟tabbar不同，tabcontrol里的自定义部分只是文字不同，并没有样式的区别。所以这里没必要将每一个选项封装成组件，而是通过自定义属性在父组件中创建 tabcontrol组件对象获取这些选项的文字数组，遍历显示即可



需求1：当tabcontrol滚动到顶部时吸顶

实现：首先要实时获取 scroll组件的滚动距离，当滚动距离大于tabcontrol组件到 scroll顶部的距离时吸顶。

页面中的数据都是网络请求来的不知道何时才能加载渲染完成，如果在未完成时获取高度则会小于实际高度。何时获取呢？在 `mounted()` 周期函数中获取到的距离明显短于实际距离。这是因为在调用此函数时 tabcontrol 上面的图片还没加载完成，主要是轮播图没有加载渲染完成。所以需要在轮播图的图片加载完成后再监听此时的`offsetTop`才能获取正确的距离。自定义事件---在 swiper 组件的图片监听 load 事件，当图片被加载完成后触发，并发送自定义事件到 home组件，在home组件的处理函数中通过 `this.$refs.tabcontrol.$el.offsetTop` 获取 tabcontrol 组件与顶部的距离。

swiper组件通过自定义事件告知视图图片已加载完成并在处理方法中通过`this.$refs.tabcontrol.$el.offsetTop` 获取 tabcontrol 组件与顶部的距离并保存到视图中；scroll组件通过自定义事件向视图发送实时的滚动距离，并与视图中保存的高度进行对比。将布尔值保存到 isnavfixed中。再在scroll组件之上创建一个tabcontrol组件，通过  v-show绑定到 isnavfixed，当 navbar滚动到顶部时隐藏的 navbar显示就完成了吸顶效果。

自定义事件在父组件中处理数据 + $refs调用子组件方法 + 自定义事件向父组件传递数据 

需求2：两个tabcontrol组件同步

实现：因为这是两个tabcontrol实例，两个组件的点击的选项并不同步。两个tabcontrol点击选项时都触发自定义事件将index传到home视图中来，并调用`tabClick()` 方法，我们可以在这个方法中，通过 `$refs`设置两个tabcontro组件对象内部的数据 `currentIndex` 为传进来的 `index`，从而修改选中状态。这样两个组件就能实现同步了。

需求3：点击选项，下面的 goodslist组件显示不同的数据。

实现：goodslist通过自定义属性获取视图中请求到的数据时需要传入 `this.goods[].list`

中括号内需要传入type 即是 `pop new sell`，显示不同的数据。可以通过自定义事件点击tabcontrol时将选项的 index传到视图，将 index映射成对应的 type，传给视图中的数据 `currentType`，即

`this.goods[this.currentType].list`。



#### goodslist组件

<img src="images/image-20210508101403154.png" alt="image-20210508101403154" style="zoom:50%;" />

结构设计：`goodsList.vue`  `goodsListItem.vue`

商品页的数据在服务器端的数据结构是这样的：

```javascript
goods{
  'pop': [ {page:1,list[]}, {page:2,list[]}, ... ],
  'new': [ {page:1,list[]}, {page:2,list[]}, ... ],
  'sell': [ {page:1,list[]}, {page:2,list[]}, ... ],
}
//3类数据是3个对象数组，每个数组都有多个对象
```

为什么这样设计？因为商品太多了，我们在请求商品页的数据时，总不能一次就把服务器上所有的商品页数据都请求下来吧。这样的数据结构可以对数据进行分页，如一页30个数据，每次请求时指定类型和页数，这样就可以只请求一页数据。



需求1：点击商品进入商品详情页，点击不同的商品详情页也不同。

实现：封装一个详情页视图组件，挂载到路由。点击任意商品即 `goodsListItem`都会跳转到这个视图。详情页的数据是请求来的那么如何实现请求点击的那个商品的数据呢？动态路由--每个商品数据中都有一个唯一的iid ，跳转时通过动态路由将iid传给url。在详情页组件中拿到url中唯一的id，通过这个id在详情页视图中发送数据请求并保存到视图。





#### backtop组件

结构：

需求1：点击组件scroll组件中的内容返回顶部。

实现：backtop组件监听原生click事件调用父组件方法，父组件方法中通过 `$refs` 获取 scroll 对象调用其 `scrollTo()`方法返回顶部。



由于这里的点击事件是原生事件且不需要传递 backtop组件向视图传递数据所以使用在视图模板中监听组建的原生click事件即可，而不是通过自定义事件。



## detail视图



在详情页视图中我们不需要底部的 tabbar组件了，但它是挂载到 app.vue中的，如何在其他页面中显示但不在detail页面中显示呢？

```javascript
//在路由配置 /router/index.js中
{
   path: '/detail/:iid',
   component: Detail,
   meta: {
     showTabbar: false,
   }
},
//在APP.vue的挂载处判断
<main-tabbar 
  v-show="this.$route.meta.showTabbar == undefined ? 
  true : (this.$route.meta.showTabbar)"/>
```

判断当前页面的route对象中是否有 `meta.showTabbar`，没有则为 true显示tabbar，有则取其值为false，不显示tabbar





#### navbar组件

结构设计：

需求1：点击返回按钮返回上一页

实现：给 `left` 区添加 click事件，调用 `this.$router.back()`返回上一级。注意这里不一定要返回到 home页在其它视图中也可能进入商品详情页。

需求2：点击navbar中的选项自动滚动到对应区域

思路：参与对象--navbar组件、scroll组件。通过 navbar组件去操作 scroll组件。

1. scroll组件滚动到指定区域可以在视图中通过 `this.$refs`调用 scroll组件的 `scrollTo()` 方法实现。

2. 点击一个选项滚动到一个区域就需要每一个选项和一个高度值对应。获取每一个区域的高度到一个数组；可以通过点击选项发送自定义事件将每个选项唯一的的 index值传递到视图。这样就将index和对应的高度映射了起来。在自定义事件处理方法中调用 `scrollTo()` 方法时，高度值传入 `array[index]` 就可以将一个选项和一个对应起来了。

实现：

1. 所以关键就是如何获取各部分的 y值。可以通过 `this.$ref.xxx.$el.offsetTop` 获取某组件的对应的 y值。

2. 那么在哪里获取才能取到正确的值呢？主要是 detailgoodsinfo.vue中的图片影响了 y值的计算，所以需要在所有的图片加载完之后再获取 y值。

3. 如何知道所有的图片加载完了呢？可以通过 `@load` 监听 detailgoodsinfo.vue中每张图片的记载完成，加载完一张发送一次自定义事件到 detail视图来给各区域计算高度，如果每加载完一张就给计算一次高度会造成性能浪费，所以在视图的处理函数中添加防抖让计算并赋值 y只执行一次。

需求3：滚动到对应区域时navbar的选项也会被选中

思路：上一个需求我们已经获取到了各区域对应高度的数组，我们在滚动过程中实时监听滚动高度，滚动到一个区域就改变一下navbar组件的选中选项

实现：实时获取滚动高度我们在scroll组件中定义了自定义属性，在创建 scroll组件时可以选择是否监听滚动事件，这里我们把它开启 scroll组件就会发送给自定义滚动事件到视图，在视图的处理方法中可以获取滚动距离。定义一个 navIndex，当滚动高度大于0号小于1号时，navIndex=0；当滚动高度大于1号小于2号时，navIndex=1，以此类推。

在此以前 navbar的选中状态是由内部定义的 currentIndex决定的。在此我们可以换一种做法，navbar通过自定义属性监听 navIndex替代 currentIndex。



#### DetailBaeInfo组件

子组件通过自定义属性获取并使用视图网络请求的数据时

获取服务器数据、保存到本地、绑定到自定义属性并使用这三个阶段分别有需要注意：

1. 定义一个类来接收服务器中的数据

视图从服务器获取数据并保存到本地，子组件通过自定义属性获取保存本地的数据。如果该数据只是简单的一个对象或数组什么的直接定义一个空对象数组获取即可。但如果子组件需要的数据分布在一个对象的多个子对象或子数组中呢？

第一种：视图定义一个空对象，直接接收并传给子组件这个大对象，视图中方便了但在子组件中使用数据时，就避免不了每个数据会有多层的路径；

第二种：视图要定义好多个变量接受这些数据，子组件也要定义好多个自定义属性来接受这些数据，在子组件中使用时直接使用即可，就不会有多层的路径问题。但每个数据保存到本地时还是要每个数据会有多层的路径地给本地数据，是这显然不够优雅。

所以我们在 `/network/detail.js` 中定义一个类，把所有需要的数据直接定义为类的**直接属性**。视图中新建一个实例来接受这些数据，返回子组件一个对象数据，子组件使用时需要的数据都是对象的直接属性，就不会有多层路径问题了。

2. 视图中定义用于接收服务器来的**对象**数据时，不能定义为 `xxx: null` 而是 `xxx: {}`

视图从服务器获取数据并保存到本地，子组件通过自定义属性获取保存本地的数据。自定义属性动态绑定本地数据是同步事件，要早于网络请求的异步事件。在子组件中自定义属性期待为 Object类型但实际传过去的是 null，而null无法转为 object类型就会报错

```
Error in render: "TypeError: Cannot convert undefined or null to object
```

数组也是一样

3. 子组件获取到的自定义属性值为对象A，在模板中使用到了 A.b 和 A.b.c类型的数据，控制台报错但页面正常显示。

```
Error in render: "TypeError: Cannot read property 'c' of undefined"
```



#### `DetailCommentInfo` 组件

需求1：将时间戳转化为指定格式的日期

实现：将时间戳转化为Dat对象，自己写一个utils.js封装一个转换函数把data对象转换为指定格式的日期



#### `DetailBottomInfo` 组件

需求1：点击加入购物车将此页面的信息添加到购物车视图中

实现：首先对购物车按钮添加点击事件，但 bottominfo组件无法操作视图中的数据，所以通过发送自定义事件在视图中获取购物车视图需要的数据，将其保存到一个对象中。 detail视图和 cart视图没有直接的关联，我们可以将获取到的数据保存到 vuex中，在 cart视图中获取并展示。

需求2：点击购物车弹出 toast提示

实现：

我们需要在商品数据对象确实添加到了 vuex中定义的数组中后再进行控制 toast弹出提示。那如何知道添加成功了呢？首先我们将加入购物车的处理方法定义在了 vuex的 actions中，点击添加购物车通过 `dispatch()`调用 actions中定义的方法。而actions通常是用来处理异步事件的，它的方法可以返回一个 promise对象，我们可以将添加操作定义在 promise对象中。添加成功之后调用 `resolve()` , 在`dispatch()`后接 `.then()`就可以进行添加成功后的操作了。

重点：vuex中 actions定义的方法可以返回一个 promise对象用以判断是否完成并进行相应操作



#### toast组件

首先要让 toast组件显示不同的信息肯定要传进来不同的信息，所以定义一个 message来接收需要显示的信息。并定义一个数据 time设置本次显示时间

vue-router、vuex可以在任何页面通过 `$router $store` 访问，那我们将 toast也设置成这种插件形式，在需要弹出时，只要调用其方法传入显示的信息和显示时间即可。而不是在每次使用时都需要引入，挂载，设置中间数据，使用，更加方便。

思路：创建一个组件对象挂载到 <body>标签的一个div中，这样在任何页面中都可以显示但默认不显示，并将这个组件对象添加到 `vue.prototype.$toast`中，这样任何页面都可以像 vuex router一样通过 $toast访问其 show() 传入要显示的信息和显示时间。

即toast对象在创建项目时创建并隐藏，而不是在每个使用到的视图中挂载创建。







## ShopCart视图



#### navbar组件

需求1：在 shopcart的 navbar中展示添加到购物车中商品的种类数量

思路：由于购物车视图保存的商品信息在 Vuex中是个对象数组，一个对象就是一个商品且不会重复，所以获取此数组的长度即可。

实现：在 vuex中的 getters定义一计算属性获取数组长度，在 `navbar`组件中通过 `mapGetters` 辅助函数将 getters中计算属性映射到本组件的计算属性中，模板中可直接使用。

#### checkbottom组件

需求1：点击组件切换选中不选中的样式

实现：

在 checkbottom组件中定义点击事件及布尔值变量，通过点击给布尔值变量取反来决定 checkbottom是否应用选中样式。

但这种方式带来一些问题：如何获取选中的商品数量和商品总金额？每个listitem包含两部分：商品数据对象的展示和 checkbottom。两者相对独立，把选中状态放到 checkbottom中很难确定一个对象是否被选中了也就很难获取选中数量及总金额。

所以在将一个对象添加到对象数组中时给其一个新属性 `ischecked ：true`，选中状态的改变则可以给 checkbottom组件添加原生点击事件给对象的 ischecked属性取反，在 checkbottom定义一个自定义属性监听对象的 ischecked属性即可改变选中状态。同时通过遍历cartList对象数组，对象的 ischecked属性为true则将其数量计入商品数量、将其金额计入总金额即可方便地统计。

由于使用 vuex中的数据是响应式的，点击改变商品的选中状态，商品的 ischecked属性发生改变。依赖于 ischecked属性的数据如总金额和总个数的计算属性也会重新计算并响应式地更新到组件中。

#### bottombar组件

需求1：点击 checkbottom实现全选

实现：



## 第三方组件

第三方组件碍于其安全性，都需要封装成自定义的组件来使用。  否则其一旦不维护或出现漏洞而无法继续在项目中使用时需要到每一个使用的页面去清理。

1. vue-awesome-swiper 移动端轮播图组件：

`npm install swiper vue-awesome-swiper --save`

2. better-scroll  移动端滚动区组件：

`npm install better-scroll --save`

可能的问题：

当 `better-scroll` 组件创建时，它会自动计算当时 content 区的高度与我们给定的 swiper 的固定高度进行对比，大于 swiper 高度才能滚动，否则不会滚动。那么问题来了，组件创建是同步事件，而网络请求 content 中的数据是异步事件，有可能数据还没加载完成组件就创加好了（尤其是图片内容）。如：实际高度1000，当加载到800时，组件就创建好了。 swiper 将 content 区的高度设置为800，但请求完后数据有1000。就会出现拉到800下面还有内容但拉不动的情况。添加 `observeDOM: true,` 插件即可，当content 中的dom发生变化时，重新计算content 区的高度。

3. fastclick

移动端浏览器在派发点击事件的时候，通常会出现300ms左右的延迟

原因: 移动端的双击会缩放导致click判断延迟

`npm install fastclick --save`

```js
import FastClick from 'fastclick'
FastClick.attach(document.body);        //在main.js中 
```

4. vue-lazyload

实现图片的懒加载

`npm install vue-lazyload --save`

```javascript
import VueLazyLoad from 'vue-lazyload'
Vue.use(VueLazyLoad)
```

在项目中使用时将

```html
<img :src="showImg" alt="">
```

改成

```html
<img v-lazy="showImg" alt="">
```

在项目中 goodslist中使用了图片懒加载

注意：由于需要显示图片时再加载，再项目中需要计算高度的地方不能使用懒加载。如 detail视图中商品展示图片就不能使用否则点击 navbar回调到错误的区域。





两种tab组件：

1. tabbar：选项是组件通过插槽而来

2. tabcontrol：选项通过遍历文字数组而来，即tab只有一个单组件

都需要实现点击选项切换选中状态：

需要每个选项都有一个相同的数据但值不同，都有一个共享的数据。

在 tabbar中，每个选项组件都有自己的路径且不同，且都可以获得当前页面的路径，每个选项将当前页面的路径是否等于自己的路径作为 v-bind绑定 class语法的布尔值表达式。相等时应用选中样式，不相等时不应用。

在 tabcontrol中，由于选项是遍历而来所以每个选项都有一个不同的 index，那如何获取共享的数据呢？它跟 tabbar不同，所有的选项都在一个组件中。可以定义一个数据 currentIndex默认为0，为每个选项添加一个点击事件将公共的 currentindex改为本选项的 index，同样每个选项将自己的 index是否等于 currentindex作为 v-bind绑定 class语法的布尔值表达式。相等时应用选中样式，不相等时不应用。













