+ http服务
  + nodejs的http服务由ServerRequest和ServerResponse对象组合
  + createServer([listen])：创建http服务，listen函数响应request事件,返回一个http.Server对象

        var http = require("http");

        const server = http.createServer((req,res)=>{
          //do something
        })
+ http.server
  + listen(port,[callback])：监听端口

        server..listen(3000);
+ http.ClientRequest
  + http.request(options,[callback])：创建ClientRequest对象

        var postData = queryString.stringify({
            'type':'home_banner'
        })

        var options = {
            hostname:"www.uokang.com",
            path:"/wx/banner/query",
            method:"POST",
            headers:{
                'Content-Type':'application/x-www-form-urlencoded',
                'Content-Length': postData.length,
            }
        }
        var clientRequest = http.request(options,(clientRes)=>{
          var chunks = [];
          console.log("status:"+clientRes.statusCode);
          clientRes.on('data',(chunk)=>{
              chunks.push(chunk);
          })
          clientRes.on('end',()=>{
              var result = null;
              for(var i=0;i<chunks.length;i++){
                  result += chunks[i];
              }
              console.log(result);
          })
        })
        clientRequest.write(postData);
        clientRequest.end();