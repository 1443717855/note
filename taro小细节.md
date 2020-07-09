# 学习taro的小细节 
## 进行模板创建时，默认名字就叫index这样在你引用时，可以少写一个文件名称
## 在定义文件路径重定向的时候需要在顶部定义一个const path = require('path')
* 具体可搜索博客
## 当你创建一个新的页面时
    constructor (props) {
    super(props)
    this.state = { date: new Date() }}(非必要)
* state可以在页面中直接写state={}
## 能够在布局中掺杂js语法(和js区别)
## 状态变量定义在state对象中，在render这个方法中可以直接引用
* 通过this.state.属性名来获取你定义在state对象中的属性
## 方法直接定义，如果你想调用的话也是在render中可以直接引用
* onClick={this.方法名}来调用方法
* 当你想要向方法中传递参数时，要注意：
    + 例如henadleClick(this,参数1，参数2)一定要加上this，方法才能获取到后面传递的参数
    + 其次 如果你想拿到这个事件的事件对象，e一定要放在参数的最后
## 生命周期和微信小程序的很像 可以自行参考taro文档的介绍
* https://taro-docs.jd.com/taro/docs/2.2.8/tutorial#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F
## 修改state中的值 其实和微信小程序中修改data中的值很类似
 * 一定要使用this.setState({属性名：属性值})进行更改
 * 其次，这个this.setState({})这个方法，修改值是异步进行的。意思就是说你修改了值可能不会立刻能够得到修改的值，如果你想打印出修改后的值需要使用它的第二个参数传入一个callback 如下：
    + `this.setState({属性名：属性值},(state)=>{在这里面可以拿到state修改之后的值})`

## taro 引入webpack-bundle-analyzer可视化打包大小插件
* 在小程序的mini中添加 然后走运行就可以在浏览器中看到对应模块大小
```javascript
    webpackChain (chain, webpack) {
      chain
        .plugin("analyzer")
        .use(require("webpack-bundle-analyzer").BundleAnalyzerPlugin, []);
    }
```
## wxParse在解析富文本的时候会加一个bindtap属性导致a标签的href失效 暂未解决
## taro 打包时wxParse和bdParse不能自动打包进对应的小程序包中 即便是我已经引用了包中的文件
# 缺少 Cannot find module '@babel/core'解决方法
* 升级框架到npm i -g @tarojs/cli@2.1.5 
## taro-f2这个东西升级到2.1.5之后interface编译不了啊 保留字段 顺着这个我添加了ts-loader
yarn add -D ts-loader
下面是我加的小程序mini中的配置但是并没有什么用  （尝试把ts改成tsx也没用）因为interface这个字段是在jsx中的
我想的是taro好像原来就支持ts语法  目前没有解决我就把版本降到2.0.0了
```javascript
webpackChain (chain, webpack) { // 模块可视化
      // chain
      //   .plugin("analyzer")
      //   .use(require("webpack-bundle-analyzer").BundleAnalyzerPlugin, []);
      chain.merge({
        module: {
          rules: {
            myloader: {
              test: /\.ts$/,
              use: [{
                loader: 'ts-loader',
                options: {}
              }]
            }
          }
        }
      })
    },
```