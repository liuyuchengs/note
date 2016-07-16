+ 关于Buffer
  + Buffer是全局模块，可直接使用
 
        var buffer = new Buffer("hello world","utf-8")
  + Buffer对象内部是一个元素为两位16进制的数组

        buffer.length();
        buffer[0] = "6c";
        var value = buffer[2];
  + 每个元素的大小为0-255，超出部分则逐次累减256，不足部分则累加256

        buffer[0]=-30; //输出226
+ Buffer转换
  + string-->Buffer:通过构造函数转换的buffer，只能存放一种编码方式，write()可存放不同编码

        //默认使用utf-8编码
        var buffer = new Buffer("hello world","utf-8");
        var buffer1 = new Buffer();
        buffer1.write("hello world",3,10,"utf-8");
  + Buffer-->string：可实现全部转换或者局部转换

        //默认使用utf-8
        buffer.toString([encoding],[start],[end]);
+ Buffer的拼接
  + Buffer在传输过程中是分段的，对于非unicode字符集，会造成乱码现象

        var fs = require('fs');
        var rs = fs.createReadStream('test.md');
        var data = '';
        rs.on("data", function (chunk){
            //等价于data = data.toString()+chunk+toString();
            data += chunk;
        });
  + 正确的拼接：将分段的Buffer缓存到一个数组内，再进行转换
 
        var fs =require("fs");
        var rs = fs.createReadStream("test.txt");
        var result = [];
        rs.on("data",function(data){
            result.push(data);
        });
        rs.on("end",function(){
            var buf = Buffer.concat(result);
            console.log(buf.toString());
        })
+ 静态方法
  + isBuffer():判断是否是buffer

        Buffer.isBuffer(data)
  + isEncoding(encoding)：判断所使用的编码

        console.log(Buffer.isEncoding("utf8"));
+ 