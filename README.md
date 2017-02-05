TestGithub

Casino game

/*This program is for a casino game in which the player has to deposit a certain amount of money and from that fixed amount
he or she has to bet for the game. Basically, we have used functions,class,inheritance,files for successfully implementing
the program.*/




//***********************************************CASINO GAME**********************************************************
//COMPILED BY-
//NOBLE JOY              



//PRE PROCESSOR DIRECTIVES
#include<iostream>
#include<string>
#include<cstdlib>
#include<fstream>

using namespace std;

void rules();                    //FUNCTION PROTOTYPE

void lines(int no,char sign);   //PARAMETERISED FUNCTION PROTOTYPE

class casino_entry              //BASE CLASS
{
public:
   string name;                 //BASE CLASS VARIABLES
    int age;                    //PUBLIC MEMBERS
    int i;
   double amount;
   double betamount;

    casino_entry()              //CONSTRUCTOR
    {
        betamount=0;
        age=0;
        amount=0;
    }

    void details()              //FUNCTION TO ENTER THE DETAILS OF PLAYER
    {
       i=1;
      cout<<"\nPRESS \"ENTER\" TO START:\n";
        cin.ignore();
        {
        cout<<"Enter your full name : ";
        getline(cin,name);
        cout<<"\n";
        cout<<"Enter your age : ";
        cin>>age;
        if(age<18)
        {
            cout<<"************GAME ONLY FOR ADULTS************";
            exit(0);
        }
        cout << "\n\nEnter Deposit amount to play game : RS.";
        cin >> amount;
        if(amount==0||amount<0)
        {
            cout<<"Deposit valid amount : RS.";
            cin>>amount;
        }
        }


    }

    void bet_placing()              //FUNCTION TO PLACE AND CHECK BETTING AMOUNT
    {

            system("cls");
            rules();
            cout << "\n\nYour current balance is RS." << amount <<"\n";


            do
            {
                cout <<name<<",enter money to bet : RS.";
                cin >> betamount;
                if(betamount > amount)
                cout << "Your betting amount is greater than your available balance\n"
                       <<"\nRe-enter data\n ";
            }while(betamount >amount);


     }

};

class play:public casino_entry          //PUBLICLY INHERITED CLASS FROM BASE CLASS
{
    int num;                            //PRIVATE VARIABLES
    int random;
    char option;
public:
    casino_entry a;                     //BASE CLASS OBJECT CREATED

    void game()                         //FUNCTION BODY
    {
        fstream file;                   //CREATING FILE OBJECT
        file.open("casin.txt",ios::app);   //OPENING A FILE
        a.details();                    //FUNCTION CALL USING OBJECT
        file<<"\n";                             //INPUTTING DATA INTO FILE
        file<<"NAME:"<<a.name<<endl;
        file<<"AGE:"<<a.age<<endl;
        file<<"AMOUNT: RS."<<a.amount<<endl;

        do
        {

            a.bet_placing();            //FUNCTION CALL USING OBJECT
            file<<"BETAMOUNT"<<(a.i)++<<":"<<a.betamount<<endl;     //INPUTTING DATA INTO FILE
            do
            {
                cout << "Guess your number to bet between 1 to 20 :";
                cin >> num;
                if(num <= 0 || num > 20)
                    cout << "Please check the number!! should be between 1 to 20\n"
                        <<"\nRe-enter data\n ";
            }
            while(num <= 0 || num > 20);

            random = rand()%20+1 ;      //CREATING RANDOM VARIABLE
            if(random == num)
            {
                cout << "\n\nGood Luck!! You won RS." << a.betamount * 10;
                a.amount =a.amount + a.betamount * 10;      //INCREAMENTING FOR WIN
                file<<"WON RS."<<a.betamount*10<<'\n';      //INPUTTING DATA INTO FILE
                file<<"AMOUNT: RS."<<a.amount<<'\n';
            }
            else
            {
                cout << "Bad Luck this time !! You lost RS. "<<a. betamount <<"\n";
                a.amount =a.amount - a.betamount;           //DECREAMENT FOR LOSS
                file<<"LOST RS."<<a.betamount<<'\n';        //INPUTTING DATA INTO FILE
                file<<"AMOUNT: RS."<<a.amount<<'\n';
            }
            cout << "\nThe winning number was : " << random <<"\n";
            cout << "\n"<<a.name<<", You have RS. " << a.amount << "\n";
            if(a.amount == 0)
            {
                cout << "You have no money to play ";
                break;
            }
            cout << "\n\n-->Do you want to play again (y/n)? ";
            cin >> option;
        }
        while(option =='Y'|| option=='y');
        cout << "\n\n\n";
    lines(70,'$');              //FUNCTION CALL
    cout << "\n\nROYAL casino wishes you good luck. Your balance amount is RS. " << a.amount << "\n\n";
    lines(70,'$');
    file<<"CURRENT AMOUNT IN HAND: RS."<<a.amount<<endl;        //INPUTTING DATA INTO FILE
    }
};
//MAIN FUNCTION
int main()
{

    play ob;                    //INHERITED CLASS OBJECT

    lines(120,'+');
    lines(120,'$');              //FUNCTION CALL
    cout << "\n\n\t\t\t\t\t  $$ ROYAL CASINO GAME $$\n\n\n\n";
    lines(120,'$');
    lines(120,'+');

    ob.game();                  //CLASS FUNCTION CALLED


return(0);
}

//END OF MAIN FUNCTION

void rules()                    //FUNCTION DEFINITION
{
    system("cls");
    cout << "\n\n";
    lines(80,'*');              //FUNCTION CALL
    cout << "\t\tRULES OF THE GAME\n";
    lines(80,'*');
    cout<<"\t-> Game is solely for adults\n";
    cout<<"\t-> You can't quit the game after betting the amount\n";
    cout << "\t-> Select a number between 1 to 20\n";
    cout << "\t-> If you win you will get 10 times of amount you bet\n";
    cout << "\t-> If you bet on wrong number you will lose your betting amount\n\n";
    lines(80,'*');
}
void lines(int no, char sign)   //FUNCTION DEFINITION
{
    for(int i=0; i<no; i++)
        cout << sign;
    cout << "\n" ;
}


//***********************************END OF PROGRAM**************************************************

