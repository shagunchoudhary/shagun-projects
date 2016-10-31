# shagun-projects
contains code of bus management 
#include<iostream>
#include<stdio.h>
#include<stdlib.h>
#include<fstream>
#include<string.h>
using namespace std;

void show_menu();
void show_bus_menu();
void show_driver_menu();
void show_member_menu();
void add_bus();
void add_driver();
void add_member();
void search_bus();
void search_driver();
void search_member();
void show_bus_list();
void show_driver_list();
void show_member_list();
void more();
void bos();			// bus on stop
void password();
void change_password();
void clr(){system("cls");}


int z=0;		// for looping the menu

class bus{
int bid;		// bus id
char bno[10];		// bus number
char rno[10];		// registration no
public:
int stop[20];
void get_data();
int ret_bid(){return bid;}
void put_data();
};

class member{
int mid;
char mname[20];
long mphone;
public:
void get_data();
int ret_mid(){return mid;}
void put_data();
};

class driver{
int did;
char dname[20];
long dphone;
public:
void get_data();
int ret_did(){return did;}
void put_data();
};

	bus B;
	member M;
	driver D;

void bus::get_data(){
clr();
cout<<"\nEnter Bus ID: ";
cin>>bid;
getchar();
cout<<"\nEnter bus no: ";
gets(bno);
cout<<"\nEnter Registration no : ";
gets(rno);
cout<<"\nEnter stops:\n";
for(int i=0;i<20;i++)
{
cin>>stop[i];
if (stop[i]==0) break;
}
}

void bus::put_data(){
cout<<"\nBus ID: "<<bid;
cout<<"\nBus no: ";
puts(bno);
cout<<"Registration no : ";
puts(rno);
cout<<"Stops: ";
for(int i=0;i<20;i++)
	{
		if (stop[i]==0) break;
		if (stop[i+1]==0)
			{
				cout<<stop[i];
			}
		else
			{
				cout<<stop[i]<<",";
			}
	}
}

void member::get_data(){
clr();
cout<<"\nEnter Member ID: ";
cin>>mid;
getchar();
cout<<"\nEnter Member name: ";
gets(mname);
cout<<"\nEnter Member phone: ";
cin>>mphone;
}

void member::put_data(){
cout<<"\nMember ID: "<<mid;
cout<<"\nMember name: ";
puts(mname);
cout<<"Member phone: "<<mphone;
}

void driver::get_data(){
clr();
cout<<"\nEnter Driver ID: ";
cin>>did;
getchar();
cout<<"\nEnter Driver name: ";
gets(dname);
cout<<"\nEnter Driver phone: ";
cin>>dphone;
}

void driver::put_data(){
cout<<"\nDriver ID: "<<did;
cout<<"\nDriver name: ";
puts(dname);
cout<<"Driver phone: "<<dphone;
}


void show_menu()
{
	clr();
	int ch;
	cout<<"\n1.Bus Records\n2.Member Records\n3.Driver Records\n4.More \n5.Exit\n\nEnter Choice:";
	cin>>ch;
	switch(ch)
	{
			case 1:{
						show_bus_menu();
						break;
				}
			case 2:{
						show_member_menu();
						break;
				}
			case 3:{
						show_driver_menu();
						break;
				}
			case 4:{
						more();
						break;
				}
			case 5:{
						z=1;
						break;
				}
	}
}


void show_bus_menu(){
	clr();
	int ch;
	cout<<"\n1.Add Bus\n2.Show Bus List\n3.Search Bus\n4.Back\n\nEnter Choice:";
	cin>>ch;
	switch(ch)
	{
			case 1:{
						add_bus();
						break;
				}
			case 2:{
						show_bus_list();
						break;
				}
			case 3:{
						search_bus();
						break;
				}
			case 4:{
						show_menu();
						break;
				}
	}
}

void show_driver_menu(){
	clr();
	int ch;
	cout<<"\n1.Add Driver\n2.Show Driver List\n3.Search Driver\n4.Back\n\nEnter Choice:";
	cin>>ch;
	switch(ch)
	{
			case 1:{
						add_driver();
						break;
				}
			case 2:{
						show_driver_list();
						break;
				}
			case 3:{
						search_driver();
						break;
				}
			case 4:{
						show_menu();
						break;
				}
	}	
}

void show_member_menu(){
	clr();
	int ch;
	cout<<"\n1.Add Member\n2.Show Member List\n3.Search Member\n4.Back\n\nEnter Choice:";
	cin>>ch;
	switch(ch)
	{
			case 1:{
						add_member();
						break;
				}
			case 2:{
						show_member_list();
						break;
				}
			case 3:{
						search_member();
						break;
				}
			case 4:{
						show_menu();
						break;
				}
	}
}


void add_bus()
{
	char des;
	B.get_data();
	cout<<"\n Do you want to save this record (Y/N): ";
    cin>>des;
    des=tolower(des);
    if (des=='y')
  		{  
	       fstream f;
     	   f.open("brec.txt",ios::out|ios::app);
     	   f.write((char*)&B,sizeof(B));
     	   f.close();
     	   cout<<"\n Bus added successfully...";
		}
	getchar();
	getchar();
}

void add_driver()
{
	char des;
	D.get_data();
	cout<<"\n Do you want to save this record (Y/N): ";
        cin>>des;
        des=tolower(des);
        if (des=='y')
        {  
           fstream f;
           f.open("drec.txt",ios::out|ios::app);
           f.write((char*)&D,sizeof(D));
           f.close();
           cout<<"\n Driver added successfully...";
        }
	getchar();
	getchar();
}

void add_member()
{
	char des;
	M.get_data();
	cout<<"\n Do you want to save this record (Y/N): ";
        cin>>des;
        des=tolower(des);
        if (des=='y')
        {  
           fstream f;
           f.open("mrec.txt",ios::out|ios::app);
           f.write((char*)&M,sizeof(M));
           f.close();
           cout<<"\n Member added successfully...";
        }
	getchar();
	getchar();
}
void search_bus()
{	
	clr();
	int id,found=0;
	cout<<"Enter ID:";
	cin>>id;
	fstream f;
	f.open("Brec.txt",ios::in);
	f.seekg(0);
	while(f)
	{
		f.read((char*)&B,sizeof(B));
		if(f.eof())break;
		if (id==B.ret_bid())
		{
			B.put_data();
			found=1;
			break;
		}
	}
	if (found==0) cout<<"\n Not Found.";
	getchar();getchar();
}
void search_driver()
{
	clr();
	int id,found=0;
	cout<<"Enter ID:";
	cin>>id;
	fstream f;
	f.open("drec.txt",ios::in);
	f.seekg(0);
	while(f)
	{
		f.read((char*)&D,sizeof(D));
		if(f.eof())break;
		if (id==D.ret_did())
		{
			D.put_data();
			found=1;
			break;
		}
	}
	if (found==0) cout<<"\n Not Found.";
	getchar();getchar();
}
void search_member()
{
	clr();
	int id,found=0;
	cout<<"Enter ID:";
	cin>>id;
	fstream f;
	f.open("mrec.txt",ios::in);
	f.seekg(0);
	while(f)
	{
		f.read((char*)&M,sizeof(M));
		if(f.eof())break;
		if (id==M.ret_mid())
		{
			M.put_data();
			found=1;
			break;
		}
	}
	if (found==0) cout<<"\n Not Found.";
	getchar();getchar();
}
void show_bus_list()
{
	clr();
	fstream f;
	f.open("brec.txt",ios::in);
        while(f)
	{		
	     	f.read((char*)&B,sizeof(B));
	     	if(f.eof())break;
			B.put_data();
			cout<<"\n\n";
	}
	f.close();		
	getchar();
	getchar();	
}
void show_driver_list()
{
	clr();
	fstream f;
	f.open("drec.txt",ios::in);
        while(f)
	{		
	     	f.read((char*)&D,sizeof(D));
	     	if(f.eof())break;
			D.put_data();
			cout<<"\n\n";
	}
	f.close();	
	getchar();
	getchar();	
}

void show_member_list()
{
	clr();
	fstream f;
	f.open("mrec.txt",ios::in);
        while(f)
	{		
	     	f.read((char*)&M,sizeof(M));
	     	if(f.eof())break;
			M.put_data();
			cout<<"\n\n";
	}
	f.close();	
	getchar();
	getchar();	
}

void more(){
	clr();
	int ch;
	cout<<"\n1.Change Password\n2.Lock\n3.Bus on Stop\n4.Back\n\nEnter Choice:";
	cin>>ch;
	switch(ch)
	{
			case 1:{
						change_password();
						break;
				}
			case 2:{
					 	getchar();password();
						break;
				}
			case 3:{
						bos();
						break;
				}
			case 4:{
						show_menu();
						break;
				}
	}
}

void bos(){
	clr();
	int sno;
	cout<<"Enter Stop no: ";
	cin>>sno;
	fstream f;
	f.open("brec.txt",ios::in);
	while(f)
	{
		f.read((char*)&B,sizeof(B));
		if(f.eof())break;
		for(int i=0;i<20;i++)
		{
			if(sno==B.stop[i])
			{
				int bid=B.ret_bid();
				cout<<"\nBus no: "<<bid;
			}
		}
	}
	getchar();getchar();
}

void password()
{
  int j=3;
  char pass[7];
  char password[11];
  int flag;
  clr();
  fstream f;
  f.open("pass.txt",ios::in);
  
  while (!f.eof())
  {
 	f >> password;  // fetching password from file
  }
 
 cout<<"\t\tJIET Bus Management System";
 
  while (j!=0)
   {
      cout<<"\n\nEnter Password (" <<j<<" chances left) :";
	  gets(pass);
      flag=strcmpi(password,pass);
	  if(flag==0)       // password is correct
  		{
		  while(z!=1)
		  show_menu();
		  break;
  		}
  	  else
  	  cout<<"\n Password is wrong....";
  	  j--;
  }
}

void change_password()
{

	char op[10];   // old password
	char np[10];   // new password
	char npr[10];  // re-entered new password
	char password[10]; //receives password from file
	getchar();

	fstream f;
    f.open("pass.txt",ios::in);
    while (f)
      {
 	      f >> password;  // fetching password from file
      }
    f.close();
	clr();
	cout<<" Enter Old Password: ";
	gets(op);

	if(strcmpi(password,op)==0)
	{
	cout<<"\n\n (Note: Donot use spaces in your password)\n\n";
	cout<<" Enter new password: ";
	gets(np);
	cout<<" Re-Enter New Password: ";
	gets(npr);
	if (strcmpi(np,npr)==0)
	   {
	   	ofstream f;
	    f.open("pass.txt",ios::out);
        f << np;  // writing password to file
        f.close();
		cout<<"\n\n Password changed successfully.";
		cout<<"\n\n Press ENTER to return....";
		getchar();
	   }
	   else
	   {
	   cout<<"\n\n New password and re-entered new password does not match.";
	   cout<<"\n\n press ENTER to return....";
	   getchar(); getchar();
	   }

	}
	else
	{
	   cout<<"\n\n The Old Password you entered is incorrect.";
	   cout<<"\n\n Press ENTER to return....";
	   getchar();
	}
	show_menu();
}



int main()
{
	password();
}
