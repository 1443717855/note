1. 首先升级脚手架
	# 使用 Taro 自己

	$ taro update self 2.0.0

	# 如果你使用 NPM

	$ npm update -g @tarojs/cli@2.0.0

	# 如果你使用 Yarn

	$ yarn global upgrade @tarojs/cli@2.0.0

2. 之后在你的项目目录里运行以下命令来升级依赖：
	$ taro update project 2.0.0

3. 安装 @tarojs/mini-runner 依赖
	# 如果你使用 NPM

	$ npm install --save-dev @tarojs/mini-runner@2.0.0

	# 如果你使用 Yarn

	$ yarn add -D @tarojs/mini-runner@2.0.0

4. 调整全局配置文件index.js
	babel、csso、uglify 等配置从 plugins 配置中移出来
	小程序配置名称由weapp改成mini

5. 异步编程调整
	Taro 2.0 中开启 async functions 支持不再需要安装 @tarojs/async-await，而是直接通过 babel 插件来获得支持。
	可以先删除@tarojs/async-await 包
	# 如果你使用 NPM

	$ npm uninstall @tarojs/async-await

	# 如果你使用 Yarn

	$ yarn remove @tarojs/async-await

	在你的 App.jsx/tsx 里删除 import '@tarojs/async-await'。

6. 在项目根目录下安装包 babel-plugin-transform-runtime 和 babel-runtime。
	
	# 如果你使用 NPM

	 npm install --save-dev babel-plugin-transform-runtime
	$ npm install --save babel-runtime

	# 如果你使用 Yarn

	$ yarn add -D babel-plugin-transform-runtime
	$ yarn add babel-runtime

7. 随后修改项目 babel 配置，配置插件 babel-plugin-transform-runtime。
	
	babel: {
  sourceMap: true,
  presets: [['env', { modules: false }]],
  plugins: [
    'transform-decorators-legacy',
    'transform-class-properties',
    'transform-object-rest-spread',
    ['transform-runtime', {
      "helpers": false,
      "polyfill": false,
      "regenerator": true,
      "moduleName": 'babel-runtime'
    }]
  ]
}

# end #