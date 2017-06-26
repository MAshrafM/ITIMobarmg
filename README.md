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

