+ 模块
  + node.js的模块基于Commonjs规范

  		// Tool.js
		function add(x,y){
		return x+y;
		}
		module.exports = {
		add:add
		} 
  + 导入模块

  		const tool = require("Tool");
		tool.add(2,3); //5
+ 包
  + 包是非单一文件的模块，可将多个文件打包成一个模块，文件夹名称既是包的名称
  + package.json指定包的入口文件(第一优先级)

  		//package.json定义如下
		{
			"name":"cat", //指定包名称
			"main":"./main.js" //指定入口文件
		}
  + 约定根目录下的index.js作为入口文件(第二优先级)
+ 包路径查找
  + 相对路径：通过指定的相对路径查找(node.js中以"."作为相对路径标记)

  		const tool = require("./Tool");
  + 非相对路径：从自身目录开始依次向上查找"node_modules"文件夹，直到文件根目录,最后到全局文件目录
+ 文件定位
  + 查找同名文件，再依次以.js .json .node文件后缀去匹配具体的文件
  + 没找到同名文件时，再依次查找同名文件夹，查找到同名文件夹后再以包的规则去查找入口文件



+ npm
  + package.json
  + init：目录内初始化一个package.json文件

		npm init;
  + dependencies：使用本模块所依赖的模块

		// 将安装的模块作为本模块的依赖模块
		npm install <package name> --save;
  + devDependencies：模块开发过程中所依赖的模块

		npm install <package name> --save-dev;

  + install/uninstall
	
		// 全局安装/删除
		npm install -g <package name>;
		npm uninstall -g <package name>;
		// 本地安装/删除
		npm install <package name>;
		npm uninstall <package name>;
  + update

		// 本地模块
		npm update <package name>;
		// 全局模块
		npm update -g <package name>;
  + search：搜索模块仓库

  		npm search <package name>;