+ let
  + let声明的变量只在当前的"{}"内有效

            {
                var b =1;
                let a =1;
            }
            console.log(b); //1
            console.log(a); //Reference Error
  + let声明的变量不会有变量提升

            {
                a = 4;
                let a; //Reference Error
            }
  + 暂时性死区:let和const声明的变量会绑定到该区域，不受外部变量的影响

            var a = 4;
            {
                a = 10;  //Reference Error
                let a;
            }
  + 不允许重复声明

            {
                var a =3;
                let a =1; //Syntax Error
            }
+ const
  + 声明常量

            const a = 1;
            a =3; //Syntax Error
  + const常量和let变量一样：只在当前的{}内有效，不会有变量提升,暂时性死区，不允许重复声明
  + 复杂对象的可变性
 
            const dog= {
                name:"tom"
            }
            dog.name = "jack";
            console.log(dog.name); //jack
+ 块级作用域
  + 使用let和const声明变量可实现js块级作用域,外部作用域无法访问内部块作用域

            for(var i=0;i<10;i++){}
            i; //10;
            for(let j=0;j<10;j++){}
            j; //ReferenceError
  + 内部块级作用域能访问和覆盖外部作用域变量
  
            function fn(){
                var a = 4;
                if(true){
                    let a = 10;
                    console.log(a); //10
                }
            }
