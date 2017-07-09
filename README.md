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
- L03: Model Connection
> Connected/Disconnected Model.  
```cs
  ...
  /// Connected Model
  // After connecting to a Database Source this line forms with the approiate properties.  
  string conStr = "Data Source = .; Initial Catalog = Test; ";
  // make a SQL connection from the defined conStr
  SqlConnection con = new SqlConnection(conStr);
  // make a SQL command after the connection
  SqlCommand cmd = new SqlCommand("select * from country");
  // Open The Connection
  con.Open();
  // Retrieve data from database
  SqlDataReader reader = cmd.ExecuteReader();
  // retrieve all records
  List<string> sRows = new List<string>();
  while(reader.Read()){ 
    sRows.Add(reader["Name"].toString());
  }
  // Print rows
  for(int i = 0; 0 < sRows.Count; i++){
    Console.WriteLine(sRows[i]);
  }
  //do not forget to close the connection
  con.Close();
  /// Disconnected Model
  string conStr = "Data Source = .; Initial Catalog = Test; Integrated Security = True";
  SqlConnection con = new SqlConnection(conStr);
  SqlCommand cmd = new SqlCommand("select * from country");
  // make a SQL Adapter
  SqlDataAdapter adpt = new SqlDataAdapter(cmd);
  // create data table to work on
  DataTable dt = new DataTable();
  // fill the adpt from the select cmd
  adpt.Fill(dt);
  // Print Rows
  for(int i = 0; 0 < dt.Rows.Count; i++){
    Console.WriteLine(dt.Rows[i]["Name"]);
  }
```  
---   
- L04: Insert and Update  
```cs
/// Example Form with two drop down list.
/// First with Country Name.
/// Second with Cities in the selected country.
void Form1_Load(object sender, EventArgs e){
  //Connection string
  string conStr = "Data Source = .; Initial Catalog = Test; Integrated Security = True";
  // Data Adapter
  SqlDataAdapter adpt = new SqlDataAdapter("select * from country", conStr);
  // create data table and fill it from database
  DataTable dt = new DataTable();
  adpt.Fill(dt);
  // configure drop down list
  ddlCountry.DisplayeMember = "Name";
  ddlCountry.ValueMember = "Id";
  ddlCountry.DataSource = dt;
  // Show cities of the country
  FillCities(int(ddlCountry.SelectedValue));
}
private void ddlCountry_SelectedIndexChanged(object sender, EventArgs e){
  FillCities(int(ddlCountry.SelectedValue));
}
private void FillCities(int countryId){
  //Connection string
  string conStr = "Data Source = .; Initial Catalog = Test; Integrated Security = True";
  // Data Adapter
  SqlDataAdapter adpt = new SqlDataAdapter(string.Format("select * from city where fk_CountryId = {0}", countryId), conStr);
  // create data table and fill it from database
  DataTable dt = new DataTable();
  adpt.Fill(dt);
  // configure drop down list
  ddlCity.DisplayeMember = "Name";
  ddlCity.ValueMember = "Id";
  ddlCity.DataSource = dt;
}
```
> - Inserting and Deleteing  
```cs
/// Example: Form with a drop down list and a button
/// select a city from the drop down list after clicking the button the city is deleted from the list.
private void Form2_Load(object sender, EventArgs e){
  FillCities();
}

private void FillCities(){
  //Connection string
  string conStr = "Data Source = .; Initial Catalog = Test; Integrated Security = True";
  // Data Adapter
  SqlDataAdapter adpt = new SqlDataAdapter("select * from city", conStr);
  // create data table and fill it from database
  DataTable dt = new DataTable();
  adpt.Fill(dt);
  // configure drop down list
  ddlCity.DisplayeMember = "Name";
  ddlCity.ValueMember = "Id";
  ddlCity.DataSource = dt;
}

private void button1_Click(object sender, EventArgs e){
  //Connection string
  string conStr = "Data Source = .; Initial Catalog = Test; Integrated Security = True";
  // Connection
  SqlConnection con = new SqlConnection(conStr);
  // Command
  SqlCommand cmd = new SqlCommand(string.Format("delete from city where id = {0}", ddlCity.SelectedValue), con);
  // Open Connection
  con.Open();
  // Excute query 
  int noOfRowsAffected = cmd.ExecuteNonQuery();
  // close connection
  con.Close();
  if(noOfRowsAffected > 0){
    MessageBox.Show("Data Deleted");
  }
  else{
    MessageBox.Show("Error");
  }
  // update the drop down list
  FillCities();
}
```
---   
