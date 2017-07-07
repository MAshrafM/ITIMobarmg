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
- L2: Controls  
```cs
// Simple example
// label Name {lblName}, Textbox {txtName}, OK button {btnOk}
// when click button show the input name in the txt box
...
// Form1
private void btnOk_Click(object sender, EventArgs e){
  this.Hide(); // to hide the first form without deleteing it nor its object.
  Form2 f2 = new Form2(); // create 2nd form object after clicking the first one
  f2.lblName.Text = string.Format("Welcome {0}", txtName.Text); // set output name in the 2nd form from the input textbox
  f2.ShowDialog(); // show form2
  txtName.Text = ""; // clear text input
  this.Show(); // show form1
  
}
//Form2
public Label lblName{
  get {return lblName;}
}
private void Form2_Load(object sender, EventArgs e){
  
}
```
> MenuStrip  
> MessageBox  
> ToolStrip  
> ContextMenuStrip  
> OpenFileDialog  
---  