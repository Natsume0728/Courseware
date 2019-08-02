# ng

## 设计原则

- YAGNI  
    You Aren't Gonna Need It，你不会需要它；不写不需要的功能
- KISS  
    Keep It Simple and Stupid，让你的代码越简单/傻瓜越好
- OCP  
    Open Close Principle，开闭原则，对外界修改封闭(不允许修改已有代码)，对外界的扩展开放
- High Cohesion，Low Coupling  
    高聚合，低耦合；功能相关代码紧密在一起；功能不相干代码拆分越明确越好
- 迪米特法则/最少知识原则  
    一个对象/组件，数据/操作越少越好

## Angular

>由Google在2009年创建的MVVM框架，适用于中大型的企业级SPA应用。

- [V1.x官网](https://angularjs.org/)   Angular.js用JS编写
- [V2.x~8.x官网](https://angular.io/)  Angular用TS编写
- [V2.x~8.x中文网](https://angular.cn/)  

提示：V1到V2的升级变化非常大！  
V1支持SCRIPT直接引入和脚手架方式；  
V2开始只支持脚手架方式。  

注意：Angular 8.x要求Node.js版本必须是10.9以上！

## 修改npm默认下载地址

如果使用NPM从官方网站下载NPM包总是失败，可以把默认下载地址改为国内淘宝网镜像：

- 查看当前下载地址：  `npm  config  get  registry`
- 默认值为： <https://registry.npmjs.org/>
- 修改为淘宝网NPM镜像：  
  `npm  config  set  registry=https://registry.npm.taobao.org/`

## 创建第一个Angular项目

1. 安装Node.js和NPM  
    Node.js版本必须>=10.9
2. 安装全局的Angular脚手架工具  
    `npm  i   -g   @angular/cli`  
    默认会在C:\Users\web\AppData\Roaming\npm目录下安装ng.cmd可执行文件及其相关文件
3. 运行全局脚手架，创建一个Angular空白项目  
    `ng  new  myngapp01`
4. 进入项目根目录，运行该项目（Node.js项目）  
    `npm  start`  或者      `ng  serve`

### 模块

- Vue.js项目的主配置文件： <span style='color:red'>vue.config.js</span>
- Angular项目的主配置文件：  <span style='color:red'>angular.json</span>
- ES6中有“模块”的概念：  export/export default、  import..from..
- Vue.js中无自己的“模块”概念——项目是由自定义组件构成；
- Angular中有自己的“模块”概念——项目是由自定义组件构成，每个组件都要放在一个特定的Module中

## Angular项目引导启动流程

1. 根据angular.json查找系统运行入口文件：main.ts
1. main.ts启动主模块： AppModule
1. 在主模块中引导启动主组件：AppComponent
1. 主组件中声明了模板和样式，最终渲染在index.html中 \<app-root/>

## Angular核心概念之一 : 组件

 >Component(组件)，就是一段可以复用的页面片段，如轮播广告、手风琴、下拉菜单.......；  
每个组件内有自己专用的HTML片段、CSS样式、JS数据和操作。  
Component = Template + Style + Script  

 提示：**Angular中每个组件(Component)必须处于某个模块(NgModule)中！！**  

### 自定义组件的步骤

1. 创建一个ts文件  
    例如： src/app/myc01.ts
2. ts文件中声明并导出一个class  

```ts
    @Component({
    selector: 'app-myc01',      //标签名
        template: '<h1>我的组件01</h1>'     //组件模板
    })
    export class MyComponent01 {  }
```

3. 在某个模块中声明该组件，否则无法使用该组件  
    `@NgModule({     declarations: [ MyComponent01 ]  })`  
4. 在当前模块内的其它组件的模板中使用该组件  
    `//app.component.html`  
    `<app-myc01></app-myc01>`  

### `ng  g component  组件名`

可以使用Angular脚手架提供的 `ng  g  component  组件名`  来自动的创建一个组件所需要的文件；  

若没有成功安装全局命令`ng`，也可以使用 `npx  ng  g  component  组件名` 。  
（`NPX`是Node.js安装包提供的一个命令，可用于执行node_modules下的可执行文件）

## Angular核心概念之二:数据绑定

>Data Bingding：把脚本中的数据(称为Model模型)，绑定到HTML(称为View视图)，未来只要Model发生改变，则View自动更新。

### Angular中数据绑定的呈现方式

- 插值语法/大胡子语法，绑定到innerHTML：{{ }}  
    `<any>{{expression}}</any>`
- 属性绑定：[ ]  
    `<any [attr]="expression">`  
    `<any attr="{{expression}}">`
- 事件绑定：( )  
    `<any (event)="fn( )">`  

 注意：**事件绑定中函数后的( )不能省略**！

 说明：(1)插值语法中可以使用<span style='color:green'>算术运算吗？比较运算符？逻辑运算符？三目运算符？调用对象的方法吗？</span><span style='color:red'>自增/自运算符？创建新对象吗——{{}}中不能出现new？</span>

### 数据绑定相关的指令

- innerHTML绑定：{{  }}  
- 属性绑定：[ attr ] = ""
- 事件绑定：( click ) = "fn( )"
- 循环绑定指令：*ngFor
- 选择绑定指令：*ngIf  
- 选择绑定指令：[ngSwitch]  *ngSwitchCase  *ngSwitchDefault
- 样式绑定指令：[ngStyle]  
- 样式绑定指令：[ngClass]
- 双向数据绑定指令：

#### 面试题：Angular中指令分为哪几类

- 组件指令    `<myc01></myc01>`  
  `Component  extends  Directive`，组件继承自指令，组件是有模板的指令
- 结构型指令  
  可以影响当前的DOM结构的指令；所有结构型指令都以 * 开头
- 属性型指令  
  不会影响DOM结构，只会影响当前元素的特征，如样式；所有的属性型指令都用 [ ] 括起来！

## Angular核心概念之三:指令(Directive)

>指令：是一种特殊的模板页面内容，可以对页面执行特殊的处理；

- 循环绑定指令： *ngFor  
`<any *ngFor="let  tmp  of  集合对象">`  
- 选择绑定指令： *ngIf  
`<any  *ngIf="expression">`  
提示：***ngIf会影响DOM结构**  
- 选择绑定指令： [ngSwitch]   *ngSwitchCase  *ngSwitchDefault  

```html
  <any  [ngSwitch]="变量名">
    <any  *ngSwitchCase="值">....</any>
    <any  *ngSwitchCase="值">....</any>
    ...
    <any  *ngSwitchDefault>....</any>
  </any>
```

- 样式绑定指令：[ngStyle]  
   `<any [ngStyle]="obj">`  
- 样式绑定指令：[ngClass]  
`<any [ngClass]="obj">`  

### (了解)如何自定义指令

  提示：可使用工具 ng  g  directive 指令名 快速的创建一个指令

```html
  <div  appNeedStrong>....</div>

  @Directive({ selector: 'appNeedStrong' })
  export class MyDirective {
  contructor( el: ElementRef){
    el.nativeElement.xxx....
  }
  }
```

## Angular中的双向数据绑定

- 方向1：Model  =>  View
- 方向2：View  =>  Model

Angular中实现双向数据绑定的方法：  
`<input  [(ngModel)] = "userName">`

  提示：**ngModel指令处于FormsModule，必须在当前模块中声明导入才能使用**：

```ts
  import { FormsModule } from '@angular/forms';
  @NgModule({
    imports: [ FormsModule ]
  })
```

如果想监视模型数据的改变（就像Vue.js中的watch函数），可以使用 ngModelChange事件：  
`<input  [(ngModel)]="userName"   (ngModelChange)="fn( )">`

## Angular核心概念之四:管道

  Vue.js中的过滤器(filter)： `<p>{{ 1 | sex('zh') }}</p>`  
  Angular中的类似的概念称为管道(pipe)：`<p>{{ 1 | sex:'zh' }}</p>`  

Vue.js没有内置任何过滤器；但Angular内置了很多好用的管道：  

- lowercase：把数据转换为小写形式
- uppercase：把数据转换为大写形式
- slice：获取字符串或数组中的一部分
- json：把对象转换为JSON字符串
- date：把日期/数字转换为特定格式的日期字符串
- number：数字格式化(每三位加逗号，并指定小数位数)
- currency：把数字以货币形式显示

### 自定义管道

  工具命令：  `ng   g   pipe  管道名`

```ts
  @Pipe({
  name: 'sex'
  })
  class SexPipe {
  transform(val, args){
    return ...;
  }
  }
```

## (重点/难点)父子组件间的数据传递

`ng  g   component   parent`  
`ng  g   component   child`  
  parent.component.html:  
  \<app-child>\</app-child>  

### 父组件给子组件传递数据： 父=>子 —— Props Down  

- 子组件声明自己专有的属性  
    `@Input()     //Input装饰器把下面的属性变为“输入型属性”`  
    `userName: string;`

```ts
// in 子组件 ts 文件

import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child-blog',
  templateUrl: './child-blog.component.html',
  styleUrls: ['./child-blog.component.css']
})
export class ChildBlogComponent {
  //声明子组件的专有属性：userName
  @Input()   //输入型属性，可以被父组件输入值
  userName:string   //子组件属性的值来自于父组件
}
```

- 父组件使用子组件的专有属性赋值——值为父组件的模型数据  
    `<app-child  [userName]="myName">`  

### 子组件给父组件传递数据： 子=>父 —— Events Up  

- 子组件声明并触发事件，触发时携带自己的数据  
  `@Output()    //声明输出型属性`  
  `unameEvent = new EventEmitter();`  

```ts
//in 子组件 ts 文件

import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child-update',
  templateUrl: './child-update.component.html',
  styleUrls: ['./child-update.component.css']
})
export class ChildUpdateComponent {
  userInput:string = ''
  //事件发射器属性：可用于对外界发射事件对象
  @Output()   //输出型属性，必须是“事件发射器”
  unameEvent = new EventEmitter(); 

  doClick(){
    console.log('用户输入了：', this.userInput)
    //向外界发射事件，并携带数据
    this.unameEvent.emit( this.userInput );
  }
}
```

`this.unameEvent.emit( 123 );`  

```html
<!-- in 子组件 html-->

CHILD-UPDATE:
<input [(ngModel)]="userInput">
<button (click)="doClick()">  修改签名  </button>
```

- 父组件监听子组件的事件，并提供处理函数接收事件数据  
  `<app-child  (unameEvent)="doEvent($event)" >`  

```ts
//in 父组件 ts 文件

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './parent.component.html',
  styleUrls: ['./parent.component.css']
})
export class ParentComponent {
  //父组件中的模型数据
  myName:string = '苍茫大地'

  //处理子组件事件的方法
  doUnameEvent( data ){
    console.log('父组件正在处理子组件事件：', data)
    //把子组件传递给父组件的数据加以利用
    this.myName = data;
  }
}
```

  `doEvent( data ){  ....  }`

```html
<!-- in 父组件 html-->
<h1>PARENT: {{myName}}的个人网站</h1>
<hr>

<app-child-update (unameEvent)="doUnameEvent($event)"></app-child-update>
```

## 服务和依赖注入

>Angular认为：  
>>Component：组件，仅应该只负责视图，只参与展示；与展示无关的语句都应该剥离出去；例如：做日志、计时、网络数据访问...
>>>Service：服务，就是一个简单的对象，负责执行从组件中剥离的与视图无关的操作，例如：做日志、计时、网络访问....
  
  创建服务： `ng   generate  service  服务名`

inject：打针，注入  
injectable：能被注入给别人的  

### Angular创建对象的两种方式

- 手工创建  
    `var logger = new LoggerService();`  
    `logger.log('用户增加了一个商品');`  
- 依赖注入(Dependency Injection)  
    `constructor(logger:LoggerService){`  
        `logger.log('用户增加了一个商品')`  
    `}`  
在构造方法中声明需要依赖某个对象，且该对象是“可以被注入的(@Injectable)”,  
那么Angular就会自动创建依赖的对象，并注入给当前构造方法

## Angular核心概念之六 —— 服务和DI

- Component：负责视图的数据绑定/事件处理
- Service：负责从组件中剥离的与视图无关的任务，如日志、计时、网络访问....
  
注意：Angular中的依赖注入是基于构造方法的参数类型，而与先后顺序无关  
  创建服务：  

```ts
  @Injectable( {
  //可以被注入给某个组件
  //Injector/Provider：注入器/服务提供者，负责创建服务对象并注入给组件，
  //Angular会自动为每个服务创建必需的注入器
  } )
  export class LoggerService{
  }
```

### 面试题

Angular中的Service可以在哪里被提供/Service的提供者/注入器有哪些？  

- 方式1：声明服务时提供——根模块中提供的服务对象是整个应用中“单例的”

```ts
   @Injectable({
        providedIn: 'root'
   })
   export  class  LoggerService{  }
```

- 方式2：在模块中提供——在当前模块中的所有组件共用同一个服务对象

```ts
   @Injectable()
   @NgModule({
       providers: [ LoggerService ]
   })
```

- 方式3：在组件声明中提供——该服务仅能作用于当前组件，且每个组件都有自己专有的服务对象

```ts
  @Component({
     selector: 'app-myc01',
     template: '  ',
     providers: [ LoggerService ]
  })
```

### 面试题：前端技术中有哪些异步请求方案

- 原生XHR： 1234
- jQuery封装： $.ajax( )   基于回调函数=>回调地狱
- Axios：底层还是XHR，基于Promise，可以避免回调地狱
- Angular HttpClient服务：底层还是XHR，基于Observable
- ES2016新方案：Fetch：底层不是XHR！就是fetch对象！不支持请求打断、请求排队！

## Angular中异步请求服务器端数据

>HTTPClient Service：是Angular官方提供的异步请求工具

### 使用步骤

1. 在主模块中引入HttpClientModule——会提供HttpClient服务的注入器  

```ts
	@NgModule({
		imports: [ HttpClientModule ]
	})
```

2. 在需要使用异步请求模块中声明依赖HttpClient服务  
  `constructor(private http: HttpClient){}`
3. 调用HttpClient提供的异步数据请求服务  
  - this.http.get( )
  - this.http.post( )
  - this.http.put( )
  - this.http.delete( )


马走日象走田		=>		双炮枪等招数
JS语言基础语法	=>		JS设计模式(23+1)


## Rx.js和Observable对象

>Angular中HttpClient服务底层基于Rx.js第三方模块
>>官方：RxJS 是 Reactive Extensions for JavaScript 的缩写，是一个基于可观测数据流在异步编程应用库。RxJS 是 Reactive Extensions 在 JavaScript 上的实现。一般说到RxJS，都会讲他是基于流的响应式的结合观察者和迭代器模式的一种库。

**Observer观察者模式（也称为“订阅-发布”模式）**：  
  乙方声明“订阅(subscribe)”甲方；  
  在未来的某个不确定时间，甲方“发布(publish)”新消息，乙方会立即接到通知。  

  HttpClient服务采用了“观察者/订阅-发布模式”，其最核心对象为：  
  `let  obj  =  new  Observable( );  //可被观察的对象`  
  `//可以关注/订阅“可被观察的”对象`  
  `obj.subscribe(  ( )=>{ //收到订阅消息时的回调函数 }   )`

## Angular中组件的声明周期钩子函数

>Hooks Function：声明好的特定的函数，到了指定的时间点，就会被自动执行
>>LifeCycle Hooks Function：在组件的不同生命阶段会自动执行的函数

1. constructor( )：构造方法，执行且仅执行一次  
2. ngOnChanges( )：组件的输入属性值发生赋值或改变  
3. **ngOnInit( )**：组件正在初始化，一般用于组件刚加载完成时执行的业务操作，如获取页面数据；执行且仅执行一次  
4. ngDoCheck( )：组件正在执行变化检查  
5. ngAfterContentInit( )：组件内容初始化之后  
6. ngAfterContentChecked()：组件内容被重新检查后  
7. ngAfterViewInit( )：组件视图初始化之后  
8. ngAfterViewChecked()：组件视图被重新检查后  
9. ngOnDestroy( )：组件即将从DOM树上销毁，用于释放定时器、取消订阅...执行且仅执行一次  

## Angular核心概念之七 —— 路由和SPA应用

>Single Page Application，单页应用——整个应用中只有一个完整的HTML页面，其它所有的“页面”其实都是一段HTML片段

- SPA应用的优点：  
  (1)DOM树只需要创建一次，“页面切换”只是在切换部分元素  
  (2)便于实现“过场动画”——多页应用不可能做到
- SPA应用的不足：  
  (1)不便于实现SEO优化  

### SPA应用的核心——路由词典(把一个地址和一个组件对应起来)

```ts
  [
      { path: 'index',  component: ...}
      { path: 'product/list',  component: ...}
      { path: 'user/login',  component: ...}
      .....
  ]
```

### SPA应用的原理

>框架根据客户端请求的路由地址，异步加载对应的组件内容，替换之前的组件内容。

### 使用Angular中的路由步骤

1. 提前准备好路由组件  
  `ng  g  component  index`  
  `ng  g  component  productList`  
  `ng  g  component  productDetail`  
2. 在根模块中创建路由词典  
  `var  routes = [ {path:'product/list', component: ...} ]`  
3. 在根模块引入路由模块，注册路由词典

```ts
  @NgModule({
    imports: [ RouterModule.forRoot(routes) ]
  })  
```

4. 在根组件的模板中声明路由组件的占位符  
  `<router-outlet></router-outlet>`  
5. 让客户端请求路由地址  
  `http://127.0.0.1:4200/product/list`

### 路由词典配置

```ts
let routes = [
  {path:'', component:IndexComponent},
  {path:'index', component:IndexComponent},
  {path:'product/list', component:ProductListComponent},
  {path:'product/detail', component:ProductDetailComponent},
  {path:'user/center', component:UserCenterComponent},
  {path:'**', component:NotFoundComponent},
]
```

注意：路由词典中的路由path不能以 '/' 开头！但是，路由跳转时指定的路径最好都以 '/' 开头！

### 路由跳转

  从一个路由地址跳转到另一个有两种方法：

- 方式1：编程方式  
  contructor( private router: Router ){ }  
  ...  
  this.router.navigateByUrl( '...' )  
- 方式2：模板方式  
  \<any  routerLink="...">  
  注意：routerLink指令可以用在任何元素上，如DIV、A、BUTTON  

### 路由参数

  在路由的path属性中，有些部分固定不变，有些部分需要动态变化：  
`{  path:  'product/detail/:pid',  component: ...  }`  

>路由参数：路由地址中的变量

使用步骤：
1. 路由词典中设置 路由参数：  
  `{ path:  'product/detail/:pid',  }`
2. 路由跳转时提供 路由参数值：  
  `<any routerLink="/product/detail/35">`
3. 在目标组件中读取当前路由的参数
```ts
  constructor( private route: ActivatedRoute ){  }
  ngOnInit(){
    this.route.params.subscribe( (data)=>{
      data.pid  就是路由参数的值
    })
  }
```

### 路由嵌套

>在一个路由组件内部，有部分内容固定，另一区域中的内容可以切换不同的子组件

路由词典：

```ts
  let  routes = [
  {
    path: 'user/center',
    component: UserCenterComponent,
    children: [
      { path: 'myinfo', component: ...},
      { path: 'headpic', component: ...},
      { path: 'security', component: ...},
    ]
  }
  ]
```

路由出口：  
  app.component.html:   `<router-outlet></router-outlet>`  
  user-center.component.html:   `....<router-outlet></router-outlet>....`

### 路由守卫

>Guard：护卫，守护者  
有些路由地址只有在特定条件满足的情况下才允许访问，不满足的情况下禁止访问——如是否登录、是否充值、是否满足时间段限制....  
>>对访问条件是否满足而进行设置，满足的话，就让访问路由组件；  
否则就不让访问 —— 这种对象成为“路由守卫对象”。

#### 使用方法

- 创建一个路由守卫：

```ts
  @Injectable({   providedIn: 'root'  })
  class  XxxGuard  {
    canActivate(){ //组件是否允许被激活
      ......
      return true / false ;
    }
  }
```

- 使用路由守卫

```ts
  [{
      path: 'user/center',
      component: UserCenterComponent,
      canActivate: [  XxxGuard ]
      children: [ ... ]
  }]
```

练习：创建一个路由守卫： TimeCheckGuard，
  作用：如果当前时间是18:00~24:00，允许用户访问user/center，否则禁止访问

## 移动端应用的种类

- Native App：  
  原生App，指使用Java/Kotlin为Android、OC/Swift为iOS开发应用程序，直接运行与手机操作系统上  
  - 优势：运行速度快  
  - 劣势：两套代码不跨平台，且必须下载
- Web App：  
  使用HTML/CSS/JS技术编写类似原生App的应用，代码运行于手机中的浏览器(如WebView)中  
  - 优势：无需提前下载、一套代码到处运行  
  - 劣势：运行效率低、不能访问手机底层系统服务
- Hybrid App：  
  使用HTML/CSS/JS技术编写类似原生App的应用，并混入部分Java/OC等驱动代码以调用系统底层服务，最终运行于操作系统中  
  - 优势：结合了前两种的优势  
- Dart / Flutter —— 代表着未来  

## 基于Angular的UI组件库

### Angular相关的组件库

- Ionic
- Material
- Zorro
- Zorro Mobile

>[Link : Ionic官网](https://ionicframework.com/)  
>>Ionic是一个基于HTML/CSS/JS技术的，创建混合App的UI组件库技术。  
底层可以不依赖于任何框架(引入.css和.js就可以运行)，也可以与Vue.js、React、Angular框架整合在一起，作为它们的第三方组件库使用
>>>第三方提供的一套WEB UI组件库，适用于编写Hybrid App。可以与Angular、Vue、React组合使用，也可以单独直接使用。  
>>>>Ionic CLI = Angular CLI + UIModule + 移动端打包工具....

### Ionic 使用方法

1. 下载全局脚手架工具  
`npm  i   -g   ionic`
2. 选择一个目录，运行脚手架工具在当前目录下创建一个项目  
   - ionic  start   项目名   blank
   - ionic  start   项目名   tabs
   - ionic  start   项目名   sidemenu  
**创建好项目后会自动调用npm  i下载所依赖的第三方模块**
3. 进入项目目录，运行它  
cd  项目名  
npm  start  
4. 用(手机)浏览器访问项目  
`http://127.0.0.1:4200`

#### Ionic的九种主题色——color

- primary(蓝白)
- secondary(青白)
- tertiary(偏紫白)
- danger(红白)
- warn(黄白)
- success(绿白)
- dark(黑白)
- medium(灰白)
- light(亮色)

#### Ionic App的页面布局

  <ion-app>
	ion-header > ion-toolbar > ion-title > 标题
	ion-content[padding] > 内容
	ion-footer > ion-toolbar > ion-title > 内容
  </ion-app>
  --------------------------------------------------------
  Ionic主体中的“栅格布局系统”——仿Bootstrap3：
  <ion-grid >
	<ion-row>
		<ion-col  no-padding  size="宽"  offset="偏移"  push="右推"  pull="左拉" >
		</ion-col>
	</ion-row>
  </ion-grid>

Module：模块
Model：模型，MVVM中第一个M
Modal：模态对话框——只要不关闭就无法使用其父窗口

#### Ionic提供预定义组件

  Icon：图标  <ion-icon name="">
  Button：按钮  <ion-button>
  Badge：徽章  <ion-badge>
  Card：卡片  ion-card > ion-card-header + ion-card-content
  Alert：警告框，必须使用AlertController创建并呈现
  Modal：模态框，必须使用ModalController创建并呈现
  Item：列表项
  List：列表
  InfiniteScroll：无穷滚动组件，滚动到底部时加载更多内容
  Refresher：刷新器，从顶部显示加载更多内容


课后任务：
(1)读取Ionic手册，完成InfiniteScroll和Refresher组件的使用
  注意：需要使用http://www.codeboy.com/data/product/list.php提供的跨域数据。
(2)自学Ionic中Slides组件和Tabs组件的使用

























## TypeScript语法知识

- 类型声明：  
class中的成员（属性、方法）、参数的参数都可以声明类型：

```ts
class Book{
   price: number = 12.5
   add(n: number): void{  }
}
```

- TS中的新类型：接口(interface)  
  接口是一种特殊的class，用于规定一个对象“必须具备”哪些功能  

```ts
  interface  Runnable{
      run( );
      stop( );
  }
  class Car  implements  Runnable{
      run( ){  ....   }
      stop( ){  ....   }
  }
```

- 类成员(属性/方法)的访问修饰符  
  - private：私有成员，只能在当前类内部使用；class中的属性一般都应该声明为私有的或被保护的！
  - protected：被保护的，只能在当前类内部以及子类中使用
  - public：默认值！公共成员，可以被任何类使用；class中的方法一般声明为公共的！
- 类属性的声明/赋值方式

```ts
class Book{
   private price: number = 0
   public constructor( price: number ){
       this.price = price
   }
}
```

上面的代码可以简写为：  

```ts
class Book{
   //构造方法中的形参前加private/protected/public此形参自动变为一个同名属性，且自动赋值
   public constructor( private price: number ){
       //此处无需写 this.price = price
   }
}

var  book1 = new Book( 100 )
```
