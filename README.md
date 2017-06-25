# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)  
  
## C# Track  
  
- L01: History and Introduction  
> - **Software Life Cycle** [Gathering Requirements, Analysis, Design, Development, Testing, Deployment, Maintenance]  
> - **Testing** [Unit Test, Functional Test, Performance Test, Stress Tess, User Acceptance Test]  
> - **History**  
>  COOL (C like Object Oriented Language) => C#  
>  C++++  
> - Programming Language  
>  **Compiler** is a program that translates program written in some high level language into object code.  
>  **Interpreter** translates high level instructions into an intermediate form, which it then executes.  
>  msil (microsoft intermediate language)  
> - Users [Developer, Tester, End User]  
> - Libraries (Static V Dynamic)  
> - Errors [Syntax Error, Logical Error, Run Time Error, Warning]  
> ```cs
> // Hello World
> using System;
> struct EntryPoint{
>   public static void Main(){
>     Console.WriteLine("Hello World!");
>     Console.ReadLine();
>   }
> }
> ```
---
- L02: Data Types and Operators  
> - **Data Types**  
>  (sbyte = 1 byte), (short, ushort = 2 bytes), (int, uint = 4 bytes), (long, ulong = 8 bytes), (byte = 1 byte), (char = 2 bytes), (bool = 1 byte), (float = 4 bytes), (double = 8 bytes), (decimal = 16 bytes), (string, object = N/A)  
>  Value Types V Reference Type  
> - **Operators** [Arithmetic, Assignment, Relational, Logical, Bitwise, Ternary]  
>  **Arithmetic** [Unary(++, --), Binary(+, -, *, /, %)]  
>  **Assignment** (=, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=)  
>  **Relational** (==, !=, <, >, <= , >=)  
>  **Logical** (!, &&, ||, true, false)  
>  **Bitwise** (&, |, ^, <<, >>, ~)  
>  **Ternary** (var = cond ? when true : when false;)  
---  
- L03: Control Statments  
> Conditional Statments [Switch, If Else], Loop Statments [For, While, Do While]  
> - **Conditional Statments**
>  Switch (int, float, char, string)  
> ```cs
> Console.Write("Please enter a char");
> char c = char.Parse(Console.ReadLine());
> switch (c)
> {
>   case'A':
>   case'a':
>     Console.WriteLine("Hi Ahmed");
>     break;
>   case'B':
>   case'b':
>     Console.WriteLine("Hi Bassem");
>     break;
>   default:
>     Console.WriteLine("Error");
>     break;
> }
> ```
> If Else (boolean)
> ```cs
> if(c=='a' || c=='A'){
>   Console.WriteLine("Hi Ahmed");
> }
> else if(c=='b' || b=='B'){
>   Console.WriteLine("Hi Bassem");
> }
> else{
>   Console.WriteLine("Error");
> }
> ```
> - **Loop Statments**  
> For Loop  
> ```cs
> for(int i = 0; i < 10; i++){
>   Console.Write("{0}", i)
> }
> // Infinite Loops
> for(;;){}
> ```
---  
- L04: Functions  
> Do While Loop  
> when the you need the code to run at least once.  
> ```cs
> int total = 0;
> int x;
> do{
>   Console.Write("Please Enter No:");
>   x = int.Parse(Console.ReadLine());
>   total += x;
> }while(total < 100)
> ```
> While Loop  
> Check first then loop  
> ```cs
> int total = 0;
> int x;
> while(total < 100){
>   Console.Write("Please Enter No:");
>   x = int.Parse(Console.ReadLine());
>   total += x;
> }
> ```
> - Functions  
>  ```cs
>  public static int Sum(int x, int y){
>    int total = x + y;
>    return total;
>  }
>  int nine = Sum(5, 4);
>  ```
>  *Recursion*  
---
- L05: Functions  
> ```cs
> public static void PrintBinary(int no){
>   int div = no / 2;
>   int mod = no % 2;
>   if(n > 1){
>     PrintBinary(div);
>   }
>   Console.WriteLine(mod);
> }
> ```
---
- L06: Arrays  
> *MagicBoxExample*
> ```cs
> public static bool PrintMagicBox(int size, int x, int y, int xFactor, int yFactor){
>     bool devFlag = true;
>     if(size%2 == 0){
>       devFlag = false
>     }
>     else{
>       devFlag = true;
>       int row = 1;
>       int col = size/2 + 1;
>   
>       for(int i = 1; i <= size * size; i++){
>           Console.SetCursorPosition(col * xFactor + x, row * yFactor + y);
>           Console.Write('{0}', i);
>           if(i % size == 0){
>             row++;
>             if(row>size){row = 1;}
>           }
>           else{
>             row--;
>             if(row == 0){row = size;}
>             col--;
>             if(col == 0){col = size;}
>           }
>       }
>    }
>   return devFlag;
> }
> ```
> - **Arrays**  
> ```cs
> public static int[] GetNumbersFromUser(int size){
>     int[] result = new int[size];
>     for(int i = 0; i < size; i++){
>       ConsoleWrite("Please Enter data no {0}:", i+1);
>       result[i] = int.Parse(Console.Readline());
>     }
>   return result;
> }
> 
> public static void PrintNumbersToUser(int[] data, int size){
>   for(int i =0; i < size; i++){
>     Console.WriteLine(data[i]);
>   }
> }
> ```
---
- L07: Struct and Enum  
> 2-Dim Arrays and Array of Arrays.  
> ```cs
> public static int[][] GetDataFromUser(){
>   Console.Write("Please Enter No Of Rows");
>   int row = int.Parse(Console.ReadLine());
>   int[] cols = new int[row];
>   for(int i = 0; i < row; i++){
>     Console.Write("Please Enter Size of Row No {0}", i + 1);
>     cols[i] = int.Parse(Console.ReadLine());
>   }
>   int[][] result = GetArrayFromUser(row, cols);
>   for(int i =0; i < row; i++){
>     for(int j = 0; j < cols[i]; j++){
>       Console.WriteLine("data[{0}][{1}]", i + 1, j+ 1);
>       result[i][j] = int.Parse(Console.ReadLine());
>     }
>   }
> }
> ```
> - **Structures**
>  ```cs
>  struct Point{
>    public int x;
>    public int y;
>  }
>  ...
>  Point p1; // = new Point(); set to default values.  
>  p1.x = 14;
>  p1.y = 9;
>  ```
> - **Enum**  
>  ```cs
>  enum NumberType{
>    Odd = 1;
>    Even = 2;
>    Normal = 3;
>  }
>  ```
---  
- L08: Classes and Namespaces
> - **Class**
> ```cs
> // Employee.cs default internal 
> public class Employee{
>   public int code;
>   public string name;
>   public float salary;
>   float bonus; // private use only in class itself
> }
> 
> // EntryPoint
> using System;
> 
> class EntryPoint{
>   public static void Main(){
>     Employee e = new Employee();
>     e.code = 2122;
>   }
> }
> ```
> - **Namespace**
> ```cs
> // Employee.cs
> namespace Office{}
>   public class Employee{
>     ...
>   }
> }
> 
> // EntryPoint
> using System;
> using Office;
> class EntryPoint{
>   public static void Main(){
>     Employee e = new Employee();
>     ...
>   }
> }
> ```
> - **String**  
>  String and string are the same.  
>  delimiter \0  
---
- L09: Variables and Nullable  
>  - **Variables**
>  Get its type on initialization  
>  var x = 3; // x is int  
>  var y = 5.5 // y is float  
>  var z = {id = 2m name = "M"} // Anon. type  
> - Dynamic type  
>  get its type at the run after the compilation  
>  *dynamix x = "hi";*  
> - **Nullable**  
>  value type can not take a null, reference types can  
>  nullable types ex: *int? x = null;*  
>  int y = x??0; // if x is null then y = 0;  
> - Implicit/Explicit Casting, Boxing/Unboxing  
---