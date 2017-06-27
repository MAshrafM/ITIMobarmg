# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)  
  
## Object Oriented Programming Track  
  
- L01: Introduction  
> - Content(Abstraction Encapsulation, Polymorphism,  Inheritance)  
> - *class*
>  Make Every class in a seperate file.
>  Do not set public on a prop. use setter/getter  
>  Constructor: special function runs automatic when an object is created from a class, ithas the same name as the class, does not have a return type.  
>  Overloading: 2 or more functions with the same name with different number or types of parameters and returns.  
>  overloading the constructors gives more variety for the developer when working with the class.  
>  Destructor||Finalizer: clear the object from heap when object got removed from memory, do not have access modifiers, start with ~ and take no params.  

> ```cs
> class Point{
>   int x;
>   int y;
>   public int GetX { return x; }
>   public int SetX(int _x) { x = _x; }
>   public Point(int _x, int _y){
>     x = _x;
>     y = _y;
>   }
>   public Point(){
>     x = y = 0;
>   }
>   public Point(int no){
>     x = y = no;
>   }
>   ~Point(){
>   }
> }
> ```
---
- L02: Classes and Objects  
> - *Queue* FIFO
> ```cs
> class Queue{
>   int[] data;
>   int size;
>   int count;
>   int toq;
>   int eoq;
>   
>   public int Getsize(){ return size; }
>   public int GetCount(){ return count; }
>   public bool SetSize(int _size){
>     bool result = false;
>     if(_size >= count){
>       result = true;
>         Queue temp = new Queue(_size);
>         int no;
>         while(t = dequeue() != null){
>           temp.push(t);
>         }
>         size = temp.size;
>         toq = temp.toq;
>         eoq = temp.eoq;
>         count = temp.count;
>         data = temp.data;
>     }
>     return result;
>   }
>   public Queue(int _size){
>     data = new int[_size];
>     size = _size;
>     toq = 0;
>     eoq = 0;
>     count = 0;
>   }
>   
>   public Queue(){
>     data = new int[10];
>     size = 10;
>     toq = 0;
>     eoq = 0;
>     count = 0;
>   }
>   
>   public bool enqueue(int no){
>     bool result = false;
>     if(count < size){ 
>       data[eoq] = no;
>       result = true;
>       eoq++;
>       if(eoq == size){ eoq = 0; }
>       count++;
>     }
>     return result;
>   }
>   
>   public int? dequeue(){
>     int result = null;
>     if (count > 0){
>       result = data[toq];
>       toq++;
>       if(toq == size){ toq = 0; }
>       count--;
>     }
>     return result;
>   }
> }
> ```
- L03: Encapsulation  
> *this* pointer  
> *this* chaining on constructors.  
> ```cs
> class Point{
>   int x;
>   int y;
>   public int GetX { return x; }
>   public int SetX(int x) { this.x = x; }
>   public Point(int x, int y){
>     this.x = x;
>     this.y = y;
>   }
>   public Point():this(0,0)
>   public Point(int no):this(no,no)
>   ~Point(){ ... }
> }
> ```
> *property*  
> *static*, is not available in every object just in the class itself, static constructor is what called first with the first encounter with class.  
> ```cs
> class Complex{
>   int real;
>   int imag;
>   static int count;
>   // Properties
>   public int Real{
>     set{ real = value; }
>     get{ return real; }
>   } 
>   public int Imag{ 
>     set{ imag = value; }
>     get{ return imag; }
>   } 
>   public static int Count{
>     get{ return count;}
>   }
>   // Constructors
>   public Complex(int real, int imag){
>     this.real = real;
>     this.imag = imag;
>     count++;
>   }
>   public Complex(int _real):this(_real, 0){}
>   static Complex(){ count = 0; }
>  //Methods
>  /// Complex x = Complex..Add(c1, c2);
>  public static Complex Add(Complex c1, Complex c2){
>    return new Complex(c1.real + c2.real, c1.imag + c2.imag);
>  }
>  //operator overloading
>  /// Complex x = c1 - c2 - c3 - c4 ;
>  public static Complex operator-(Complex c1, Complex c2){
>    return new Complex(c1.real - c2.real, c1.imag - c2.imag);
>  }
>  public static Complex operator-(Complex c1, int no){
>    return new Complex(c1.real - no, c1.imag);
>  }
>  // using the same function above ^ to avoid repeating
>  public static Complex operator-(int no, Complex c1){
>    return new c1 + no;
>  }
>  // cast to complex implicit/explicit
>  public static implicit operator Complex(int no){ return new Complex(no);}
>  public static explicit operator int(Complex c){ return c.real; }
> }
> ```
- L04: Operator Overloading  
> Continue Complex Class Operators  
> ```cs
>  ...
>   public static bool operator >(Complex c1, Complex c2){
>     bool result = false;
>     double pC1 = Math.Sqrt(c1.real ^ 2 + c1.imag ^ 2);
>     double pC2 = Math.Sqrt(c2.real ^ 2 + c2.imag ^ 2);
>     if(pC1 > pC2){result = true;}
>     return result;
>   }
>   public static bool operator >=(Complex c1, Complex c2){
>     bool result = false;
>     if(c1 > c2 || (c1.real == c2.real && c1.imag == c2.imag)){result = true;}
>    return result;
>   }
>   public static bool operator <(Complex c1, Complex c2){
>     bool result = false;
>     if(c2 > c1){result = true;}
>     return result;
>   }
>   public static Complex operator ++(Complex c){
>     return new Complex(c.real+1, c.imag);
>   }
> ```  
> - *Single Tone Design Pattern*  
---
- L05: Constructors
> Relations between classes (Composition, Aggregation, Associations, Inheritance, InnerClass) 
> **Composition** 
> ```cs
> class Wall{
>   float width;
>   float height;
>   float thick;
>   
>   public float Width{
>     get { return width; }
>     set { width = value; }
>   }
>   public float Height{
>     get { return height; }
>     set { height = value; }
>   }
>   public float Thick{
>     get { return thick; }
>     set { thick = value; }
>   }
>   
>   public Wall(float _width, float _height, float _thick){
>     width = _width;
>     height = _height;
>     thick = _thick;
>   }
>   public Wall(float _width, float _height):this(_width, _height, 0.25f);
>   public Wall(float _width):this(_width, 2.6f, 0.25f);
>   //Copy Constructor
>   public Wall(Wall w):this(w.width, w.height, w.thick)
>   //Clone
>   public Wall Clone(){
>     return new Wall(this);
>   }
>   
> }
> 
> class Room{
>   Wall w1;
>   Wall w2;
>   Instructor[] instructors;
>   
>   public Wall w1{
>     get { return w1; }
>     set{ if(value != null){ w1 = value }}
>   }
>   public Wall w2{
>     get { return w2; }
>     set{ if(value != null){ w2 = value }}
>   }
>   
>   public Room(float w1Width, float w1Height, float w1Thick, float w2Width, float w2Height, float w2Thick, params Instructor[] _instructors){
>     w1 = new Wall(w1Width, w1Height, w1Thick);
>     w2 = new Wall(w2Width, w2Height, w2Thick);
>     instructors = _instructors;
>   }
>   public Room(float w1Width, float w1Height, float w2Width, float w2Height, params Instructor[] _instructors){
>     w1 = new Wall(w1Width, w1Height);
>     w2 = new Wall(w2Width, w2Height);
>     instructors = _instructors;
>   }
>   public Room(Wall _w1, Wall _w2):this(_w1.Width, _w1.Height, _w1Thick, _w2.Width, _w2.Height, _w2.Thick, null)
>   public Room(Room r):this(new Wall(r.w1), new Wall(r.w2))
> }
>   Public Room Clone(){ return new Room(this); }
> ```
---
- L06: Inheritance  
> ```cs
> class Instructor{
>   private int id;
>   Room room;
>   
>   public int Id{
>     get{return id;}
>     set{id = value;}
>   }
>   internal Room Room{
>     get {return room;}
>     set {room = value;}
>   }
>   public string Name{ get; set; }
>   public Instructor(int id, string name, Room room){
>     this.id = id;
>     this.Name = name;
>     this room = room;
>   }
>   public Instructor():this(default(int), null, null)
>   public Instructor(Instructor i):this(i.id, i.Name, i.room)
>   public Instructor Clone(){return new Instructor(this);}
> }
> ```
> - *Inheritance*  
>  All classes inherent from Object.  
>  protected on parent acts as public only on childreen and private otherwise.  
> - Classes types (conceret, sealed, abstract, static, partial, inner)  
>  *sealed* prevent class to inherent from it  
>  *abstract* cannor be instantiated.  
---
- L07: Inheritance 2  
> *hiding*: having a method in the child with the same name as in the parent; to call the parent method from the child you *base.* it.   
> *override*: child method override methods with the same name and *virtual* modifier in the parent.  
> Dynamic Binding.  
---
- L08: Abstraction
> An abstract class means that, no object of this class can be instantiated, but can make derivations of this.  
> An abstract class cannot be a sealed class.  
> An abstract method cannot be private.  
> An abstract member cannot be static.
> An abstract method cannot have the modifier virtual. Because an abstract method is implicitly virtual.  
---  
- L09: Polymorphism  
> In C#, every type is polymorphic because all types, including user-defined types, inherit from Object.  
> When a derived class inherits from a base class, it gains all the methods, fields, properties and events of the base class. The designer of the derived class can choose whether to: override virtual members in the base class, inherit the closest base class method without overriding it; define new non-virtual implementation of those members that hide the base class implementations.  
> Polymorphism is often referred to as the third pillar of object-oriented programming, after encapsulation and inheritance.  
--- 
- L10: Intrface  
> An interface is defined as a syntactical contract that all the classes inheriting the interface should follow.  
> Interfaces contain only the declaration of the members. It is the responsibility of the deriving class to define the members. It often helps in providing a standard structure that the deriving classes would follow.  
> Abstract classes to some extent serve the same purpose, however, they are mostly used when only few methods are to be declared by the base class and the deriving class implements the functionalities.  
> Implicit/Explicit implementation.  
> - Exceptions  
>  *throw*  
>  *try{} catch{}*  
---