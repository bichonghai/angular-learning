# 面向对象设计
* 面向对象技术是现代软件开发中的重要技术之一。面向对象变成的好处毋庸置疑，现在的主流语言如Java、C++都是面向对象的。
现在的面向对象理论更多的是使用Java或C++进行描述，究其根源，在于这些语言都是传统的面向对象语言，
具有面向对象理论所指明的一切特性：类、封装、继承、多态等等。  
* 相比而言，一些动态语言如JavaSript就显得不那么面向对象——至少，在JavaScript中并没有类class这一关键字。

Javascript是一门解释型的语言，是基于对象的，并不是真正的面向对象的语言，对变量类型的应用也是宽松的，其实它同样可以模拟面向对象的功能。 

## 面向对象的语言具有三个特性：封装、继承和多态
### ES5 类【书籍中有7种左右模式，本质上3种技术混合】  
2009 年 12 月，ECMAScript 5.0 版正式发布。  
* 构造函数模式：【形式最贴近JAVA的模式】 
function Person (Name,Age,Job) {  
      this.name = Name;    
      this.age = Age;   
      this.job= Job;  
      address="私有";//属性的私有实现    
      this.sayName= function () {        
              alert(this.name)     
      }    
}    
var personOne=  new Person("Erric",26,"Engineer");  
var personTwo=  new Person("Lori",26,"teacher");  
console.log(personTwo.name); //公有属性可以直接访问    
缺点： 
每个方法都要在每个实例上重新创建一遍  
personOne和personTwo中的sayName方法不是同一个方法，每个函数都是一个对象.  
* 	组合构造函数和原型模式【效果最贴近JAVA的模式】  
function Person(name,age,job){    
　　this.name=name;  
　　this.age=age;  
　　this.job=job;  
    address="私有";//属性的私有实现    
　　this.friends=["Machiel","Dophe"];  
};  
Person.prototype={  
　　constructor:"Person",  
　　sayName:function(){  
　　　　alert(this.name)  
　　}  
};  
var person=new Person("Niche",12,"Software")  
console.log(person.friends);  
person.sayName();   
在这个例子中，实例属性都是在构造函数中定义的，而由所有实例共享的属性 constructor 和方法 sayName()则是在原型中定义的。  
person1.friends（向其中添加一个新字符串），并不会影响到 person2.friends，因为它们分别引用了不同的数组。  
这种构造函数与原型混成的模式，是目前在 ECMAScript中使用最广泛、认同度最高的一种创建自定义类型的方法。  
### ES5 继承 
* 通过原型链实现  
function Super(){     
　　this.property = 'Super Property'       
}       
Super.prototype.getProperty = function(){    
　　return this.property   
}  
// 子类  
function Sub(){    
　　this.property = 'Sub Property'  
}    
Sub.prototype = new Super()    
Sub.prototype.constructor = Sub   
   
### ES5 多态  
* 所谓多态就是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。  
* 参考例子  
var makeSound = function(animal) { // 把不变的部分隔离出来
    animal.sound();  
};  
 
把可变的部分各自封装起来，每个类型的动物各自封装  
var Duck = function() {};  
Duck.prototype.sound = function() {  
      console.log("嘎嘎嘎");  
};
var Chicken = function() {};  
Chicken.prototype.sound = function() {  
      console.log("咯咯咯");  
};  
makeSound( new Duck() ); // 嘎嘎嘎  
makeSound( new Chicken() ); // 咯咯咯   
javascript是弱类型的语言，因为根本就不需要像java那样引入接口、抽象类，因为只要参数的结构类似，就可以模拟多态。【接口和类就是结构一样】    

## ES6 【明确了类、继承，定义了let、const等局部变量，但没有定义私有、公有、保护、变量的类型等特性】
参考网址： http://es6.ruanyifeng.com/#docs/intro  
2015 年 6 月，ECMAScript 6 正式通过，成为国际标准。从 2000 年算起，这时已经过去了 15 年。  
### ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。

基本上，ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用 ES6 的class改写，就是下面这样。

//定义类
class Point {  
  constructor(x, y) {  
      this.x = x; 
       this.y = y;  
  }  

  toString() {  
       return '(' + this.x + ', ' + this.y + ')';  
  }  
}  
### Class 可以通过extends关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

class Point {  
}  

class ColorPoint extends Point {  
}  
上面代码定义了一个ColorPoint类，该类通过extends关键字，继承了Point类的所有属性和方法。但是由于没有部署任何代码，所以这两个类完全一样，等于复制了一个Point类。下面，我们在ColorPoint内部加上代码。  

class ColorPoint extends Point {  
  constructor(x, y, color) {  
      super(x, y); // 调用父类的constructor(x, y)  
      this.color = color;  
  }  

  toString() {  
      return this.color + ' ' + super.toString(); // 调用父类的toString()
  }  
}  
### 模块（module）体系 
1.历史上，JavaScript 一直没有模块（module）体系，无法将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。其他语言都有这项功能，比如 Ruby 的require、Python 的import，甚至就连 CSS 都有@import，但是 JavaScript 任何这方面的支持都没有，这对开发大型的、复杂的项目形成了巨大障碍。  
在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。  

2.ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。

3.ES6的模块案例  
export { es6 as default } from './someModule'; //模块导入  
// 等同于
import { es6 } from './someModule';  
export default es6;                            //模块导出           


## TypeScript 【定义了属性的类型推断、公共，私有与受保护的修饰符、泛型、接口等，一句话越来越像 java】
TypeSciprt是一门脚本语言，它算是Javascript的增强版，它扩展Javascript的类库，增加了面向对象特性。当然它最大的特点是兼容Javascript，它可以将自己的代码编译成Javascript代码。  
为什么会有 TypeScript?     
JavaScript 只是一个脚本语言，并非设计用于开发大型 Web 应用，JavaScript 没有提供类和模块的概念，而 TypeScript 扩展了 JavaScript 实现了这些特性。TypeScript 主要特点包括：  

TypeScript 是微软推出的开源语言，使用 Apache 授权协议  
TypeScript 是 JavaScript 的超集.   
TypeScript 增加了可选类型、类和模块  
TypeScript 可编译成可读的、标准的 JavaScript  
TypeScript 支持开发大规模 JavaScript 应用  
TypeScript 设计用于开发大型应用，并保证编译后的 JavaScript 代码兼容性  
TypeScript 扩展了 JavaScript 的语法，因此已有的 JavaScript 代码可直接与 TypeScript 一起运行无需更改  
TypeScript 文件扩展名是 ts，而 TypeScript 编译器会编译成 js 文件  
TypeScript 语法与 JScript .NET 相同  
TypeScript 易学易于理解  
语法特性  
类 Classes  
接口 Interfaces  
模块 Modules   
类型注解 Type annotations  
编译时类型检查 Compile time type checking   
Arrow 函数 (类似 C# 的 Lambda 表达式)  

* 定义了基础类型【布尔值 、字符串、枚举、数字、数组、枚举、void  Object
   https://www.tslang.cn/docs/handbook/basic-types.html  
* 定义了 公共，私有与受保护的修饰符，更加完善了类的定义 。
  https://www.tslang.cn/docs/handbook/classes.html  
* 定义了接口
  https://www.tslang.cn/docs/handbook/interfaces.html  
* 定义了泛型
  https://www.tslang.cn/docs/handbook/generics.html  

### 重点
1.ES5、ES6 、TypeScript 的过程中，语言越来越像面相对象的语言。  
2.TypeScript的特性是编译期检查，而不是运行时检查。  
这个就不难理解，为了TypeScript的程序为啥经过编译后，可以运行在ES5和ES6可以运行的平台上。  
因为那些语法特性，比如 private、public、基本类型，都是编译时进行检查，就类似于 java---编译为class一样。  
3.TypeScript是ES6、ES5的子集，也就意味着支持他们的所有语法，这样不是意味着大家还可能继续使用不推荐的语法。   
 的确如此    
4.TSLint 代码规范检查  
  在编写 JavaScript 代码时，我们可以通过 ESLint 来进行代码规范检查，编写 TypeScript 代码时也可以使用 TSLint，两者在配置上也有些相似。对于初学者来说，使用 TSLint 可以知道哪些程序的写法是不被推荐的，从而养成更好的 TypeScript 代码风格。  

## TypeScript、ES6 的编译
React项目一般使用Babel进行编译，Angular【不是AngularJS】项目则会使用TSC进行编译。  
TypeScript、ES6 都是无法直接在大部分浏览器上执行的，必须经过编译转化才能直接运行。  
TypeScript的编译使用tsc编译器，tsc编译器可以指定最终编译的js的版本。 
Babel 是一个 JavaScript 编译器，Babel 通过语法变换器支持最新版本的 JavaScript。  
Babel是一个广泛使用的转码器，可以将ES6代码转为ES5代码，从而在现有环境执行。  

### 几句话概述
1.TypeScript 最接近面向对象的语言实现   
2.TypeScript 在支持面相对象特性时，是编译期检查，通过tsc进行编译，具备完整的兼容ES5和ES6的转化。   
3.TypeScript 开发友好，那些编译期的语法检查，开发工具都直接提醒，避免开发人员的不友好的编码。    


