# BlackJack-C-

In Blackjack, players aim to have a hand value closer to 21 than the dealer’s hand without exceeding 21. Each player is dealt two cards, and card values are as follows: numbered cards are worth their face value, face cards (King, Queen, Jack) are worth 10, and Aces can be worth 1 or 11, depending on what benefits the hand. Players can choose to "hit" (take an additional card) or "stand" (keep their current hand). If a player's hand exceeds 21, they "bust" and lose the round. The dealer must draw cards until reaching at least 17. If the dealer busts, remaining players win. If neither busts, the hand closest to 21 wins.


Code For Class:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    
    namespace BlackJack
    {
        class Class
        {
            private static string _Globalusername = "ivantop";
            private static string _Globalpass = "1234";
            private static string _GlobalID = "X";
    
            public static string Globalusername
            {
                get { return _Globalusername; }
                set { _Globalusername = value; }
            }
            public static string Globalpass
            {
                get { return _Globalpass; }
                set { _Globalpass = value; }
            }
            public static string GlobalID
            {
                get { return _GlobalID; }
                set { _GlobalID = value; }
            }
        }
    }


Code For Form1 Login Page:

    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    
    namespace BlackJack
    {
        public partial class Form1 : Form
        {
            public Form1()
            {
                InitializeComponent();
                label1.BackColor = Color.Transparent;
                Password_input.UseSystemPasswordChar = true;
                Password_input.PasswordChar = '•';
            
            }
    
            private void Form1_Load(object sender, EventArgs e)
            {
                
            }
    
            private void Login_button_Click(object sender, EventArgs e)
            {
                string username = Username_input.Text;
                string password = Password_input.Text;
                string real_username = Class.Globalusername.ToString();
                string real_password = Class.Globalpass.ToString();
                if (username == real_username)
                {
                    if (password == real_password)
                    {
                        Class.GlobalID = "W";
                        Form Form2 = new BlackJackInterface();
                        Form2.ShowDialog();
                      
                    }
                    else
                    {
                        MessageBox.Show("Wrong Password");
                    }
                }
    
                else
                {
                    MessageBox.Show("wrong username");
                }
                Username_input.Text = "";
                Password_input.Text = "";
    
            }
    
    
        }
    }


Code For BlackJackInterface:

    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    
    namespace BlackJack
    {
        public partial class BlackJackInterface : Form
        {       
            private List<int> playerHand = new List<int>();
            private List<int> dealerHand = new List<int>();
            private Random random = new Random();
         //   private int i = 0;
            int whatindex = 1;
            int whatindexfordealer = 1;
         
    
            public BlackJackInterface()
            {
                InitializeComponent();
                Restart_button.Hide();
                Draw_button.Hide();
                Hold_button.Hide();
                Menu_button.Hide();
                Playerscore.Text = "";
                Dealerscore.Text = "";
                HideCards();
                
    
    
            }
    
            private void HideCards()
            {
                pictureBox1.Hide();//players cards
                pictureBox12.Hide();//players cards
                pictureBox13.Hide();//players cards
                pictureBox14.Hide();
                pictureBox15.Hide();
    
                pictureBox2.Hide();//dealers cards
                pictureBox22.Hide();//dealers cards
                pictureBo23.Hide();//dealers cards
                pictureBox24.Hide();
                pictureBox25.Hide();
            }
    
            private void Finish_Game()
            {
                Draw_button.Enabled = false;
                Hold_button.Enabled = false;
                Restart_button.Show();
                Menu_button.Show();
            }
    
            private void Find_Winner()
            {
                int playerTotal = CalculateHand(playerHand);
                int dealerTotal = CalculateHand(dealerHand);
    
                Dealerscore.Text = "Dealer: " + string.Join(", ", dealerHand);
    
                if (dealerTotal > 21)
                {
                    info_label.Text = "Dealer busted! You win!";
                }
                else if (playerTotal > dealerTotal)
                {
                    info_label.Text = "You win! Your total: " + playerTotal + " vs Dealer's total: " + dealerTotal;
                }
                else if (dealerTotal > playerTotal)
                {
                    info_label.Text = "Dealer wins! Dealer's total: " + dealerTotal + " vs Your total: " + playerTotal;
                }
                else
                {
                    info_label.Text = "It's a tie!";
                }
    
                Finish_Game();
            }
    
            private int DrawCardP1()
            {
                int randomcard = random.Next(2, 12);
                if (whatindex == 1)
                {
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox1.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox1.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox1.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox1.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox1.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox1.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox1.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox1.Image = Properties.Resources.image10K; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox1.Show();
                    whatindex += 1;
                }
                else if (whatindex == 2)
                {               
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox12.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox12.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox12.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox12.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox12.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox12.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox12.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox12.Image = Properties.Resources.image10Q; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox12.Show();
                    whatindex += 1;
                }
                else if (whatindex == 3)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox13.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox13.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox13.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox13.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox13.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox13.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox13.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox13.Image = Properties.Resources.image10J; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox13.Show();
                    whatindex += 1;
                }
                else if (whatindex == 4)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox14.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox14.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox14.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox14.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox14.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox14.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox14.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox14.Image = Properties.Resources.image10K; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox14.Show();
                    whatindex += 1;
                }
                else if (whatindex == 5)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox15.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox15.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox15.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox15.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox15.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox15.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox15.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox15.Image = Properties.Resources.image10Q; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox15.Show();
                    whatindex += 1;
                }
               
                return randomcard; // Returns a random card value between 2 and 11
    
            }
            private int DrawCardP2()
            {
                int randomcard = random.Next(2, 12);
                if (whatindexfordealer == 1)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox2.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox2.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox2.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox2.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox2.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox2.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox2.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox2.Image = Properties.Resources.image10J; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox2.Show();
                    whatindexfordealer += 1;
                }
                else if (whatindexfordealer == 2)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox22.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox22.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox22.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox22.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox22.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox22.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox22.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox22.Image = Properties.Resources.image10K; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox22.Show();
                    whatindexfordealer += 1;
                }
                else if (whatindexfordealer == 3)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBo23.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBo23.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBo23.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBo23.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBo23.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBo23.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBo23.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBo23.Image = Properties.Resources.image10Q; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBo23.Show();
                    whatindexfordealer += 1;
                }
                else if (whatindexfordealer == 4)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox24.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox24.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox24.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox24.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox24.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox24.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox24.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox24.Image = Properties.Resources.image10Q; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox24.Show();
                    whatindexfordealer += 1;
                }
                else if (whatindexfordealer == 5)
                {
                    
                    if (randomcard == 2) { pictureBox2.Image = Properties.Resources.image2; }
                    else if (randomcard == 3) { pictureBox25.Image = Properties.Resources.image3p; }
                    else if (randomcard == 4) { pictureBox25.Image = Properties.Resources.image4c; }
                    else if (randomcard == 5) { pictureBox25.Image = Properties.Resources.image5p; }
                    else if (randomcard == 6) { pictureBox25.Image = Properties.Resources.image6h; }
                    else if (randomcard == 7) { pictureBox25.Image = Properties.Resources.image7d; }
                    else if (randomcard == 8) { pictureBox25.Image = Properties.Resources.image8h; }
                    else if (randomcard == 9) { pictureBox25.Image = Properties.Resources.image9p; }
                    else if (randomcard == 10) { pictureBox25.Image = Properties.Resources.image10Q; }
                    else if (randomcard == 11 || randomcard == 1) { pictureBox25.Image = Properties.Resources.Ace; }
                    pictureBox25.Show();
                    whatindexfordealer += 1;
                }
                return randomcard; // Returns a random card value between 2 and 11
    
            }
    
      //      private void CardShow(List<int> playerHand)
    
    
            private void Ace_fix()
            {
                for (int i = 0; i < playerHand.Count; i++)
                {
                    if (playerHand[i] == 11)
                    {
                        playerHand[i] = 1;
                    }
                }
            }
            private int CalculateHand(List<int> hand)
            {
                int total = 0;
                int aceCount = 0;
    
                foreach (int card in hand)
                {
                    if (card == 11)
                    {
                        aceCount++;
                    }
                    total += card;
                }
    
                while (total > 21 && aceCount > 0)// See if Aces total is over 21
                {
                    total -= 10;
                    aceCount--;
                    Ace_fix();
                    
                }
    
                return total;
    
            }
    
            private void BlackJackInterface_Load(object sender, EventArgs e)
            {
                string FID = Class.GlobalID.ToString();
                if (FID == "X")
                {
                    MessageBox.Show("no login");
                    this.Close();
                }
                label1.Text = Class.Globalusername.ToString();
    
            }
    
            private void Strat_button_Click(object sender, EventArgs e)
            {
                Draw_button.Show();
                Hold_button.Show();
                          
                playerHand.Clear();  // Reset game 
                dealerHand.Clear();
                
                playerHand.Add(DrawCardP1());// two cards for player and dealer
                playerHand.Add(DrawCardP1());
                dealerHand.Add(DrawCardP2());
                dealerHand.Add(DrawCardP2());
                pictureBox22.Hide();
    
                Scores();
                Hold_button.Enabled = true;
                Draw_button.Enabled = true;
                Strat_button.Hide();
                
    
          //      CardShow(playerHand);
            
                
    
            }
    
            private void Hold_button_Click(object sender, EventArgs e)
            {
                int dealerTotal = CalculateHand(dealerHand);
                while (dealerTotal < 17)
                {
                    dealerHand.Add(DrawCardP2());
                    dealerTotal = CalculateHand(dealerHand);
                    pictureBox22.Show();
                }
    
                Scores();
                Find_Winner();
            }
    
            private void Draw_button_Click(object sender, EventArgs e)
            {
                playerHand.Add(DrawCardP1());
                CalculateHand(playerHand);
                Scores();
                
               // MessageBox.Show(CalculateHand(playerHand).ToString());
    
                if (CalculateHand(playerHand) > 21)
                {
                    info_label.Text = "You busted! Dealer wins.";
                    Dealerscore.Text = "Dealer: " + string.Join(", ", dealerHand);
                    Finish_Game();
                }
                
                
            }
    
            private void Scores()
            {
                Playerscore.Text = "Player: " + string.Join(", ", playerHand) + " (Total: " + playerHand.Sum() + ")"; //CalculateHand(playerHand);
                Dealerscore.Text = "Dealer: " + dealerHand[0] + " + ?";
                
                
            }
    
            private void Restart_button_Click(object sender, EventArgs e)
            {
                Playerscore.Text = "";
                Dealerscore.Text = "";
    
                playerHand.Clear();
                dealerHand.Clear();
                HideCards();
    
                Hold_button.Enabled = false;
                Draw_button.Enabled = false;
    
                info_label.Text = "";           
                Strat_button.Show();
                Restart_button.Hide();
                Menu_button.Hide();
                whatindex = 1;
                whatindexfordealer = 1;
    
            }
    
            private void Menu_button_Click(object sender, EventArgs e)
            {
                this.Close();
                 
            }
    
    
        }
    }


  
