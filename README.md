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
>   //int size;
> }Stack;
> 
> // Implementation Level
> void CreateStack(Stack *ps){
>   ps->top = NULL; // Null defined in <stdlin.h>
>   //size = 0;
> }
> 
> void Push(SrackEntry e, Stack *ps){
>   StackNode *pn = (StackNode*)malloc(sizeof(StackNode));
>   pn->entry = e;
>   pn->next = ps->top;
>   ps->top = pn;
>   //size++;
> }
> 
> void Pop(StackEntry *pe, Stack *ps){
>   StackNode *pn;
>   *pe = ps->top->entry;
>   pn = ps->top
>   ps->top = ps->top->next;
>   free(pn); 
>   size--;
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
- L06: Stacks: Linked-based Implementation II  
> ```c
> void ClearStack(Stack *ps){
>   StackNode *pn = ps->top;
>   while(pn){
>     pn = pn->next;
>     free(ps->top);
>     ps->top = pn;
>   }  
>   // size = 0;
> }
> 
> void TraverseStack(Stack *ps, void(*pf)(SrackEntry)){
>   StackNode *pn = ps->top;
>   while(pn){
>     (*pf)(pn->entry);
>     pn = pn->next;
>   }
>   //for(StackNode *pn = ps->top; pn; pn = pn->next){(*pf)(pn->entry);}
> }
> int StackSize(Stack *ps){
>   int x;
>   StackNode *pn = ps->top;
>   for(x = 0; pn; pn = pn->next){ x++; }
>   return x;
>   // retrun ps->size;
> }
> ```
> Which is better (Array-based || Linked-based) ? is a wrong question. Know very well the pros and cons of each implementation and decided based on your application needs.  
---  
- L08: Stacks application: Recursion.  
> The great importance of stacks is OS.  
> *Tower of Hanoi*
> ```c
> void MoveDisks(int count, int start, int finish, int temp){
>   /*Pre:
>     - There are at least count disks in the tower start.
>     - The top disk on each of towers temp and finish is larger than any of the top count disks on tower start.
>   Post: 
>     - The top count disks on start have been moved to finish;
>     - temp (used for temporary storage) has been returned to its starting position
>   */
>   if(count > 0){
>     MoveDisks(count - 1, start, temp, finish);
>     printf("Move disk %d from %d to %d\n", count, start, finish);
>     MoveDisks(count - 1, temp, finish, start);
>   }
> }
> ```
> There are some cases in which solving the problem iteratively is better if the iterative algorithm does not need a stack. Hence solving it recursively builds an unnecessarily stack; which wastes memory and time consumed in function return.  
> ```c
> // Factorial iteratively
> int Factorial(int n){
>   //it is better to return a double instead of int
>   int count, product;
>   for(product = 1, count = 2; count <= n; count++){ product *= count; }
>   return product;
> }
> // Factorial recursively, not needed
> int Factorial(int n){
>   return ( n == 0) ? 1 : (n*Factorial(n-1));
> }
> // Fibonacci recursively O(c^n)
> int Fibonacci(int n){
>   if(n <= 0){ return 0;}
>   else if(n == 1){ return 1;}
>   else return Fibonacci(n-1) + Fibonacci(n-2);
> }
> // Fibonacci iteratively O(n)
> int Fibonacci(int n){
>   int i, twoback, oneback, current;
>   if(n <= 0){ return 0; }
>   else if(n == 1){ return 1; }
>   else{
>     twoback = 0;
>     oneback = 1;
>     for(i = 2; i <= n; i++){
>       current = twoback + oneback;
>       twoback = oneback;
>       oneback = current;
>     }
>     return current;
>   }
> }
> ```
> Tail Recursion: Last statment in a function is a call to itself. *if a tail recursion occur then it can be replaced by an iteration.
> ```c
> void MoveDisks(int count, int start, int finish, int temp){
>   int swap;
>   while(count > 0){
>     MoveDisks(count - 1, start, temp, finish);
>     printf("Move disk %d from %d to %d\n", count, start, finish);
>     count--;
>     swap = start;
>     start = temp;
>     temp = swap;
>   }
> }
> ```
---  
- L09: Stacks application: Polish Notation  
> Convert from infix to postfix
> ```c
> void InfixToPostfix(char infix[], char postfix[]){
>   int i,j;
>   char op, c;
>   Stack s;
>   CreateStack(&s);
>   for(i = 0; j = 0; (c = infix[i])!= '\0'; i++){
>     if(IsDigit(c)){ postfix[j++] = c; }
>     else{
>       if(!StackEmpty(&s)){
>         StackTop(&op, &s);
>         while(!StackEmpty(&s) && Precedent(op, c)){
>           Pop(&op, &s);
>           postfix[j++] = op;
>           if(!StackEmpty(&s)){ StackTop(&op, &s); }
>         }
>       }
>       Push(c, &s);
>     }
>   }
>   while(!StackEmpty(&s)){
>     Pop(&op, &s);
>     postfix[j++] = op;
>   }
>   postfix[j] = '\0';
> }
> 
> int isDigit(char c){
>   return(c>='0' && c<= '9');
> }
> 
> int Precedent(char op1, char op2){
>   if(op1 == '$') return 1;
>   if((op1 == '*') || (op1 == '/')) return (op2!='$');
>   if((op1 == '+') || (op1 == '-')) return ( (op2!='$')&&(op2!='*')&&(op2!='/') );
>   return 0;
> }
> 
> void main(){
>   char infix[]= "1+2*3$4/5+6";
>   char postfix[8];
>   InfixToPostfix(infix, postfix);
>   printf("\n %s", postfix);
>   getch();
> }
> /**********/
> double EvaluatePostfix(char expr[]){
>   int i;
>   char c;
>   double op1, op2, val;
>   Stack s;
>   CreateStack(&s);
>   for(i = 0; (c = expr[i])!='\0'; i++){
>     if(IsDigit(c)){
>       Push((double)(c-'0'), &s);
>     }
>     else{
>       Pop(&op2, &s);
>       Pop(&op1, &s);
>       val = Oper(c, op1, op2);
>       Push(val, &s);
>     }
>   }
>   Pop(&val, &s);
>   return val;
> }
> double Oper(char c, double op1, double op2){
>   switch(c){
>     case '+': return (op1+op2);
>     case '-': return (op1-op2);
>     case '*': return (op1*op2);
>     case '/': return (op1/op2);
>     case '$': return (pow(op1,op2));
>   }
> }
> ```
> *Notes* We can not use InfixToPostfix and EvaluatePostfix in the same program because of different Element types. thus a sol is by preprocessing for now!  
> ```c
>   /* Stack.h */
>   //#define INFIX_TO_POSTFIX
>   #define EVALUATE_POSTFIX
>   
>   #ifdef INFIX_TO_POSTFIX
>     typedef char ElementType;
>     #define MAXELEMENTS 100
>     typedef ElementType StackEntry;
>     #define MAXSTACK MAXELEMENTS
>   #endif
>   
>   #ifdef EVALUATE_POSTFIX
>     typedef double ElementType;
>     #define MAXELEMENTS 100
>     typedef ElementType StackEntry;
>     #define MAXSTACK MAXELEMENTS
>   #endif
> ```  
---  
- L10: Queues: Array-based Implementation  
> FIFO structure  
> Circular implementation  
> A *Queue* of elements of type T is a finite sequence of elements of T together with the following operations: (create, determine whether empty or full, find size, append, retrieve, serve, traverse and clear)  
> ```c
> typedef struct queue{
>   int front;
>   int rear;
>   int size;
>   QueueEntry entry[MAXQUEUE];
> }Queue;
> 
> // Implementation Level
> void CreateQueue(Queue *pq){
>   pq->front = 0;
>   pq->rear = -1;
>   pq->size = 0;
> }
> void Append(QueueEntry e, Queue *pq){
>   pq->rear = (pq->rear + 1) % MAXQUEUE;
>   pq->entry[pq->rear] = e;
>   pq->size++;
> }
> void Serve(QueueEntry *pe, Queue *pq){
>   *pe = pq->entry[pq->front];
>   pq->front = (pq->front + 1) % MAXQUEUE;
>   pq->size--;
> }
> int QueueEmpty(Queue *pq){
>   retrun !pq->size
> }
> int QueueFull(Queue *pq){
>   return (pq->size == MAXQUEUE);
> }
> int QueueSize(Queue *pq){
>   return pq->size;
> }
> void ClearQueue(Queue *pq){
>   pq->front = 0;
>   pq->rear = -1;
>   pq->size = 0;
> }
> void TraverseQueue(Queue *pq, void(*pf)(QueueEntry)){
>   int pos, s;
>   for(pos = pq->front, s = 0; s < pq->size; s++){
>     (*pf)(pq->entry[pos]);
>     pos = (pos + 1) % MAXQUEUE;
>   } 
> }
> ```
---  
- L11: Queues: Linked-based Implementation  
> ```c 
> typdef struct queuenode{
>   QueueEntry entry;
>   struct queuenode *next;
> }QueueNode;
> typdef struct queue{
>   QueueNode *front;
>   QueueNode *rear;
>   int size;
> }Queue;
> 
> void CreateQueue(Queue *pq){
>   pq->front = NULL;
>   pq->rear = NULL;
>   pq->size = 0;
> }
> int Append(QueueEntry e, Queue *pq){
>   QueueNode *pn = (QueueNode*)malloc(sizeof(QueueNode));
>   // do this also for Stacks to check for exhausted memory after malloc
>   if(!pn){return 0;}
>   else{
>     pn->next = NULL;
>     pn-entry = e;
>     if(!pq->rear){pq->front = pn;}
>     else{pq->rear->next = pn;}
>     pq->rear = pn;
>     pq->size++;
>   }
> }
> void Serve(QueueEntry *pe, Queue *pq){
>   QueueNode *pn = pq->front;
>   *pe = pn->entry;
>   pq->front = pn->next;
>   free(pn);
>   if(!pq->front){pq->rear = NULL;}
>   pq->size--;
> }
> int QueueEmpty(Queue *pq){
>   retrun !pq->size
> }
> int QueueFull(Queue *pq){
>   return 0;
> }
> int QueueSize(Queue *pq){
>   return pq->size;
> }
> void ClearQueue(Queue *pq){
>   while(pq->front){
>     pq->rear = pq->front->next;
>     free(pq->front);
>     pq->front = pq->rear;
>   }
>   pq->size = 0;
> }
> void TraverseQueue(Queue *pq, void(*pf)(QueueEntry)){
>   int pos, s;
>   for(QueueNode *pn = pq->front; pn; pn = pn->next){
>     (*pf)(pq->entry);
>   } 
> }
> ```  
---