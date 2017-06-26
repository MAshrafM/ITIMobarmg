# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)  
  
## Object Oriented Programming Track  
  
- L01: Introduction  
> - Content(Abstraction Encapsulation, Polymorphorphism,  Inheritance)  
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



