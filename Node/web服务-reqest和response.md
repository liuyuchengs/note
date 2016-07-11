+ nodejs的web服务-request
  + 使用http内置模块创建web服务
  + request对象和response对象挂载在处理函数中

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
        

        
        