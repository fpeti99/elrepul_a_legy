...........
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace _2_ZH_GYAKORLAS
{
    class Legy
    {

        /*Button legy;
        public Legy (Button l)
        {
            legy = l;
            legy.Height = 10;
            legy.Width = 10;
            legy.Text = "";
        }*/

        public void repul(int x_elmozdulas, int y_elmozdulas,Button b)
        {
            b.Left = b.Left + x_elmozdulas;
            b.Top = b.Top + y_elmozdulas;
        }

        public bool beka_veszely(int x, int y, Button b)
        {
            //AB távolság: gyök (b1  - a1) négyzet + (b2 - a2) négyzet
            bool veszely = false;

            if (Math.Sqrt(Math.Pow((b.Left - x), 2) + Math.Pow((b.Top - y), 2)) < 100)
            {
                veszely = true;
            }

            return veszely;
        }

        public bool beka_megette(int x, int y, Button b)
        {
            bool megette = false;

            if (Math.Sqrt(Math.Pow((b.Left - x), 2) + Math.Pow((b.Top - y), 2)) < 50)
            {
                megette = true;
            }

            return megette;
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

namespace _2_ZH_GYAKORLAS
{
    public partial class Form1 : Form
    {
        Legy L = new Legy();
        Random rand = new Random();

        int eger_x;
        int eger_y;

        int irany;

        int sebesseg = 25;

        int x_elmozdulas, y_elmozdulas;

        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void Form1_MouseMove(object sender, MouseEventArgs e)
        {
            eger_x = e.X;
            eger_y = e.Y;

            label1.Text = eger_x.ToString();
            label2.Text = eger_y.ToString();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
         
            irany = rand.Next(1, 5);
           
                switch (irany)
                { 
                    case 1:
                        {
                            x_elmozdulas = sebesseg;
                            y_elmozdulas = 0;
                            break;
                        }
                    case 2:
                        {
                            x_elmozdulas = -sebesseg;
                            y_elmozdulas = 0;
                            break;
                        }
                    case 3:
                        {
                            x_elmozdulas = 0;
                            y_elmozdulas = sebesseg;
                            break;
                        }
                    case 4:
                        {
                            x_elmozdulas = 0;
                            y_elmozdulas = -sebesseg;
                            break;
                        }
                    default: break;
              }
            

            /*if(button1.Left < 0 || button1.Top < 0 || button1.Left + button1.Width > Width - 50 || button1.Top + button1.Height < Height - 50)
            {
               
            }*/

            L.repul(x_elmozdulas, y_elmozdulas, button1);

            if (L.beka_veszely(eger_x, eger_y, button1) == true)
            {
                sebesseg = 100;
                button1.BackColor = Color.Red;
            }
            else
            {
                sebesseg = 25;
                button1.BackColor = Color.White;
            }

            if(L.beka_megette(eger_x, eger_y, button1) == true)
            {
                timer1.Enabled = false;
                MessageBox.Show("Nyertél!");
                timer1.Enabled = true;
            }

        }
    }
}
