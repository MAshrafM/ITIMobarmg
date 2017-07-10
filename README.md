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
- L05: ADO.NET  
> Three Tiers Layers
```cs
/// Data Base Layer (DBL)
static class DBL{
  static string conStr;
  // static initializer
  static DBL(){
    conStr = "Data Source = .; Initial Catalog = Test; Integrated Security = True";
  }
  // Dynamic excute queries
  public static DataTable ExcuteQuery(string selectCommand){
    // init Adapter
    SqlDataAdapter adpt = new SqlDataAdapter(selectCommand, conStr);
    // return result
    DataTable result = new DataTable();
    // fill adapter
    adpt.Fill(result);
    return result;
  }
  // To insert/update/delete
  public static int ExcuteNonQuery(string dmlCommand){
    int result;
    SqlConnection con = new SqlConnection(conStr);
    SqlCommand cmd = new SqlCommand(dmlCommand, con);
    con.Open();
    result = cmd.ExcuteNonQuery();
    con.Close();
    return result;
  }
  public static object ExcuteScaler(string selectCommand){
    object result = null;
    DataTable dt = ExcuteQuery(selectCommand);
    if(dt.Rows.Count > 0){
      result = dt.Rows[0][0];
    }
    return result;
  }
}
/// Data Access Layer (DAL)
static class CountryDAL{
  // Select All
  public static DataTable GetAll(){
    return DBL.ExcuteQuery("Select * from Country");
  }
  // Select One
  public static DataRow DataRow GetById(int id){
    DataRow result = null;
    DataTable dt = DBL.ExcuteQuery(string.Format("Select * from Country where id = {0}", id));
    if(dt.Rows.Count > 0){
      result = dt.Rows[0];
    }
    return result
  }
  // Delete
  public static bool Delete(int id){
    return DBL.ExcuteNonQuery(string.Format("Delete * from Country where id = {0}", id)) > 0;
  }
  // Update
  public static bool Update(int id, string name){
    return DBL.ExcuteNonQuery(string.Format("update Country set name = '{0}' where id = {1}", name, id)) > 0;
  }
  // Insert
  public static bool Add(string name){
    return DBL.ExcuteNonQuery(string.Format("insert into Country values('{0}')", name)) > 0;
  }
}
static class CityDAL{
  // Select All
  public static DataTable GetAll(){
    return DBL.ExcuteQuery("Select * from City");
  }
  // Select One
  public static DataRow DataRow GetById(int id){
    DataRow result = null;
    DataTable dt = DBL.ExcuteQuery(string.Format("Select * from City where id = {0}", id));
    if(dt.Rows.Count > 0){
      result = dt.Rows[0];
    }
    return result
  }
    // Get All by Country Id
  public static DataTable GetByCountryId(int countryId){
    return DBL.ExcuteQuery(string.Format("select * from City where fk_CountryId = {0}", countryId));
  }
  // Delete
  public static bool Delete(int id){
    return DBL.ExcuteNonQuery(string.Format("Delete * from City where id = {0}", id)) > 0;
  }
  // Update
  public static bool Update(int id, string name, int countryId){
    return DBL.ExcuteNonQuery(string.Format("update City set name = '{0}', fk_CountryId = {1} where id = {2}", name, countryId, id)) > 0;
  }
  // Insert
  public static bool Add(string name, int countryId){
    return DBL.ExcuteNonQuery(string.Format("insert into City values('{0}', {1})", name, countryId)) > 0;
  }  
}
/// Form using the DB Layer
void Form1_Load(object sender, EventArgs e){ 
  // configure drop down list
  ddlCountry.DisplayeMember = "Name";
  ddlCountry.ValueMember = "Id";
  ddlCountry.DataSource = CountryDAL.GetAll();
  // Show cities of the country
  FillCities(int(ddlCountry.SelectedValue));
}

/// Function with DB Layer
private void FillCities(countryId){
  // configure drop down list
  ddlCity.DisplayeMember = "Name";
  ddlCity.ValueMember = "Id";
  ddlCity.DataSource = CityDAL.GetByCountryId(countryId);
}
/******* Form2 *******/
/// Using DBL
private void Form2_Load(object sender, EventArgs e){
  FillCities();
}

private void FillCities(){
  // configure drop down list
  ddlCity.DisplayeMember = "Name";
  ddlCity.ValueMember = "Id";
  ddlCity.DataSource = CityDAL.GetAll();
}

private void button1_Click(object sender, EventArgs e){
  bool i = CityDAL.Delete((int)ddlCity.SelectedValue);
}
```
> Six Tier Layer  
> Object Relational Model (ORM)
```cs
/// Entity Layer
sealed class Country{
  int id;
  string name;
  CityCollection cities; 
  // properties
  public int Id{
    get{ return id; }
    set{ id = value}
  }
  public string Name{
    get { return name; }
    set { name = value; } 
  }
  public CityCollection Cities{
    get { return cities; }
    set { cities = value; }
  }
  // Constructors
  public Country(int id, string name, CityCollection cities){
    this.id = id;
    this.name = name;
    this.cities = cities;
  }
  public Country(int id, string name, params City[] citiesCol){
    this.id = id;
    this.name = name;
    for(int i = 0; i  cities.Length; i++){
      this.cities.Add(cities[i]);
    }
  }
  public Country(int id, string name):this(id, name, citiesCol:null){}
  public Country(string name):this(0, name, citiesCol:null){}
  public Country(Country c):this(c.id, c.name, c.cities){}
  // Clone
  public Country Clone(){
    return new Country(this);
  }
  // Override
  public override string ToString(){
    return base.ToString();
  }
  public override bool Equals(object obj){
    return base.Equals(obj);
  }
}
sealed class City{
  int id;
  string name;
  Country country;
  //Properties
  public int Id{
    get{ return id; }
    set{ id = value}
  }
  public string Name{
    get { return name; }
    set { name = value; } 
  }
  public Country Country{
    get { return country; }
    set { country = value; }
  }
  // Constructors
  public City(int id, string name, Country country){
    this.id = id;
    this.name = name;
    this.country = country;
  }
  public City(int id, string name):this(id, name, null){}
  public City(string name):this(0, name, null){}
  public City(City c):this(c.id, c.name, null){}
  // Clone
  public City Clone(){
    return new City(this);
  }
  // Override
  public override string ToString(){
    return base.ToString();
  }
  public override bool Equals(object obj){
    return base.Equals(obj);
  }
}
/// Collections Layer
class CityCollection:List<City>{}
class CountryCollection:List<Country>{}
```
--- 