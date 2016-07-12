+ 关于cookie
  + 缓存在客户端的键值对数据，仅限指定域名内的页面可见
  + 符合条件的http访问均会将该cookie发送到服务器端
  + key=value：指定键值对
  + Domain：指定域名
  + path：指定路径
  + Max-Age/Expires：指定cookie过期日期
  + HttpOnly：客户端是否可以通过脚本修改

        name=value; Path=/; Expires=Sun, 23-Apr-23 09:01:35 GMT; Domain=.domain.com;
+ 操作cookie
  + 服务端生成cookie字符串

        //生成cookies
        var serizleCookie =  (key,value,opt)=>{
            var repairs = [key+"="+value];
            opt = opt || {};
            if(opt.maxAge){repairs.push("Max-Age="+opt.maxAge)};
            if(opt.path){repairs.push("Path="+opt.path)};
            if(opt.httpOnly){repairs.push("HttpOnly="+opt.httpOnly)};
            return repairs.join(";");
        }
  + 将cookie字符串添加到响应头的Set-Cookie中

        // 添加单条cookie
        res.setHeader("Set-Cookie",serizleCookie("isVis","1",{path:"/test"}));
        // 添加多条cookie
        res.setHeader("Set-Cookie",[serizleCookie("isVis","1",{path:"/test"}),serizleCookie("second","2")]);
  + 解析客户端返回的cookie

        //解析cookies
        var parseCookie = (cookie)=>{
            var cookies = {};
            if(!cookie){
                return cookies;
            }
            var list = cookie.split(";");
            for(var i=0;i<list.length;i++){
                var repair = list[i].split("=");
                cookies[repair[0].trim()] = repair[1];
            }
            return cookies;
        }
