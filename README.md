# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)  
  
Though this is not part of the ITI series, this is the recommended course on Data Structure from FCIH-OCW by Dr. [Waleed A. Yousef](http://www.helwan.edu.eg/university/staff/Dr.WaleedYousef/HTML/DataStructures.html).  

## Data Structures  

- L01: Introduction to Data Structures  
> - Why Data Structure (Queue, Stack, Tree, Graphs)  
---
- L02: Concepts: Encapsulation and ADT  
> - array as a familiar data structure.  
>   ```c
>   int MyArr[10];
>   ```
>   reserving a continuous space in memory so that *memory size = element size * #elements*  
>   giving the starting address the name MyArr.  
>   ```c
>   MyArr[3] = 27;
>   ```
>   This calculates the location address = MyArr + 3 * sizeof(int)  
>   Then stores 27 in that location.  
> - Information Hiding (Encapsulation)  
>  The use of functions. You use the structure at the user level without caring about the details at the implementation level.  
> - Definitions  
>  *type* is a set of values and a set of operations on thouse values.  
>  *sequence of length 0* is empty. A seuence of length n >= 1 of elements from a set T is an ordered pair (S_n-1, t) where S_n-1 is a sequence of length n - 1 of elements from n and t is an element of T.  
>  **Abstraction Data Type (ADT)** is a data type that is accessed only through an interface or ( Accessing mechanism). We refer to a program that uses an ADT as a client and a program that specifies the data type as an implementation.  
>  **Stack** of elements of type T is a finite sequence of element of T together with the following operations: create stack, determine whether if full or not, determine whether if empty or not, find size, push new entry, pop entry, retrieve the top entry, traverse entries, clear the stack.  
---  
- L03: Stacks: Array-based Implementation I  
> ```c
> typedef struct stack{
>   int top;
>   StackEntry entry[MAXSTACK];
> }Stack;
> 
> void CreateStack(Stack *ps){
>   ps->top = 0;
> }
> 
> void Push(StackEntry e, Stack *ps){
>   ps->entry[ps->top++] = e;
> }
> 
> void main{
>   StackEntry e;
>   Stack s;
>   CreateStack(&s);
>   if(!StackFull(s)){Push(e, &s);}
> }
> ```
> It is not a good idea nor professional to handle exception with print statment on the implementation level.  
---  
- L04: Stacks: Array-based Implementation II  
> It could be StackFull(s) but this wastes memory and time of copying.  
> ```c
> ...
> int StackFull(Stack *ps){
>   return ps->top >= MAXSTACK;
> }
> 
> void Pop(StackEntry *pe, Stack *ps){
>   *pe = ps->entry[--ps->top];
> }
> int StackEmpty(*ps){
>   return !ps->top;
> }
> 
> void Pop(StackEntry *pe, Stack *ps){
>   *pe = ps->entry[ps->top - 1];
> }
> 
> int StackSize(*ps){
>   return ps->top;
> }
> 
> void ClearStack(Stack *ps){
>   ps->top = 0;
> }
> void main(){
>   ...
>   if(!StackFull(&s)){Push(e, &s);}
>   if(!StackEmpty(&s)){Pop(&e, &s);}
>   if(!StackEmpty(&s)){StackTop(&e, &s);}
>   x = StackSize(&s);
>   ClearStack(&s);
> }
> ``` 