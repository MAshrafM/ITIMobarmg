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
> //Implementation Level
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
> // User Level
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
> //Implementation Level
> ...
> int StackFull(Stack *ps){
>   return ps->top >= MAXSTACK;
> }
> 
> void Pop(StackEntry *pe, Stack *ps){
>   *pe = ps->entry[--ps->top];
> }
> int StackEmpty(Stack *ps){
>   return !ps->top;
> }
> 
> void StackTop(StackEntry *pe, Stack *ps){
>   *pe = ps->entry[ps->top - 1];
> }
> 
> int StackSize(Stack *ps){
>   return ps->top;
> }
> 
> void ClearStack(Stack *ps){
>   ps->top = 0;
> }
> //User Level
> void main(){
>   ...
>   if(!StackFull(&s)){Push(e, &s);}
>   if(!StackEmpty(&s)){Pop(&e, &s);}
>   if(!StackEmpty(&s)){StackTop(&e, &s);}
>   x = StackSize(&s);
>   ClearStack(&s);
> }
> ``` 
---  
- L05: Stacks: Array-based Implementation III  
> ```c
> //implementation level
> ...
> void TraverseStack(Stack *ps, void(*pf)(StackEntry)){
>   for(int i = ps->top; i > 0; i--){
>     (*pf)(ps->entry[i-1]);
>   }
> }   
> void main(){
>   ...
>   TraverseStack(&s, &Display);
> }
> //user level
> void Display(StackEntry e){
>   printf("e is: %d\n", e);
> }
> // if stack top was not implemented on the implementation level.  
> void StackTop(StackEntry *pe, Stack *ps){
>   Pop(pe, ps);
>   Push(*pe, ps);
> }
> ```
> **Notes** StackEntry and MAXSTACK should be defined in the User Level because they concern the user, Also they have to be defined in the implementation level because they are referenced in Stack.cpp; then they have to be defined in Stack.h which is included in both Stack.cpp and the user main file.  
> ```c
> /***** Stack.h *******/
> #define MAXSTACK 100
> typedef struct stack{
>   int top;
>   StackEntry entry[MAXSTACK];
> }Stack;
>
> void Push(StackEntry, Stack *);
> void Pop(StackEntry *, Stack *);
> int StackEmpty(Stack *);
> int StackFull(Stack *);
> void CreateStack(Stack *);
> void Top(StackEntry *, Stack *);
> int StackSize(Stack *);
> void ClearStack(Stack *);
> void TraverseStack(Stack *, void(*)(StackEntry));
> ```
---  
- L06: Stacks: Linked-based Implementation I  
> *type definition*  
> diffrentiate between stacknode and stack to make logical distinction between the stack itself and its top which points to the node. and for upgradability.  
> ```c
> typdef struct stacknode{
>   SrackEntry entry;
>   struct stacknode next;
> }StackNode;
> 
> typdef struct stack{
>   StackNode *top;
> }Stack;
> 
> // Implementation Level
> void CreateStack(Stack *ps){
>   ps->top = NULL; // Null defined in <stdlin.h>
> }
> 
> void Push(SrackEntry e, Stack *ps){
>   StackNode *pn = (StackNode*)malloc(sizeof(StackNode));
>   pn->entry = e;
>   pn->next = ps->top;
>   ps->top = pn;
> }
> 
> void Pop(StackEntry *pe, Stack *ps){
>   StackNode *pn;
>   *pe = ps->top->entry;
>   pn = ps->top
>   ps->top = ps->top->next;
>   free(pn); 
> }
> void  StackTop(StackEntry *pe, Stack *ps){
>   *pe = ps->top->entry;
> }
> int StackEmpty(Stack *ps){
>   return !ps->top;
> }
> int StackFull(Stack *ps){
>   return 0;
> }
> 
> // User Level
> 
> void main(){
>   Stack s;
>   CreateStack(&s);
>   Push(e, &s);
>   Pop(&e, &s);
>   StackTop(&e, &s)
> }
> ```
---