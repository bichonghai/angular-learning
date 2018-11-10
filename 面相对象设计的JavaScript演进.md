# 面向对象设计
* 面向对象技术是现代软件开发中的重要技术之一。面向对象变成的好处毋庸置疑，现在的主流语言如Java、C++都是面向对象的。
现在的面向对象理论更多的是使用Java或C++进行描述，究其根源，在于这些语言都是传统的面向对象语言，
具有面向对象理论所指明的一切特性：类、封装、继承、多态等等。  
* 相比而言，一些动态语言如JavaSript就显得不那么面向对象——至少，在JavaScript中并没有类class这一关键字。

Javascript是一门解释型的语言，是基于对象的，并不是真正的面向对象的语言，对变量类型的应用也是宽松的，其实它同样可以模拟面向对象的功能。 

## 面向对象的语言具有三个特性：封装、继承和多态
### ES5 类【书籍中有7种左右模式，本质上3种技术混合】
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
 所谓多态就是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。  
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

