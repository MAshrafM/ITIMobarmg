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