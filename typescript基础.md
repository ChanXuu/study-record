##  TypeScript数据类型

​	typescript中为了代码更规范,便于维护,增加了类型校验,写ts代码要指定类型

1. **数字类型(Number)**

   ```typescript
   //es5写法 
   let aa = 666
   
   //ts写法
   let aa:number = 666
   ```

   

2. **布尔类型(booleam)**

   ```typescript
   //ts写法
   let aa:boolean = true
   ```

   

3. **字符串类型(string)**

   ```typescript
   //ts写法
   let aa:string = 'cx'
   ```

   

4. **数组类型(array)**

   ```typescript
   //ts写法
   
   //第一种:
   let aa1:number[] = [1,2,3] //number类型数组
   //第二种
   let aa2:Array<number> = [1,2,3]
   //第三种
   let aa3:any[] = ['1',2,true]
   ```

   

5. **元组类型(tuple)**

   ```typescript
   //可以给数组中位置指定数据类型
   let arr:[number,string] =[666,'cx] 
   ```

   

6. **枚举类型(enum)**

   ```typescript
   //用于 用自然语言中含义清楚的单词来表示它的每一个值,这种方法叫做枚举
   enum Flag {success = 1,error = 0}
   let s:Flag = Flag.success // 输出1
   
   enum Color {blue,red,black}
   let s:Color = Color.blue // 输出0,如果标识符没有赋值,则输出下标
   
   enum Color {blue,red=5,black}
   let s:Color = Color.black // 输出6,因为下标是上一个的值加一
   ```

   

7. **任意类型(any)**

   ```typescript
    let aa:any = 666
    aa = 'cx' //不报错
    aa = true //不报错
   ```

   

8. **null 和 undefined**

   ```typescript
   //null 和 undefined 其他(never)类型的子类型
   
   let num:number
   console.log(num) //输出 undefined   报错
   
   let num1:undefined;
   console.log(num1) //输出undefined  正确
   
   //定义没有赋值就是undefined
   var num2:number|undefined
   console.log(num2)  //不报错
   
   var num3:number|undefined | null
   
   
   ```

   

9. **void类型**

   ```typescript
   //空类型,一般用于函数没返回值
   
   function getData():viod{
       console.log('666)
   }
   getData();
   ```

   

10. **never类型**

    ```typescript
    //其他类型 ,代表从不会出现的值
    //这意味着声明never的变量只能被never类型所赋值
    
    let a:never;
    a=123 //错误写法
    
    a=(()=>{
        throw new Error('错误')
    })()
    ```

##  TypeScript函数

1. **函数的定义**

   ```typescript
   //es5
   function aa(){}
   let aa1=function(){}
   
   //ts
   function aa2():string{return '123'}
   let aa3=function():number{return 123}
   
   //1.ts中定义方法传参
   function aa4(name:string,age:number):string{
       retrun `${name}----${age}`
   }
   aa4('cx',24)
   
   let aa5 = function(name:string,age:number):string{
        retrun `${name}----${age}`
   }
   aa5('cx',24)
   
   //没有返回值
   function aa6():void{}
   
   ```



2. **方法的可选参数**

   ```typescript
   
   //es5里面方法的实参和形参可以不一样,但是ts中必须一样,如果不一样就需要配置可选参数
   //注意:可选参数必须配置到参数的最后
   function aa7(c):string{
       if(age){
           return `${name}----${age}`
       }else{
           return `${name}----年龄保密`
       }
   }
   aa7('cx',24) // cx --- 24
   aa7('cx') //cx ---年来保密
   ```

3. **默认参数**

   ```typescript
   //3.默认参数
   //es5里不能设置默认参数,es6和ts都可以设置默认参数
   function aa8(name:string,age:number=20):string{
       if(age){
           return `${name}----${age}`
       }else{
           return `${name}----年龄保密`
       }
   }
   aa8('cx',24) // cx --- 24
   aa8('cx') //cx --- 20
   ```

   

4. **剩余参数**

   ```typescript
   //4.剩余参数
   function aa9(...result:number):number{
       let sum = 0
       for(let i = 0;i< result.length;i++){
           sum+=result[i]
       }
   }
   aa9(1,2,3)//6
   
   function aa10(x,...result:number):number{
       let sum = 0
       for(let i = 0;i< result.length;i++){
           sum+=result[i]
       }
   }
   aa10(1,2,3)//5
   
   ```

   

5. **函数的重载**

   ```typescript
   //5.函数的重载
   //java中方法的重载:重载指的是两个或者两个以上同名函数,但他们的参数不一样,这时候会出现函数的重载的情况
   
   //ts中的重载:通过为同一个函数提供多个函数类型定义来实现多种功能的目的
   //ts为了兼容es5和es6重载的写法和java中有区别
   
   //es5中出现同名方法,下面的方法会替换上面的方法
   
   //ts中的重载
   //参数不一样
   function aa11(name:string):string{}
   function aa11(age:number):number{}
   
   function aa11(str:any):any{
       if(typeof str ==='string'){
           retrun '字符串'+str
       }else{
           return '数字'+str
       }
   }
   //参数一样
   function aa12(name:string):string
   function aa12(name:string,age:number):string
   function aa12(name:string,age:any):any{
       if(age){
           retrun '我叫'+ name + '我的年龄是' + age
       }else{
           retrun '我叫'+ name
       }
   }
   
   aa12('cx') //正确
   aa12(123) //错误
   aa12('cx',24) //正确
   
   ```

   

6. **箭头函数 **

   ```typescript
   //6.箭头函数 es6
    //this指向问题   箭头函数里面的this指向上下文
   
   ```



## TypeScript中的类

1. **es5中**

``` typescript
//es5 定义类
//1.最简单的类
function aa(){
    this.name = 'cx
    this.age = 24
}

var a = new aa();
a.name  // cx

//2.构造函数和原型链里面增加方法
function aa1(){
    this.name = 'cx
    this.age = 24
    this.bb = function(){ //实例方法
        console.log('123')
    }
}
var b = new aa1();
b.bb() // 123


//原型链( 原型链上面的属性会被多个实例共享)
aa2.prototype.sex = '男';
aa2.prototype.work = function(){
    console.log(456)
}

var c = new aa2()
c.sex //男
c.work  //456

//静态方法
aa2.run = function(){
    console.log(123)
}

aa2.run() //123


//3.es5里面的继承(原型链 + 对象冒充的组合继承模式)

//对象冒充
function aa3(){
    aa2.call(this); //对象冒充实现继承
}

var w = new aa3();
w.work //456  对象冒充可以继承构造函数里面的属性和方法,但是没法继承原型链上的属性和方法

function aa4(){}
aa4.prototype = new aa2(); //原型链实现继承,可以继承构造函数里面的属性和方法,也可以继承原型链上的属性和方法
var x = new aa4()
x.run()//123
x.work()//456

//原型链实现继承的问题
function aa5(name,age){
    this.name = name
    this.age = age 
    this.run = funciton(){
        console.log('run')
    }
}

aa5.prototype.sex = '男'
aa5.prototype.work = function(){
    console.log('work')
}

var p = new aa5('cx',24)
p.run() // run

function web(name,age){
    
}
web.prototype = new aa5()
var w = new web('cx',20) //原型链实例化子类的时候没法给父类传参
w.run(); //报错

//组合继承
function web(name,age){
	aa5.call(this,name,age) //对象冒充继承  实例化类可以给父类传参
}
web.prototype = new aa5()

var w = new web('cx',20)
w.run() //run
w.work() //work
```

2. **ts中定义类**

   ```typescript
   //例子1
   class per{
       name:string;  //属性 前面省略了public关键词
       constructor(n:string){//构造函数  实例化的时候触发的方法
           this.name = n;
       }
       run():void{
           console.log(this.name)
       }
   }
   var p = new per('cx')
   p.run()
   
   //例子2
   class per {
       name: string;  //属性 前面省略了public关键词
       constructor(name: string) {//构造函数  实例化的时候触发的方法
           this.name = name;
       }
       getName():string{
           return this.name
       }
       setName(name:string):void{
           this.name = name
       }
   }
   
   var p = new per('cx')
   p.getName()
   console.log(p.getName()) //cx
   p.setName('lw')
   console.log(p.getName()) //lw
   
   
   ```

3. **ts中实现继承  extends , super**

   ```typescript
   //例子1
   class per{
       name:string;
       constructor(name:string){
           this.name = name
       }
       run():string{
           return `${this.name}在运动`
       }
   }
   
   class web extends per{
       constructor(name:string){
           super(name) //初始化父类的构造函数
       }
   }
   
   let w = new web('lw')
   console.log(w.run()) //lw在运动
   
   //例子2  扩展子类方法
   class per{
       name:string;
       constructor(name:string){
           this.name = name
       }
       run():string{
           return `${this.name}在运动`
       }
   }
   
   class web extends per{
       constructor(name:string){
           super(name) //初始化父类的构造函数
       }
       work():void{
           console.log(`${this.name}在工作`)
       }
   }
   
   let w = new web('lw')
   console.log(w.run()) //lw在运动
   w.work() //lw在工作
   
   //例子3 父类子类有同名方法,会执行子类的方法
   
   class per{
       name:string;
       constructor(name:string){
           this.name = name
       }
       run():string{
           return `${this.name}在运动`
       }
   }
   
   class web extends per{
       constructor(name:string){
           super(name) //初始化父类的构造函数
       }
       run():string{
           return `${this.name}在工作-子类`
       }
   
   }
   
   let w = new web('lw')
   console.log(w.run()) //lw在工作-子类
   
   ```

4. **类里面的修饰符**

   1. public 

      ```typescript
      //公有类型  在类里面.子类.类外面都可以访问(默认)
      class per{
          public name:string;
          constructor(name:string){
              this.name = name
          }
          run():string{
              return `${this.name}在运动`
          }
      }
      class web extends per{
          constructor(name:string){
              super(name) //初始化父类的构造函数
          }
          work():void{
              console.log(`${this.name}在工作`)
          }
      }
      
      let w = new web('lw')
      console.log(w.run()) //lw在工作
      ```

      

   2. protected

     ```typescript
     //保护类型 在类里面.子类里面可以访问    在类外面没法访问
     class per{
         protected name:string;
         constructor(name:string){
             this.name = name
         }
         run():string{
             return `${this.name}在运动`
         }
     }
     class web extends per{
         constructor(name:string){
             super(name) //初始化父类的构造函数
         }
         work():void{
             console.log(`${this.name}在工作`)
         }
     }
     let w = new web('cx')
     
     w.work() //cx在工作
     w.name //没输出,提示是受保护的
     ```

     

   3. private

     ```typescript
     //私有类型  在类里面可以访问,子类和类外部都没法访问
     class per {
         private name: string;
         constructor(name: string) {
             this.name = name
         }
         run(): string {
             return `${this.name}在运动`
         }
     }
     let x = new per('cx')
     x.run() //cx在运动
     
     class web extends per {
         constructor(name: string) {
             super(name) //初始化父类的构造函数
         }
         work(): void {
             console.log(`${this.name}在工作`) //这里会提示是私有属性
         }
     }
     let w = new web('cx')
     w.run() //cx在工作
     w.name //这里会提示是私有属性
     ```

     
   
5. 静态属性 静态方法

   ```typescript
   class per {
       name:string
       static age:number = 24  //静态属性
       constructor(name:string){
           this.name = name
       }
   
       run(){//实例方法
           console.log(`${this.name}在运动`)
       }
   
       static print(){//静态方法,里面没法直接调用类里面的属性
           console.log('这是ts静态方法' + `${this.age}`)
       }
   }
   
   //非静态方法不能直接用,要实例化
   let p = new per('cx')
   console.log(p.name)
   p.run()
   
   //静态方法可以直接调用
   per.print() 
   console.log(per.age)
   ```

   

6. 抽象类 继承多态

   ```typescript
   //多态:父类定义一个方法不去实现,让继承它的子类去实现,每个子类有不同的表现
   //多态属于继承
    class animal {
       name:string
       constructor(name:string){
           this.name = name;
       }
       eat(){ //具体吃什么,不知道 ,让继承它的子类去实现,每一个子类的表现不一样
           console.log('吃的方法')
       }
   }
   
   class dog extends animal {
       constructor(name:string){
           super(name)
       }
       eat():string{
           return `${this.name}吃骨头`
       }
   }
   
   class cat extends animal {
       constructor(name: string) {
           super(name)
       }
       eat(): string {
           return `${this.name}吃鱼`
       }
   }
   ```

7. 抽象方法

   ```typescript
   //ts中的抽象类:它是提供其他类继承的基类,不能直接被实例化
   //用abstract关键字定义抽象类方法,抽象类中的抽象方法不包含具体实现并且必须在派生类中实现
   //abstract 抽象方法只能放在抽象类里面
   //抽象类用来定义标准的
   //例子: 用来定义标准:animal 这个类要求它的子类必须包含eat方法
   
    abstract class animal {
       name: string
       constructor(name: string) {
           this.name = name;
       }
       abstract eat():any;
       run(){
           console.log('其他方法可以不实现')
       }
   }
   
   //var a = new animal() //错误,无法创建抽象类的实例。
   
   class dog extends animal { 
       //抽象类的子类必须实现抽象类里面的抽象方法
       constructor(name: string) {
           super(name)
       }
       eat(): string {
           return `${this.name}吃骨头`
       }
   }
   
   var d = new dog('地豆')
   console.log(d.eat()) //地豆吃骨头
   
   
   ```



##  TypeScript 接口

```typescript
/* 接口的作用:在面向对象的编程,接口是一种规范的定义,它定义了行为和动作的规范,在程序设计里面,接口起到了一种限制和规范的作用.接口定义了某一批类所需要遵循的规范,接口不关心这些类的内部状态数据,也不关心这些类里方法的实现细节,它只规定这批类里面必须提供某些方法,提供这些方法的类就可以满足实际需要.ts中的接口类似于java,同时还增加了更灵活的接口类型,包括属性.函数.可索引和类等

定义标准
 */
```

1. **属性类接口**

   ```typescript
   //对json的约束
   //对批量方法传入参数进行约束
   
   interface FullName{
       firstName:string; //注意分号结束
       secondName:string;
       age:number;
   }
   
   function printt(name: FullName) {
       //必须传入对象 firstName secondName
       console.log(`${name.firstName}--${name.secondName}`)
   } 
   
   function printtInfo(name: FullName) {
       //必须传入对象 firstName secondName
       console.log(`${name.firstName}--${name.secondName}--${name.age}`)
   } 
   
   //print('111') //错误写法
   
   var obj = {//传入的参数必须包含firstName和secondName
       firstName:'c',
       secondName:'x',
       age:20
   }
   
   printt(obj) // c--x
   printtInfo(obj) //c--x--20
   
   //接口:可选属性
   interface FullName1{
       firstName?:string; //注意分号结束
       secondName?:string;
       age:?number;
   }
   ```

   

2. **函数类型接口**

   ```typescript
   //函数类型接口 
   //对方法传入的参数,以及返回值进行约束 批量约束
   
   //例子:加密的函数类型接口
   interface encrypt {
       (key:string,value:string):string;
   }
   
   var md5: encrypt = function (key:string,value:string):string{
       return key + value
   }
   
   console.log(md5('cx','blw')) //cxblw
   ```

   

3. **可索引接口**

   ```typescript
   
   //数组.对象的约束  (不常用)
   
   
   //可索引接口 数组的约束
   interface userArr {
       [index:number]:string
   }
   
   //var arr:userArr = [123,456]  //错误写法
   var arr:userArr = ['aaa','bbb'] //正确
   
   //可索引接口 对象的约束
   interface userArr1 {
       [index:string]:string
   }
   
   var arr1: userArr1 = {name:'cx'}
   ```

   

4. **类类型接口**

   ```typescript
   //类类型接口 ：对类的约束 和  抽象类有点相似
   
   interface animal{
       name:string;
       eat(str:string):void;
   }
   //implements 表示实现
   class dog implements animal{
       name:string
       constructor(name:string){
           this.name = name
       }
       eat(){
           console.log(this.name +'吃骨头')
       }
   }
   var d = new dog('狗')
   d.eat() //狗吃骨头
   ```

   

5. **接口扩展**

   ```typescript
   //接口可以继承接口
   interface animal{
       eat():void;
   }
   
   //接口的继承
   interface person extends animal{
           word():void;
   }
   
   class progammer {
       name:string
       constructor(name:string){
           this.name = name
       }
       coding(code:string){
           console.log(this.name +'写'+ code)
       }
   }
   
   //实现
   /* class web implements person{
       name:string
       constructor(name:string){
           this.name = name
       }
       eat(){
           console.log(this.name+'喜欢吃')
       }
       word(){
           console.log(this.name+'写代码')
       }
   } */
   
   //继承加实现
   class web extends progammer implements person{
       constructor(name:string){
           super(name)
       }
       eat() {
           console.log(this.name + '喜欢吃')
       }
       word() {
           console.log(this.name + '写代码')
       }
   }
   
   
   var w = new web('cx')
   w.eat() //cx喜欢吃
   w.word() //cx写代码
   w.coding('js') //cx写js
   ```

     



