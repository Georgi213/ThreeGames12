


Разработки для Matching game.


Перезапускать форму или выходит из нее в зависимости от ответа .

void restartGame() 
            {
                if (MessageBox.Show($"Vead: {score.ToString()}\nAeg sekundid: {tik.ToString()}!\nKas soovite uuesti mängida?", "Tulemus!", MessageBoxButtons.YesNo) == DialogResult.Yes)
                {

                    Application.Restart();
                    Environment.Exit(0);
                }
                else
                {
                    Application.Exit();

                }

            }


Сделать 3 сложности. Легкая,нормальная и сложная
  difficult = new Label 
            {
                Text = "Valige raskusaste",
                Location = new Point(110, 100),
                Size = new Size(400, 100),
                Font = new Font("Arial", 28, FontStyle.Bold)
            };
            this.Controls.Add(difficult);
            string[] buttonstext = { "Lihtne", "Tavaline", "Raske" }; 
            int y = 200;
            for (int i = 0; i < buttonstext.Length; i++) 
            {

                Button button = new Button
                {
                    Text = buttonstext[i],
                    Location = new Point(210, y),
                    Size = new Size(100, 80)
                };
                button.Click += Button_Click; 
                this.Controls.Add(button);
                y += 100;
            }

 List<string> icons = new List<string>()
        {
            "!", "!", "N", "N", "r", "r",
            "b", "b", "v", "v", "~", "~",
        };
        List<string> icons_2 = new List<string>()
        {
            "!", "!", "N", "N", ",", ",", "k", "k",
            "b", "b", "v", "v", "w", "w", "z", "z"
        };
        List<string> icons_3 = new List<string>()
        {
            "!", "!", "N", "N", ",", ",", "k", "k", "`", "`",
            "b", "b", "v", "v", "w", "w", "z", "z", "f", "f"
        };

if (nupp_sender.Text == "Lihtne")
            {

                new Matching(4, 3, icons, tableLayoutPanel);

            }
            else if (nupp_sender.Text == "Tavaline")
            {

                new Matching(4, 4, icons_2, tableLayoutPanel);

            }
            else if (nupp_sender.Text == "Raske")
            {

                new Matching(5, 4, icons_3, tableLayoutPanel);
            }


Разработки для Matquiz.

Заменять старые примеры на новые. 

 public void NewExamples_Click(object sender, EventArgs e) //Meetod loob vormi uute väärtustega uuesti
        {
            matem = new Mathematicquiz(this.x, this.y, this.difficult);
            matem.Show();
        }
Выводить правильные ответы нажимая на кнопку проверить

  private void showTrueAns(object sender, EventArgs e) 
        {
            int[] ans = new int[4];
            ans[0] = intnum[0] + intnum2[0];
            ans[1] = intnum[1] - intnum2[1];
            ans[2] = intnum[2] * intnum2[2];
            ans[3] = intnum[3] / intnum2[3];
            for (int i = 0; i < 4; i++)
            {
                Label l = new Label { Text = ans[i].ToString() };
                tableLayoutPanel.Controls.Add(l, 6, i);
            }
            showAns.Enabled = false;

        }

Возможность менять сложность примеров при выьоре

 Label difficult = new Label //Sildi loomine
            {
                Text = "Valige raskusaste",
                Location = new Point(225, 15),
                Size = new Size(200, 20),
                Font = new Font("Arial", 10, FontStyle.Bold)
            };
            this.Controls.Add(difficult);
            string[] buttonstext = { "Lihtne", "Tavaline", "Raske" }; 
            int x = 170;
            for (int i = 0; i < buttonstext.Length; i++) //Nuppude loomine
            {

                Button buttons = new Button
                {
                    Text = buttonstext[i],
                    Location = new Point(x, 50),
                    Size = new Size(80, 40)
                };
                buttons.Click += difficultChoice; 
                this.Controls.Add(buttons);
                x += 80;
            }


 public void difficultChoice(object sender, EventArgs e) //Метод изменяет сложность примеров
        {
            this.Controls.Clear();
            Button nupp_sender = (Button)sender;
            if (nupp_sender.Text == "Lihtne")
            {
                x = 20;
                y = 2;
                difficult = "Lihtne";

            }
            else if (nupp_sender.Text == "Tavaline")
            {
                x = 30;
                y = 3;
                difficult = "Tavaline";
            }
            else if (nupp_sender.Text == "Raske")
            {
                x = 50;
                y = 5;
                difficult = "Raske";
            }
            matem = new Mathematicquiz(x, y, difficult);
            matem.Show();
        }


Разработки для Picture viewer.

Нажимая по кнопку меняет картинку на случайную из папки с картинками. 

else if (nupp_sender.Text == "Juhuslik pilt")
            {

                pictureBox1.Load(files[rnd.Next(0, files.Count)]);
                Bitmap finalImg = new Bitmap(pictureBox1.Image, pictureBox1.Width, pictureBox1.Height);
                pictureBox1.Image = finalImg;
                pictureBox1.Show();
            }

Возможность добавлять вашу картинку в папку с картинками.

 else if (nupp_sender.Text == "Teie fail kaustas") 
            {
                if (openFileDialog1.ShowDialog() == DialogResult.OK)
                {
                    string sourceFile = openFileDialog1.SafeFileName;
                    string destinationFile = @"..\..\..\randompic\" + sourceFile;
                    File.Move(openFileDialog1.FileName, destinationFile);
                

Создание регистрационной и логин формы

public partial class Login : Form
    {
        SqlCommand cmd;
        SqlConnection cn;
        SqlDataReader dr;
        //
        public Login()
        {
            InitializeComponent();
        }

        private void Login_Load(object sender, EventArgs e)
        {
            cn = new SqlConnection(@"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=C:\Users\User\Desktop\Registration3games-main\3 games\RegistrationAndLogin\Database.mdf;Integrated Security=True");
            cn.Open();
        }

        private void Btnregister_Click(object sender, EventArgs e)
        {
            this.Hide();
            Registration registration = new Registration();
            registration.ShowDialog();
        }

        private void BtnLogin_Click(object sender, EventArgs e)
        {
            if (txtpassword.Text != string.Empty || txtusername.Text != string.Empty || txtemail.Text != string.Empty)
            {

                cmd = new SqlCommand("select * from LoginTable where username='" + txtusername.Text + "' and email='" + txtemail.Text + "' and password='" +txtpassword.Text+"'", cn);
                dr = cmd.ExecuteReader();
                if (dr.Read())
                {
                    dr.Close();
                    this.Hide();
                    Starting starting = new Starting();
                    starting.ShowDialog();
                }
                else
                {
                    dr.Close();
                    MessageBox.Show("No Account avilable with this username and password ", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }

            }
            else
            {
                MessageBox.Show("Please enter value in all field.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }


 public partial class Registration : Form
    {

        SqlCommand cmd;
        SqlConnection cn;
        SqlDataReader dr;

        public Registration()
        {
            InitializeComponent();
        }

        private void Registration_Load(object sender, EventArgs e)
        {
            cn = new SqlConnection(@"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=C:\Users\User\Desktop\Registration3games-main\3 games\RegistrationAndLogin\Database.mdf;Integrated Security=True");
            cn.Open();
        }

        private void BtnRegister_Click(object sender, EventArgs e)
        {
            if (txtconfirmpassword.Text != string.Empty || txtpassword.Text != string.Empty || txtusername.Text != string.Empty || txtemail.Text != string.Empty)
            {
                if (txtpassword.Text == txtconfirmpassword.Text)
                {
                    cmd = new SqlCommand("select * from LoginTable where username='" + txtusername.Text + "'", cn);
                    dr = cmd.ExecuteReader();
                    if (dr.Read())
                    {
                        dr.Close();
                        MessageBox.Show("Username Already exist please try another ", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                    }
                    else
                    {
                        dr.Close();
                        cmd = new SqlCommand("insert into LoginTable values(@username,@password,@email)", cn);
                        cmd.Parameters.AddWithValue("username", txtusername.Text);
                        cmd.Parameters.AddWithValue("password", txtpassword.Text);
                        cmd.Parameters.AddWithValue("email", txtemail.Text);
                        cmd.ExecuteNonQuery();
                        MessageBox.Show("Your Account is created . Please login now.", "Done", MessageBoxButtons.OK, MessageBoxIcon.Information);
                    }
                }
                else
                {
                    MessageBox.Show("Please enter both password same ", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
            else
            {
                MessageBox.Show("Please enter value in all field.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void Button1_Click(object sender, EventArgs e)
        {
            this.Hide();
            Login login = new Login();
            login.ShowDialog();
        }






