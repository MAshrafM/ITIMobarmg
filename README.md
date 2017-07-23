# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)  
  
## Adavanced C# Track  
  
- L01: Delegate  
> A delegate is a type that represents references to methods with a particular parameter list and return type.  
> Delegates are used to pass methods as arguments to other methods.  
```cs
// init delegate
delegate void MyDelegate<T>(T[] arr) where T:IComparable;
// main program
class Program{
  static void Main(string[] args){
    int[] x = {3, 2, 7, 8, 1, 0, 24, 66};
    Sort(x, SelectionSort);
    //chaining
    MyDelegate<int> m = BubbleSort;
    m += SelectionSort;
    m(x);
  }
  public static void Sort<T>(T[] arr, MyDelegate<T> m) where T:IComparable{
    m(arr);
  }
  // delegated functions  
  static void SelectionSort<T>(T[] arr) where T:IComparable<T>{
    for(int i = 0; i < arr.Length - 1; i++){
      for(int j = i + 1; j < arr.Length; j++){
        if(arr[i].CompareTo(arr[j]) > 0){
          Swap(ref arr[i], ref arr[j]);
        }
      }
    }
  }
  
  static void BubbleSort<T>(T[] arr) where T:IComparable<T>{
    int y = 1;
    bool sorted = false;
    do{
      sorted = true;
      for(int i = 0; i < arr.Length - y; i++){
        if(arr[i].CompareTo(arr[i+1]) > 0){
          Swap(ref arr[i], ref arr[i+1]);
          sorted = false;
        }
      }
      y++;
    }while(!sorted);
  }
  
  public static void Swap<T>(ref T obj1, ref T obj2){
    T result = obj1;
    obj1 = obj2;
    obj2 = result;
  }
}
```
---  
- L02: Events  
```cs
delegate void MyDelegate();
class Menu{
  public event MyDelegate PressEnter;
  List<string> menuItems;
  ConsoleColor hBackColor;
  ConsoleColor hForeColor;
  ConsoleColor backColor;
  ConsoleColor foreColor;
  int x;
  int y;
  int current;
  //Constructor
  public Menu(List<string> menuItems,ConsoleColor hBackColor, ConsoleColor hForeColor, ConsoleColor backColor, ConsoleColor foreColor, int x, int y){
    PressEnter = OnPressEnter;
    this.menuItems = menuItems;
    this.hBackColor = hBackColor;
    this.hForeColor = hForeColor;
    this.backColor = backColor;
    this.foreColor = foreColor;
    this.x = x;
    this.y = y;
    this.current = 0;
  }
  public Menu(List<string> menuItems,ConsoleColor hBackColor, ConsoleColor hForeColor, int x, int y):this(menuItems, hBackColor, hForeColor, ConsoleColor.Black, ConsoleColor.White, x, y){}
  
  private void Draw(){
    for(int i = 0; i < menuItems.Count; i++){
      Console.SetCursorPosition(x, y+i);
      if(i == current){
        Console.BackgroundColor = hBackColor;
        Console.ForegroundColor = hForeColor;
      }
      else{
        Console.BackgroundColor = BackColor;
        Console.ForegroundColor = ForeColor;
      }
      Console.Write(menuItems[i]);
    }
    Console.ResetColor();
  }
  public void Show(){
    bool flag = true;
    ConsoleKeyInfo cki;
    do{
      Draw();
      cki = Console.ReadKey(true);
      switch(cki.Key){
        case ConsoleKey.UpArrow:
          current--;
          if(current < 0){current = menuItems.Count - 1;}
          break;
        case ConsoleKey.DownArrow:
          current++;
          if(current == menuItems.Count){current = 0;}
          break;
        case ConsoleKey.Enter:
          PressEnter();
          break;
        case Console.Escape:
          flag = false;
          break;
        case ConsoleKey.Home:
          current = 0;
          break;
        case ConsoleKey.End:
          current = menuItems.Count - 1;
          break;
      }
    }while(flag);
  }
  
  public void OnPressEnter(){
    
  }
}
```
---  
- L03: Delegate Standard  
```cs
class MyEventArgs:EventArgs{
  int current;
  bool isExit;
  
  public int Current{
    get { return current; }
    set { current = value; }
  }
  
  public bool IsExit{
    get { return isExit; }
    set { isExit = value; }
  }
  
  public MyEventArgs(int current){
    this.current = current;
    isExit = false;
  }
}

delegate void MyDelegate(object sender, MyEventArgs e);

class Menu{
  public event MyDelegate PressEnter;
  List<string> menuItems;
  ConsoleColor hBackColor;
  ConsoleColor hForeColor;
  ConsoleColor backColor;
  ConsoleColor foreColor;
  int x;
  int y;
  int current;
  //Constructor
  public Menu(List<string> menuItems,ConsoleColor hBackColor, ConsoleColor hForeColor, ConsoleColor backColor, ConsoleColor foreColor, int x, int y){
    PressEnter = OnPressEnter;
    this.menuItems = menuItems;
    this.hBackColor = hBackColor;
    this.hForeColor = hForeColor;
    this.backColor = backColor;
    this.foreColor = foreColor;
    this.x = x;
    this.y = y;
    this.current = 0;
  }
  public Menu(List<string> menuItems,ConsoleColor hBackColor, ConsoleColor hForeColor, int x, int y):this(menuItems, hBackColor, hForeColor, ConsoleColor.Black, ConsoleColor.White, x, y){}
  
  private void Draw(){
    for(int i = 0; i < menuItems.Count; i++){
      Console.SetCursorPosition(x, y+i);
      if(i == current){
        Console.BackgroundColor = hBackColor;
        Console.ForegroundColor = hForeColor;
      }
      else{
        Console.BackgroundColor = BackColor;
        Console.ForegroundColor = ForeColor;
      }
      Console.Write(menuItems[i]);
    }
    Console.ResetColor();
  }
  public void Show(){
    ConsoleKeyInfo cki;
    MyEventArgs abc = new MyEventArgs(current);
    do{
      Draw();
      cki = Console.ReadKey(true);
      switch(cki.Key){
        case ConsoleKey.UpArrow:
          current--;
          if(current < 0){current = menuItems.Count - 1;}
          break;
        case ConsoleKey.DownArrow:
          current++;
          if(current == menuItems.Count){current = 0;}
          break;
        case ConsoleKey.Enter:
          abc = new MyEventArgs(current);
          PressEnter(this, abc);
          break;
        case Console.Escape:
          flag = false;
          break;
        case ConsoleKey.Home:
          current = 0;
          break;
        case ConsoleKey.End:
          current = menuItems.Count - 1;
          break;
      }
    }while(!abc.IsExit);
  }
  
  public void OnPressEnter(object sender, MyEventArgs e){
    
  }
}

```
---  
- L04: Event Handlers  
```cs
class MyEventArgs:EventArgs{
  int current;
  bool isExit;
  
  public int Current{
    get { return current; }
    set { current = value; }
  }
  
  public bool IsExit{
    get { return isExit; }
    set { isExit = value; }
  }
  
  public MyEventArgs(int current){
    this.current = current;
    isExit = false;
  }
}

class Menu{
  public event EventHandler<MyEventArgs> PressEnter;
  List<string> menuItems;
  ConsoleColor hBackColor;
  ConsoleColor hForeColor;
  ConsoleColor backColor;
  ConsoleColor foreColor;
  int x;
  int y;
  int current;
  //Constructor
  public Menu(List<string> menuItems,ConsoleColor hBackColor, ConsoleColor hForeColor, ConsoleColor backColor, ConsoleColor foreColor, int x, int y){
    PressEnter = OnPressEnter;
    this.menuItems = menuItems;
    this.hBackColor = hBackColor;
    this.hForeColor = hForeColor;
    this.backColor = backColor;
    this.foreColor = foreColor;
    this.x = x;
    this.y = y;
    this.current = 0;
  }
  public Menu(List<string> menuItems,ConsoleColor hBackColor, ConsoleColor hForeColor, int x, int y):this(menuItems, hBackColor, hForeColor, ConsoleColor.Black, ConsoleColor.White, x, y){}
  
  private void Draw(){
    for(int i = 0; i < menuItems.Count; i++){
      Console.SetCursorPosition(x, y+i);
      if(i == current){
        Console.BackgroundColor = hBackColor;
        Console.ForegroundColor = hForeColor;
      }
      else{
        Console.BackgroundColor = BackColor;
        Console.ForegroundColor = ForeColor;
      }
      Console.Write(menuItems[i]);
    }
    Console.ResetColor();
  }
  public void Show(){
    ConsoleKeyInfo cki;
    MyEventArgs abc = new MyEventArgs(current);
    do{
      Draw();
      cki = Console.ReadKey(true);
      switch(cki.Key){
        case ConsoleKey.UpArrow:
          current--;
          if(current < 0){current = menuItems.Count - 1;}
          break;
        case ConsoleKey.DownArrow:
          current++;
          if(current == menuItems.Count){current = 0;}
          break;
        case ConsoleKey.Enter:
          abc = new MyEventArgs(current);
          PressEnter(this, abc);
          break;
        case Console.Escape:
          flag = false;
          break;
        case ConsoleKey.Home:
          current = 0;
          break;
        case ConsoleKey.End:
          current = menuItems.Count - 1;
          break;
      }
    }while(!abc.IsExit);
  }
  
  public void OnPressEnter(object sender, MyEventArgs e){
    
  }
}  
```  
---  
- L05: Anonymous Functions and Lambda Expressions  
```cs
/// Anonymous Functions
public delegate double Calc(double x, double y);
public class EntryPoint{
  static void Main(){
    Calc abc = delegate(double o, double p){
      return o / p ;
    }
    double u = abc(4, 3);
  }
}
/// Lambda Expressions
public delegate double Calc(double x, double y);
public class EntryPoint{
  static void Main(){
    Calc abc = (o, p) => o / p;
    double u = abc(4, 3);
  }
}
```
---  
- L06: Declarative / Imperative Programming  
> Attributes in c#  
---  
- L07: Enum / Attributes
> obsolute  
> try{}catch{}finally{}  
---   
