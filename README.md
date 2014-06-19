#面向对象编程：
***
**一、概念：**

> 面向对象编程（Object Oriented Programming, OOP, 面向对象程序设计）是一种**计算机编程架构**，OOP的一条基本原则是*计算机程序是由单个能够起到子程序作用的单元或对象组合而成*，OOP达到了软件工程的三个目标：**重用性、灵活性和扩展性**。为了实现整体运算，每个对象都能够接收信息、处理数据和向其它对象发送信息。首先，面向对象符合人类看待事物的一般规律。其次，采用面向对象方法可以使系统各部分各司其职、各尽所能。为编程人员敞开了一扇大门，使其编程的代码更简洁、更易于维护，并且具有更强的可重用性。--百度百科  

**二、javascript中的面向对象：**  
我们可以把对象想象成现实世界中的某一个具体的事物，比如一部手机，就是一个对象，它有长、宽、高、颜
色、重量，这叫对象的属性，手机有打电话、发短信等功能，这些功能叫对象的方法。js中的对象是由系列名值对组成的，在js中，一切都是对象，如：字符串，数值，数组，函数等，但这里主要是指自定义对象。  
**1.创建对象：**
要写面向对象的程序，得先创建一个对象，在js中创建对象有两种方法：对象字面量和`Object`构造函数,如下：

		var person={};//字面量表示法,推荐
		  //或者
		var person=new Object();//构造函数法

**2.添加属性与方法：**有了对象，就可以为对象添加属性与方法（*方法其实与一般函数无异，当一个函数属于一个对象时，就叫对象的方法*），如下：

		var person={
			   name:"William",//添加一个name属性
			   sayName:function(){//添加一个sayName的方法
			       alert(this.name);
			   }
			};
		
		//还可以用以下两种方式添加属性与方法

	  	person.name="William";
	  	person.sayName=function(){
	      	alert(this.name);
	  	}

		person["name"]="William";
		person["sayName"]=function(){
		   alert(this.Name);
		}
定义好了对象的属性与方法之后，我们就可以读取对象的属性，调用对象的方法,如下：
		
		var myName=person.name;//读取对象的属性
		person.sayName();//调用对象的方法。输出William


  

 **3.存在的问题：**  
上面的概念里提到，面向对象编程要实现软件工程的三个目标：**重用性、灵活性和扩展性** ,那我们看上面的方式能不能实现这个目标。  

		//如果我有另一个对象person2，需要从person对象方继承sayName方法，可以这样做
		var person2=person;//对象的继承
		//因为person2名字不一样，所以我需要改变person2的name属性
		person2.name='Jack';
		//又因为另一个对象还具有别的功能（方法）：唱歌，所以需要扩展person2的方法
		person2.sing=function(){
			alert('I am singing');
		}
		//现在我们来调用person2的方法
		person2.sayName()//输出Jack，没什么问题。

		//再调一下person的方法
		person.sayName();//输出Jack
		person.sing();//输出I am singing


sing本来是person2扩展的方法，但现在person也有了此方法。也就是说，我们改变子对象的属性和方法时，父对象也受到了影响。这是什么原因造成的呢？那是因为，在js中，只有基本类型在赋值给另外的变量时，才会将自身复制一份，而对象，函数，数组等引用类型，在赋值给其它变量时，并不会复制自身，而只是将对象在内存中的地址给了变量。也就是说，person与person2其实指向的是内存中的同一个对象。这也就不难理解，为什么我们改变person2的属性与方法时，person也会跟着改变了。如果我们有多个类似的对象，由于不能继承，我们就需要定义多个对象。
		
		var a=5;
		var b=a;
		b=10;

		alert(b===a);//false

		var a={name:'William'}
		var b=a;
		b={name:'Jack'}

		alert(b===a);//true

由此可见，这种方式不能实现代码的重用与扩展。我们需要其它构建对象的方法。

 **4.类的概念:**
 >类是现实生活中一类具有共同特征的事物的抽象，是面向对象编程的基础。
 
上面是类的定义，如动物、植物，就是两种类。我们还可以把类看作是图纸或者模具,通过图纸和模具，可以生产出多个完全一样的产品。在程序中，模具就是类，生产出来的产品，就是类的实例。  

在其它言语中，都有类的概念，我们来看看PHP中如何定义一个类，并通过类实例化一个对象：
	
		//在PHP中，可以通过class关键字定义一个类
	    class Person{
	        var $name;//定义类的公有属性
	        private $age;//定义类私有属性
	        function sayName(){
	            echo($this->$name)
	        }
	        function setAge($age){//提供设置私有属性的方法,对属性值验证通过后才能设置
	            if($age<0||$age>110){
	                echo('年龄不符合要求');
	            }else{
	                $this->$age=$age;
	            }
	        }
	    }
	    //实例化一个对象，也可以理解为，通过模具，生产出来一个产品。
	    var $p1=new Person();
	    $p1->$name="William";//设置name属性
	    $p1->sayName();//输出William
	    $p1->$age=20;//错误，无法设置私有属性
	    $p1->setAge(20);

 **5.javascript中的类:**  
javascript里并没有类的概念，但是有构造函数，它和其它语言的类是非常相似的。
 顾名思义，构造函数是用来构造一个对象的，它需要通过关键字new来调用。如果你按普通的方式调用它，那它其实与普通函数并没有什么区别。

	    function Person(name){//定义一个构造函数。构造函数我们一般以大写字母开始
	        this.name=name;//给实例添加一个属性
	        this.sayName=function(){//给实例添加一个方法
	            alert('My name is'+this.name);
	        }
	    }

下面调用构造函数，记住一定要加关键字`new`
	
		var p1=new Person('William');//通过关键字new调用一个函数，会返回一个此构造函数的实例
	    var p1=Person('William');//错误。如果忘记加关键字new，不会返回实例，p1值是undefined
**注意：对于普通函数，不要通过new关键字调用，不然可能得不到你想要的结果** 
  
		function sum(a,b){
     		return a+b;
 		}
		var num=new sum(2,3);//错误，返回的是sum的实例，而不是计算结果。

 实例化了对象，我们就可以调用它的方法

		p1.sayName();//输出My name is William

如果我们需要多个对象，只需多次调用构造函数来实例化对象就可以了。
    
	    var p2=new Person('Jack');//再实例化一个对象
	    p2.sayName();//My name is Jack

我们来扩展p2，给它添加一个方法，并重写它的sayName方法

		p2.sayName=function(){//重写sayName方法
			alert('hello');
		}
		p2.eat=function(){
			alert('eating');//扩展添加一个新方法
		}
		p2.sayName();//hello
		p2.eat();//eating
		//下面我们在p1上调用这两个方法
		p1.sayName();//William,还是输出的原来的值
		p1.eat();//错误，p1并没有eat方法
		//也就是说，我们重写p2的sayName方法，扩展一个eat方法，并没有影响另一个实例p1
		//更进一步说，我们实例化一千个对象，这一千个对象都是不同的。但他们都是由一个构造函数构造的。
		//这样就节省了很多代码。
到现在为止，似乎面向对象的扩展性与灵活性都解决了。但写程序不只是解决问题，还对性能有要求。在现实世界中，一个人具有吃饭这个方法，另一个人具有另一个人的吃饭方法，这没有任何问题。但在程序中，存放对象及对象的属性与方法是需要内存空间的，一个对象的方法与属性越多，它占用的内存空间就越大。所以我们期望的是：**两个对象具有不同的属性（就好比人有高矮胖瘦），但它们的方法应该共享（因为功能是一样的)**，下面我们看p1与p2是不是共享一个方法的

	    //判断p1与p2的sayName方法是否相等
	    alert(p1.sayName===p2.sayName);//false。

p1与p2的方法并不相等，也就是说p1与p2各自存了一个sayName方法。当对象过多时，内存占用无疑会增加。所以要解决共享方法的问题，我们必须找其它方法。

 **6.对象的原型(prototype)：**
 >每个javascript对象都有一个原型(prototype属性)，原型上的方法，**可以被所有实例共享**。

上面提到，原型上的方法可以被所有实例共享，利用这个特点，我们可以把需要共享的方法，定义在对象的原型上，如下：
 

		var Person=function(name){
		 	this.name=name;
		};
	
		Person.prototype.sayName=function(){
		 	alert('My name is' +this.name);
		}

下面我们来检测，原型上的方法是不是被所有实例共享的
	
		var p1=new Person('William');
		var p2=new Person('Jack');
		alert(p1.sayName===p2.sayName);//true

p1与p2的sayName方法是相等的，可见，它们确实是共享的一个方法。也就是说，即使实例化一千个对象，它们都是共享的同一个sayName方法，大大的节约了内存的开销。这是怎么做到的？下面来看原型链。
	
	
**7.原型链：**  
>原型本身也是对象，它也有自己的原型，而它自己的原型对象又可以有自己的原型，这样就组成了一条链，这个链就是原型链。

每个实例对象都有一个\_\_proto\_\_属性，这个属性指向了该实例的构造函数的原型对象。我们知道对象是引用类型，也就是说\_\_proto\_\_属性只是存了一个指针，并不包含对象。当我们调用一个实例的方法时，程序首先会在实例本身上寻找这个方法，如果找不到，程序会通过\_\_proto__属性找到prototype对象，在prototype上查找这个方法，如果找到了就调用，如果没找到，它又会通过原型对象的原型去查找，直到找到顶点。

		p1.sayName()//其实p1实例上并没有sayName这个方法
		Person.prototype.sayName;//这时它会去原型对象上找这个方法

**8.对象的扩展与继承：**

    var Animal=function(){}
    Animal.prototype.eatFood=function(){
        alert('I\'m eating!');
    }
    
    var Vivipara=function(){};
    Vivipara.prototype=new Animal();//继承Animal
    Vivipara.prototype.sayName=function(){//扩展Animal
        alert('叽哩呱啦');
    }
    
    var Person=function(name){
        this.name=name;
    }
    Person.prototype=new Vivipara();
    Person.prototype.sayName=function(){
        alert('My name is' +this.name);
    }
    
    var p1=new Person('涛哥');
    p1.eatFood();
    p1.sayName();//输出My name is 涛哥,而不是叽哩呱啦，因为Person重写了sayName方法

 **9.需要注意的地方**
 1)不能在实例化的对象上设置prototype

    var Person=function(){}
    var p1=new Person;
    p1.prototype.sayName=function(){};//错误

 2)构造函数内及原型方法内关键字'this'的指向

    var Person=function(name){
        this.name=name;//this指向的是实例化的对象，而不是构造函数Person
    }
    Person.prototype={
        sayName:function(){
            console.log(this.name);//**同样，在原型的方法内，this指向的也是实例化出的对象，而不是原型对象。**
        }
    }

 3)静态方法（属性)、实例方法(属性)、原型方法(属性)

    var Person=function(){};
    Person.sayName=function(){
        alert(this.name);//静态方法内的this关键字指向的是构造函数。
    }
    var p1=new Person;
    p1.sayName();//错误，构造函数的静态方法，实例是不能调用的。
    Person.sayName();//Person
    
    var Person=function(name){
        this.name=name;//实例属性
        this.eat=function(){//实例方法
            alert('I am eating');
        }
    }
    
    Person.eat();//错误，相对应的，构造函也不能调用实例方法
    
    Person.prototype={
        sex:'female',//原型属性
        saySex:function(){//原型方法
            alert(this.sex);//female，注意，此时实例是没有sex这个属性的，它是通过原型链，找到原型上的sex属性并输出
        }
    }
    Person.saySex();//错误，同理,构造函数也不能调用原型对象上的方法
    Person.prototype.saySex();//可以通过原型对象调用原型方法
    

 4)对象的私有属性与私有方法

    function Person(name){
        this._name=name;
    }
    Person.prototype={
        /**
         * @private
        **/
        _sayName:function(){
            
        },
        getName:function(){
            return this._name;
        },
        setName:function(name){
            this._name=name;
        }
    }
    var p1=new Person('xiaoli');
    /**
        虽然js的对象属性可以在任务时间修改，但对于对象标识了私有的属性，最好不要直接修改
        而是通过该对象提供的接口进行修改,同样，标识了私有的方法，也不要去调用
     **/
    p1._name='taoge';//错误
    p1.setName('William');//正确
