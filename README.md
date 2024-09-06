using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;

namespace RestaurantMS
{
    public partial class Food : Form
    {
        public Food()
        {
            InitializeComponent();
        }

        private void btnSave_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
         using(   MySqlConnection con = new MySqlConnection(connectionString)) {
            try
            {
                con.Open();
                MySqlCommand cmd = new MySqlCommand("Insert into tab2 (foodId,foodname,price,Quantity )VALUES(@foodId,@foodname,@price,@quantity)", con);
                cmd.Parameters.AddWithValue("@foodId", int.Parse(textBox1.Text));
                cmd.Parameters.AddWithValue("@foodName", textBox2.Text);
                cmd.Parameters.AddWithValue("@Price", textBox3.Text);
                cmd.Parameters.AddWithValue("@Quantity", textBox4.Text);
                cmd.ExecuteNonQuery();

                MessageBox.Show("Record Saved Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

            }
            catch (Exception ex)
            {
                MessageBox.Show("Error: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        } }

        private void btnAdd_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();

                    MySqlCommand cmd = new MySqlCommand("SELECT * FROM tab2", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;

                    MessageBox.Show("Data Added Successfully", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while fetching data: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }

        private void btnNew_Click(object sender, EventArgs e)
        {
            textBox1.Text = "";
            textBox2.Text = "";
            textBox3.Text = "";
            textBox4.Text = "";
            
        }

        private void btnUpdate_Click(object sender, EventArgs e)
        {

            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    if (string.IsNullOrWhiteSpace(textBox1.Text) || string.IsNullOrWhiteSpace(textBox2.Text) ||
    string.IsNullOrWhiteSpace(textBox3.Text) || string.IsNullOrWhiteSpace(textBox4.Text))
                    {
                        MessageBox.Show("Please fill in all fields before updating.", "Validation Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        return;
                    }
                    MySqlCommand cmd = new MySqlCommand("Update tab2 set foodName=@FoodName,Price=@Price,Quantity=@Quantity WHERE foodId=@FoodId", con);
                    cmd.Parameters.AddWithValue("@foodId", int.Parse(textBox1.Text));
                    cmd.Parameters.AddWithValue("@foodName", textBox2.Text);
                    cmd.Parameters.AddWithValue("@Price", textBox3.Text);
                    cmd.Parameters.AddWithValue("@Quantity", textBox4.Text);
                    cmd.ExecuteNonQuery();
                 
                    MessageBox.Show("Record Updated Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while updating the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }

            }
        }

        private void btnDelete_Click(object sender, EventArgs e)
        {

            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {

                    con.Open();
                    if (string.IsNullOrWhiteSpace(textBox1.Text) || string.IsNullOrWhiteSpace(textBox2.Text) ||
    string.IsNullOrWhiteSpace(textBox3.Text) || string.IsNullOrWhiteSpace(textBox4.Text))
                    {
                        MessageBox.Show("Please fill in all fields before updating.", "Validation Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        return;
                    }
                    MySqlCommand cmd = new MySqlCommand("delete FROM tab2 where foodId=@FoodId", con);
                    cmd.Parameters.AddWithValue("@foodId", int.Parse(textBox1.Text));

                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Deleted Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }

        private void btnDisplay_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Select * from tab2 ", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;
                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        
        }

        private void Food_Load(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("SELECT * FROM tab2", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;
                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while fetching data: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }


    }
}
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;

namespace RestaurantMS
{
    public partial class Payment : Form
    {
        public Payment()
        {
            InitializeComponent();
        }

        private void Payment_Load(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Select * from payment ", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;
                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }

    
            private void btnSave_Click(object sender, EventArgs e)
            {
                string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
                using (MySqlConnection con = new MySqlConnection(connectionString))
                {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Insert into payment (PId,PName,Food1,Food2,PaymentMethod,Amount ) VALUES (@PId,@PName,@Food1,@Food2,@PaymentMethod,@Amount)", con);
                    cmd.Parameters.AddWithValue("@PId", int.Parse(textBox1.Text));
                    cmd.Parameters.AddWithValue("@PName", textBox2.Text);
                    cmd.Parameters.AddWithValue("@Food1", textBox3.Text);
                    cmd.Parameters.AddWithValue("@Food2", textBox4.Text);
                    cmd.Parameters.AddWithValue("@PaymentMethod", textBox5.Text);
                    cmd.Parameters.AddWithValue("@Amount", textBox6.Text);
                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Saved Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("Error: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }

            }

        private void btnAdd_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();

                    MySqlCommand cmd = new MySqlCommand("SELECT * FROM payment", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;

                    MessageBox.Show("Data Added Successfully", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while fetching data: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }

            }
        }

        private void btnNew_Click(object sender, EventArgs e)
        {

            textBox1.Text = "";
            textBox2.Text = "";
            textBox3.Text = "";
            textBox4.Text = "";
            textBox5.Text = "";
            textBox6.Text = "";

        }

        private void btnUpdate_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    if (string.IsNullOrWhiteSpace(textBox1.Text) || string.IsNullOrWhiteSpace(textBox2.Text) ||
    string.IsNullOrWhiteSpace(textBox3.Text) || string.IsNullOrWhiteSpace(textBox4.Text))
                    {
                        MessageBox.Show("Please fill in all fields before updating.", "Validation Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        return;
                    }
                    MySqlCommand cmd = new MySqlCommand("Update payment set PName=@PName,Food1=@Food1,Food2=@Food2,PaymentMethod=@PaymentMethod,Amount=@Amount WHERE PId=@PId", con);
                    cmd.Parameters.AddWithValue("@PId", int.Parse(textBox1.Text));
                    cmd.Parameters.AddWithValue("@PName", textBox2.Text);
                    cmd.Parameters.AddWithValue("@Food1", textBox3.Text);
                    cmd.Parameters.AddWithValue("@Food2", textBox4.Text);
                    cmd.Parameters.AddWithValue("@PaymentMethod", textBox5.Text);
                    cmd.Parameters.AddWithValue("@Amount", textBox6.Text);
                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Updated Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while updating the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            }

        private void btnDelete_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {

                    con.Open();
                    if (string.IsNullOrWhiteSpace(textBox1.Text) || string.IsNullOrWhiteSpace(textBox2.Text) ||
    string.IsNullOrWhiteSpace(textBox3.Text) || string.IsNullOrWhiteSpace(textBox4.Text))
                    {
                        MessageBox.Show("Please fill in all fields before updating.", "Validation Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        return;
                    }
                    MySqlCommand cmd = new MySqlCommand("delete FROM payment where PId=@PId", con);
                    cmd.Parameters.AddWithValue("@PId", int.Parse(textBox1.Text));

                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Deleted Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            }

        private void button1_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Select * from payment ", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;
                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            }
    }
    }
    
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;

namespace RestaurantMS
{
    public partial class Order : Form
    {
        private const string V = "MM/dd/yyyy";

        public Order()
        {
            InitializeComponent();
        }

        private void label6_Click(object sender, EventArgs e)
        {

        }

        private void dateTimePicker1_ValueChanged(object sender, EventArgs e)
        {
            dateTimePicker1.CustomFormat = "MM/dd/yyyy";
        }
        private void dateTimePicker_KeyDown(object sender, KeyEventArgs e)
        {
            if (e.KeyCode == Keys.Enter)
            {
                dateTimePicker1.CustomFormat = "";

            }
        }

        private void btnSave_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Insert into orders (OrderId,Ordername,Food1,Food2,Date ) VALUES (@OrderId,@Ordername,@Food1,@Food2,@Date)", con);
                    cmd.Parameters.AddWithValue("@OrderId", int.Parse(textBox1.Text));
                    cmd.Parameters.AddWithValue("@OrderName", textBox2.Text);
                    cmd.Parameters.AddWithValue("@Food1", textBox3.Text);
                    cmd.Parameters.AddWithValue("@Food2", textBox4.Text);
                    MySqlParameter dateParam = new MySqlParameter("@Date", MySqlDbType.Date);
                    dateParam.Value = dateTimePicker1.Value.Date; // Ensure it's in the correct format
                    cmd.Parameters.Add(dateParam);

                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Saved Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("Error: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }

        }

        private void btnAdd_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();

                    MySqlCommand cmd = new MySqlCommand("SELECT * FROM orders", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;

                    MessageBox.Show("Data Added Successfully", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while fetching data: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }


            }
        }

        private void btnNew_Click(object sender, EventArgs e)
        {
            textBox1.Text = "";
            textBox2.Text = "";
            textBox3.Text = "";
            textBox4.Text = "";
            
          
          
           
        }

        private void btnUpdate_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    if (string.IsNullOrWhiteSpace(textBox1.Text) || string.IsNullOrWhiteSpace(textBox2.Text) ||
    string.IsNullOrWhiteSpace(textBox3.Text) || string.IsNullOrWhiteSpace(textBox4.Text))
                    {
                        MessageBox.Show("Please fill in all fields before updating.", "Validation Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        return;
                    }
                    MySqlCommand cmd = new MySqlCommand("Update orders set OrderName=@OrderName,Food1=@Food1,Food2=@Food2,Date=@Date WHERE OrderId=@OrderId", con);
                    cmd.Parameters.AddWithValue("@OrderId", int.Parse(textBox1.Text));
                    cmd.Parameters.AddWithValue("@OrderName", textBox2.Text);
                    cmd.Parameters.AddWithValue("@Food1", textBox3.Text);
                    cmd.Parameters.AddWithValue("@Food2", textBox4.Text);
           
                    MySqlParameter dateParam = new MySqlParameter("@Date", MySqlDbType.Date);
                    dateParam.Value = dateTimePicker1.Value.Date; // Ensure it's in the correct format
                    cmd.Parameters.Add(dateParam);
                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Updated Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while updating the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            }

        private void btnDelete_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {

                    con.Open();
                    if (string.IsNullOrWhiteSpace(textBox1.Text) || string.IsNullOrWhiteSpace(textBox2.Text) ||
    string.IsNullOrWhiteSpace(textBox3.Text) || string.IsNullOrWhiteSpace(textBox4.Text))
                    {
                        MessageBox.Show("Please fill in all fields before updating.", "Validation Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                        return;
                    }
                    MySqlCommand cmd = new MySqlCommand("delete FROM orders where OrderId=@OrderId", con);
                    cmd.Parameters.AddWithValue("@OrderId", int.Parse(textBox1.Text));

                    cmd.ExecuteNonQuery();

                    MessageBox.Show("Record Deleted Successfuly", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            }

        private void btnDisplay_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Select * from orders ", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;
                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            }

        private void Order_Load(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            using (MySqlConnection con = new MySqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    MySqlCommand cmd = new MySqlCommand("Select * from orders ", con);
                    MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                    DataTable dt = new DataTable();
                    da.Fill(dt);
                    dataGridView1.DataSource = dt;
                }
                catch (Exception ex)
                {
                    MessageBox.Show("An error occurred while deleting the record: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }
    }
    }
    using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace RestaurantMS
{
    public partial class Main : Form
    {
        public Main()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            Food fd = new Food();
            fd.Show();
        }

        private void button2_Click(object sender, EventArgs e)
        {
            Customer cs= new Customer();
            cs.Show();
        }

        private void button3_Click(object sender, EventArgs e)
        {
            Order order = new Order();
            order.Show();
        }

        private void button4_Click(object sender, EventArgs e)
        {
            Payment p= new Payment();
            p.Show();
        }
    }
}
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;


namespace RestaurantMS
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            string connectionString = "Server=localhost;Port=3306;Database=inn;User=root;Password=Barober@27";
            MySqlConnection con = new MySqlConnection(connectionString);

            try
            {
                con.Open();
                string username = textBox1.Text;
                string password = textBox2.Text;

                string query = "SELECT Username, Password FROM tab WHERE Username = @username AND Password = @password";
                MySqlCommand cmd = new MySqlCommand(query, con);
                cmd.Parameters.AddWithValue("@username", username);
                cmd.Parameters.AddWithValue("@password", password);

                MySqlDataAdapter da = new MySqlDataAdapter(cmd);
                DataTable dt = new DataTable();
                da.Fill(dt);

                if (dt.Rows.Count > 0) { Main m = new Main();
                    m.Show();
                }
                else { MessageBox.Show("Wrong Username or Password"); }
            }
            catch (Exception ex)
            {
                MessageBox.Show("Connection Failed: " + ex.Message);
            }
        }


    }
}

            
    
        





        
    

