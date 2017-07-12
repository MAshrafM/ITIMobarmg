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