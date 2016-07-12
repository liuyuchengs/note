##### request和response
+ nodejs的web服务-request
  + 使用http内置模块创建web服务
  + request对象和response对象挂载在处理函数中
  + request对象包含所有的http请求信息

        var http = require("http");

        http.createServer((req,res)=>{
            res.writeHead(200,{"Content-Type":"text/plain"});
            res.end("hello node.js");
        }).listen(3000);
  + 解析request的method

        http.createServer((req,res)=>{
            var method =req.method;
            res.end(method);
        }).listen(3000);
  + 解析路径

        var url = require("url");

        var path = url.parse(req.url).path; //string
  + 解析查询字符串,如果查询字符串的key出现多次，那么它的值组合成一个数组

        var queryString =require("querystring");

        var query = queryString.parse(url.parse(req.url).query); //object

+ nodejs的web服务-response
  + statusCode/statusMessage：设置响应流的状态码/状态文本

        res.statusCode = 400; //badrequest
        res.statusMessage = "Not Found";
  + setHeader(key,value)：设置响应流请求头

        res.setHeader("Content-Type","text/json");
  + writeHead():响应流中写入状态码和请求头

        res.writeHead(400,{"Content-Type":"text/plain"});
  + write(chunk,[encoding],[callback])：响应流中写入信息，可以是string或buffer

        res.write("hello wolrd","utf8",()=>{
            console.log("response success");
        })
  + end([data],[encoding],[callback])：结束响应流

        res.end("server is over",()=>{
            console.log("server is over");
        });

##### url 
+ 解析url
  + 加载url模块后，使用parse()解析url,返回一个解析对象

            var url = require("url");
            var result = url.parse("http://www.baidu.com/index.html?info=search");
            //解析成
            Url {
                protocol: 'http:',
                slashes: true,
                auth: null,
                host: 'www.baidu.com',
                port: null,
                hostname: 'www.baidu.com',
                hash: null,
                search: '?info=search',
                query: 'info=search',
                pathname: '/index.html',
                path: '/index.html?info=search',
                href: 'http://www.baidu.com/index.html?info=search' 
            }
  + 设置第二个参数为true，生成的query将不再是字符串，而是包含查询信息的对象

            var result1 = url.parse("index.html?info=search",true);
            //解析成
            Url {
                protocol: null,
                slashes: null,
                auth: null,
                host: null,
                port: null,
                hostname: null,
                hash: null,
                search: '?info=search',
                query: { info: 'search' },
                pathname: 'index.html',
                path: 'index.html?info=search',
                href: 'index.html?info=search' 
            }
+ 生成url
  + 使用format()将一个url对象生成url字符串

            var result2 = url.format({
                protocol:"http",
                hostname:"www.baidu.com",
                pathname:"index.html",
                search:"info=liuyucheng"
            
            })
            //生成如下url
            http://www.baidu.com/index.html?info=liuyucheng
+ 拼接url
  + 使用resolve()拼接成url

            var result3 = url.resolve("http://www.baidu.com/fo/fn","../../index.html");
            //拼接成
            http://www.baidu.com/index.html

##### Query String
+ 将查询字符串转换成对象

            var querys = require("querystring");
            var result4 = querys.parse("first=jack&second=tom&second=jases&three");
            { first: 'jack', second: [ 'tom', 'jases' ], three: '' }
+ 将对象转换成查询字符串

            var result5 = querys.stringify({ first: 'jack', second: [ 'tom', 'jases' ], three: '' });
            “first=jack&second=tom&second=jases&three=”  
        