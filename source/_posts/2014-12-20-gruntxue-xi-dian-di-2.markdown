---
layout: post
title: "Grunt学习点滴2"
date: 2014-12-20 16:43:56 +0800
comments: true
categories: 
---

#Grunt实战

##简单样例

1. 简单注册一个foo的任务

```javascript
module.exports = function(grunt) {
	  //注册一个foo的任务     grunt.registerTask('foo', function() {       grunt.log.writeln('foo is running...');	  }); 
};
```

运行命令grunt foo就可以执行foo任务

```bash
$grunt foo
Running "foo" task
foo is running...

Done, without errors.
```

2.注册多个任务

```javascript
module.exports = function(grunt) {

	  //注册一个foo1的任务     grunt.registerTask('foo1', function() {       grunt.log.writeln('foo1 is running...');	  }); 
	  
	  //注册一个foo2的任务
	  grunt.registerTask('foo2', function() {       grunt.log.writeln('foo1 is running...');	  }); 
	  
	  //默认grunt执行default任务
	  grunt.registerTask('default', ['foo1','foo2']); 
};
```

执行default任务:

```
//default默认任务 可以省略
>grunt
Running "foo1" task
foo1 is running...

Running "foo2" task
foo1 is running...

Done, without errors.
```


3. 初始化变量和获取变量的值

```javascript
module.exports = function(grunt){
	//初始化任务bar中的变量foo
	grunt.initConfig({
		bar: {
			foo: 42
		}
	})
	
	grunt.registerTask('bar', function(){
		//获取变量bar {foo:42}
		var bar = grunt.config.get('bar');
		var bazz = bar.foo +7;
		grunt.log.writeln('Bazz is' + bazz);
	})

}
```

运行结果:

```bash
grunt bar
Running "bar" task
Bazz is 49

Done, without errors.
```

##查找bug和样式错误
JSHint是一个javascript代码验证工具

测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-contrib-jshint
	|__src
	|	|__demo.js
	|__Gruntfile.js
	|__package.json
	
```

安装JSHint工具

```
npm install grunt-contrib-jshint --save-dev
安装完成后my-project/node_modules/grunt-contrib-jshint有个REAEDME.md文件 相当于API
```

测试代码

```javascript
//Gruntfile.js
//参数curly:必须用括号包裹 不能写这种代码while (notEnd())
//doSomething();
//参数eqeqeq: 对于简单类型，使用===和!==，而不是==和!=
 module.exports = function(grunt) {
	//加载jshint模块
	grunt.loadNpmTasks('grunt-contrib-jshint');

	// Project configuration.
	grunt.initConfig({
		jshint: {
			options: {
				curly: true,
				eqeqeq: true
			},
			all: ['src/demo.js']
		}
	});
	// Define the default task
	grunt.registerTask('default', ['jshint']);
};

//demo.js
if(7 == "7") alert(42);

```

测试结果

```bash
>grunt
Running "jshint:all" (jshint) task

   src/demo.js
      1 |if(7 == "7") alert(42);
                ^ Expected '===' and instead saw '=='.
      1 |if(7 == "7") alert(42);
                      ^ Expected '{' and instead saw 'alert'.

>> 2 errors in 1 file
Warning: Task "jshint:all" failed. Use --force to continue.

Aborted due to warnings.
```

修改demo.js为

```javascript
if(7 === '7'){
	alert(42);
}
```

运行结果

```bash
>grunt
Running "jshint:all" (jshint) task
>> 1 file lint free.

Done, without errors.
//没有错误
```

##Transcompilation
像Dart、CoffeeScript、TypeScript 和 JavaScript都能翻译成javascript语言,grunt可以简单配置自动翻译

###Coffeescript-->Javascript

测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-contrib-coffee
	|__src
	|	|__demo.coffee
	|__Gruntfile.js
	|__package.json
	
```

安装grunt-contrib-coffee 

```bash
npm install grunt-contrib-coffee --save-dev
```

测试代码

```javascript
module.exports = function(grunt) {
	//加载coffee模块
	grunt.loadNpmTasks('grunt-contrib-coffee');

	// Project configuration.
	grunt.initConfig({
		coffee: {
			compile: {
				files: {
					'dest/demo.js': 'src/demo.coffee'
				}
			}
		}
	});
	// Define the default task
	grunt.registerTask('default', ['coffee']);
};
```

执行结果:

```
//结果显示自动创建文件dest/demo.js
>grunt
Running "coffee:compile" (coffee) task
>> 1 files created.

Done, without errors.

```

###Jade-->Html
测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-contrib-jade
	|__src
	|	|__demo.jade	
	|__Gruntfile.js
	|__package.json
	
```

安装grunt-contrib-jade 

```bash
npm install grunt-contrib-jade --save-dev
```

测试代码

```javascript
module.exports = function(grunt) {
	//加载jade模块
	grunt.loadNpmTasks('grunt-contrib-jade');

	// Project configuration.
	grunt.initConfig({
		jade: {
			compile: {
				files: {
					'dest/demo.html': 'src/demo.jade'
				}
			}
		}
	});
	// Define the default task
	grunt.registerTask('default', ['jade']);
};
```

执行结果:

```
//结果显示自动创建文件dest/demo.html
> grunt
Running "jade:compile" (jade) task
>> 1 file created.

Done, without errors.

```

Stylus-->CSS
Haml,Sass,Less等等

##Minification(代码压缩)
减少网络流量,为了提高网站性能和用户访问速度

- Javascript: [https://github.com/gruntjs/grunt-contrib-uglify](https://github.com/gruntjs/grunt-contrib-uglify)
- CSS: [https://github.com/gruntjs/grunt-contrib-cssmin](https://github.com/gruntjs/grunt-contrib-cssmin)
- HTML: [https://github.com/gruntjs/grunt-contrib-htmlmin](https://github.com/gruntjs/grunt-contrib-htmlmin)

示例: Javascript压缩

###grunt-contrib-uglify
测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-contrib-uglify
	|__src
	|	|__demo.js	
	|__Gruntfile.js
	|__package.json
	
```

安装grunt-contrib-uglify

```bash
npm install grunt-contrib-uglify --save-dev
```

测试代码

```javascript
module.exports = function(grunt) {
	//加载uglify模块
	grunt.loadNpmTasks('grunt-contrib-uglify');

	// Project configuration.
	grunt.initConfig({
		uglify: {
			files: [{
				src: 'src/demo.js',
				dest: 'dest/demo.min.js'
			}]
		}
	});
	// Define the default task
	grunt.registerTask('default', ['uglify']);
};
```

执行结果:

```
//结果显示自动创建文件dest/demo.min.js
>grunt
Running "uglify:files" (uglify) task
>> 1 file created.

Done, without errors.

```

##Concatenation(合并文件)
合并文件也可以减少网页加载时间,程序员开发时往往把js代码分成几个模块,但上线时合并文件能减少客户端的请求数

##grunt-contrib-concat(合并js文件)
测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-contrib-concat
	|__src
	|	|__src1.js
	|	|__src2.js
	|__Gruntfile.js
	|__package.json
	
```

安装grunt-contrib-concat

```bash
npm install grunt-contrib-concat --save-dev
```

测试代码

```javascript
module.exports = function(grunt) {
    //加载concat模块
    grunt.loadNpmTasks('grunt-contrib-concat');

    // Project configuration.
    grunt.initConfig({
        concat: {
            dist: {
                src: ['src/src1.js','src/src2.js'],
                dest: 'dest/concat.js'
            }
        }
    });
    // Define the default task
    grunt.registerTask('default', ['concat']);
};
```

执行结果:

```
//结果显示自动创建文件dest/concat.js
>grunt
Running "concat:dist" (concat) task
File dest/concat.js created.

```

##Deployment部署自动化
部署是一个重复而又枯燥的过程,每次上线项目时,都要ssh远程登录到服务器,找到正确的路径把文件拷贝进去然后重新启动,可能还有更复杂的过程,比如对当前版本的备份,而Grunt就有插件可以完成这样的自动化部署

下面介绍两种部署方式:FTP,SFTP

###FTP
测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-ftp-deploy
	|__build
	|	|__build1.js
	|	|__build2
	|		|___build3.js
	|__.ftppass
	|__Gruntfile.js
	|__package.json
	
```

安装grunt-ftp-deploy

```bash
npm install grunt-ftp-deploy --save-dev
```

测试代码

```javascript
//Gruntfile.js
module.exports = function(grunt) {
    //加载ftp模块
    grunt.loadNpmTasks('grunt-ftp-deploy');

    // Project configuration.
    grunt.initConfig({
        'ftp-deploy': {
            build: {
                auth: {
                    host: 'ip地址',
                    port: '端口号,
                    authKey: 'mypassword'
                },
                src: 'build',
                dest: '/home/trip/ftpDemo'
            }
        }
    });
    // Define the default task
    grunt.registerTask('default', ['ftp-deploy']);
};

//.ftppass
{
	"mypassword": {//名字和authKey相同
		"username": "你的用户名",
		"password": "你的密码"
	}
}
```

执行结果:

```
//结果显示自动创建文件夹和文件
>grunt
Running "ftp-deploy:build" (ftp-deploy) task
>> New remote folder created /home/trip/ftpDemo/
>> New remote folder created /home/trip/ftpDemo/build2
>> FTP upload done!

Done, without errors.

```

###SFTP
测试环境目录

```
|___my-project
	|__node_modules
	|	|__grunt
	|	|__grunt-ssh
	|__build
	|	|__build1.js
	|	|__build2
	|		|___build3.js
	|__.ftppass
	|__Gruntfile.js
	|__package.json
	
```

安装grunt-ssh

```bash
npm install grunt-ssh --save-dev
```

测试代码

```javascript
//Gruntfile.js
module.exports = function(grunt) {
    //加载sftp模块
    grunt.loadNpmTasks('grunt-ssh');

    grunt.initConfig({
    	 //读取secret中的内容
        secret : grunt.file.readJSON('secret.json'),
        sftp: {
            options: {
                host: '<%= secret.host %>',
                username: '<%= secret.username %>',
                password: '<%= secret.password %>',
                path: '服务器路径',
                showProgress: true,
                srcBasePath: '本地复制的文件家路径(build/)'
            },
            files: {
                src: "复制的文件(build/)"
            }
        }
    });
    // Define the default task
    grunt.registerTask('default', ['sftp']);
};

//secret.json
{
    "host" : "ip地址",
    "username" : "用户名",
    "password" : "密码"
}
```

执行结果:

```
//结果显示自动创建文件夹和文件
>grunt
Running "ftp-deploy:build" (ftp-deploy) task
>> New remote folder created /home/trip/ftpDemo/
>> New remote folder created /home/trip/ftpDemo/build2
>> FTP upload done!

Done, without errors.

```








