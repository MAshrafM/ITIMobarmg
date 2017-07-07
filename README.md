# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)  
  
## Windows Form and ADO.NET  
  
- L01: Introduction 
```cs 
...
using System.Windows.Forms;
using System.Drawing;
namespace MyForms{
  class MyForm:Form{
    Button b;
    TextBox t;
    
    public MyForm()::base(){
      Text = "Hi"; // this.Text change name of form.
      t = new TextBox();
      // setting a button
      b = new Button(); // create a point object
      b.Text = "Hi"; // text property
      // need System Drawing .dll to use Point class
      // Point Class takes int as px
      b.Location = new Point(100, 100);
      Controls.Add(b); // add button control to form
      Controls.Add(t); // add textbox to form
    }
  }
}
```
> Instead of Code with VS You can Drag and Drop  
> New Windows Form Project  
> Properties  
> Windows Form is not supported anymore it got deprecated for WPF Windows Presetation Foundation, but we have it for backward compatability.  
---