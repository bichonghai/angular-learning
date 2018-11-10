# 面向对象设计
* 面向对象技术是现代软件开发中的重要技术之一。面向对象变成的好处毋庸置疑，现在的主流语言如Java、C++都是面向对象的。
现在的面向对象理论更多的是使用Java或C++进行描述，究其根源，在于这些语言都是传统的面向对象语言，
具有面向对象理论所指明的一切特性：类、封装、继承、多态等等。  
* 相比而言，一些动态语言如JavaSript就显得不那么面向对象——至少，在JavaScript中并没有类class这一关键字。
但是，在JavaScript中并不是没有类的概念。于是有人说，JavaScript是基于对象的语言，而不是面向对象的语言。

## 面向对象的语言具有三个特性：封装、继承和多态
### 来看看ES5如何实现
* 构造函数模式：【形式最贴近JAVA的模式】 
function Person (Name,Age,Job) {  
      this.name = Name;    
      this.age = Age;   
      this.job= Job;    
      this.sayName= function () {        
              alert(this.name)     
      }    
}    
var personOne=  new Person("Erric",26,"Engineer");  
var personTwo=  new Person("Lori",26,"teacher");  
console.log(personTwo.name);  //有人说，此相当于属性只能公有，没有私有概念，这个后面会说  
缺点： 
每个方法都要在每个实例上重新创建一遍  
personOne和personTwo中的sayName方法不是同一个方法，每个函数都是一个对象.  
* 	组合构造函数和原型模式【效果最贴近JAVA的模式】  
function Person(name,age,job){    
　　this.name=name;  
　　this.age=age;  
　　this.job=job;  
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
