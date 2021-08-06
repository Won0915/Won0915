#include<iostream>
//#include"mylib.h"
#include <stdio.h>
#include <conio.h>
#include<ctime> /* thu vi?n h? tr? v? th?i gian th?c */
#include "windows.h" // thu vi?n này bá d?o l?m nhé - ch?a nhi?u d? choi nek - c? tìm hi?u d?n d?n s
//======= l?y t?a d? x c?a con tr? hi?n t?i =============
#define KEY_NONE	-1
using namespace std;
#define Max 100
int sl = 7;
//ve tuong tren

void ve_tuong_tren();
void ve_tuong_duoi();
void ve_tuong_trai();
void ve_tuong_phai();
void ve_tuong();
void khoi_tao_ran(int toadox[], int toadoy[]);
void xoa_du_lieu_cu(int toadox[], int toadoy[]);
void ve_ran(int toadox[], int toadoy[]);
void xu_li_ran(int toadox[], int toadoy[], int x, int y, int &xqua, int &yqua);

void them(int a[], int x);
void xoa(int a[], int vt);

bool kt_ran_cham_tuong(int x0, int y0);
bool kt_ran_cham_duoi(int toadox[], int toadoy[]);
bool kt_ran(int toadox[], int toadoy[]);


void taoqua(int &xqua, int &yqua, int toadox[], int toadoy[]);
bool kt_ran_de_qua(int xqua, int yqua, int toadox[], int toadoy[]);
bool kt_ran_an_qua(int xqua, int yqua,int x0,int y0);

void gotoXY(short x, short y)
{
	HANDLE hConsoleOutput;
	COORD Cursor_an_Pos = { x, y };
	hConsoleOutput = GetStdHandle(STD_OUTPUT_HANDLE);
	SetConsoleCursorPosition(hConsoleOutput, Cursor_an_Pos);
}

void SetColor(WORD color)
{
	HANDLE hConsoleOutput;
	hConsoleOutput = GetStdHandle(STD_OUTPUT_HANDLE);

	CONSOLE_SCREEN_BUFFER_INFO screen_buffer_info;
	GetConsoleScreenBufferInfo(hConsoleOutput, &screen_buffer_info);

	WORD wAttributes = screen_buffer_info.wAttributes;
	color &= 0x000f;
	wAttributes &= 0xfff0;
	wAttributes |= color;

	SetConsoleTextAttribute(hConsoleOutput, wAttributes);
}

void ve_tuong_tren()
{
	int x = 10, y =0;
	while(x < 100)
		{
			gotoXY(x, y);
			cout<<"_";
			x++;
		}
}
void ve_tuong_duoi()
{
	int x = 10, y=26;
		while(x < 100)
		{
			gotoXY(x, y);
			cout<<"_";
			x++;
		}
}

void ve_tuong_trai()
{
	int x =10, y=1;
	while(y < 27)
		{
			gotoXY(x, y);
			cout<<"|";
			y++;
		}

}

void ve_tuong_phai()
{
	int x = 100, y = 1 ;
	while(y < 27)
		{
			gotoXY(x, y);
			cout<<"|";
			y++;
		}	
}
//khoi tao ran

void khoi_tao_ran(int toadox[], int toadoy[]) // gióng hàm khoi tao gia tri
{
	int x = 50, y = 13; // vì lúc nãy láy màn hình console có chieu dai la 100, nên chia 2
	for(int i=0; i<sl; i++) // sl là do dai cua con ran
		{
			toadox[i] = x;
			toadoy[i] = y;
			x--;
		}
		
}
//ve ran

void ve_ran(int toadox[], int toadoy[]) // gióng hàm xuát giá tri
{
	
	for(int i=0; i<sl; i++)
		{
				gotoXY(toadox[i], toadoy[i]);
					if(i == 0)
						cout<<"O";
					else
						cout<<"o";
		}	
}
void ve_tuong()
{
	int i = rand()%(15-1+1)+1;
	SetColor(i);
	ve_tuong_tren();
	ve_tuong_duoi();
	ve_tuong_trai();
	ve_tuong_phai();
	SetColor(7);
} 
//con ran di chuyen
void xu_li_ran(int toadox[], int toadoy[], int x, int y, int &xqua, int &yqua)
{
	them(toadox, x);
	them(toadoy, y);
		if(kt_ran_an_qua(xqua, yqua, toadox[0], toadoy[0]) == false)
			{
					xoa(toadox, sl-1);
					xoa(toadoy, sl-1);
					
			}
		else
			{
				taoqua(xqua, yqua, toadox, toadoy);
			}
	ve_ran(toadox, toadoy);
	//tao lai qu?

}
//con ran di chuyen lien quan toi thuat toan, them bot phan tu
void them(int a[], int x)
{
	for(int i=sl; i> 0; i--)
		{
			a[i] = a[i-1];
		}
	a[0] = x;
	sl++;
}

void xoa(int a[], int vt)
{
	for(int i = vt; i < sl; i++)
		{
			a[i] = a[i+1];
		}
	sl--;
}
// xoa du lieu cu
void xoa_du_lieu_cu(int toadox[], int toadoy[])
{
	
	for(int i=0; i<sl; i++)
		{
				gotoXY(toadox[i], toadoy[i]);
					if(i == 0)
						cout<<" ";
					else
						cout<<" ";
		}	
}

bool kt_ran_cham_tuong(int x0, int y0)
{
	//ran cham tuong tren
	if(y0==1 && (x0 >=10 && x0 <= 100))
	{
			return true;
	}
	//ran cham tuong duoi
	else if(y0==26 && (x0 >=10 && x0 <= 100))
	{
			return true;
	}
	//ran cham tuong phai
	else if(x0 == 100 && (y0 >=1 && y0 <= 26))
	{	
		return true;
	}
	//ran cham tuong trai
	else if(x0==10 && (y0 >=1 && y0 <= 26))		
	{
			return true;
	}
	return false;
}

bool kt_ran_can_duoi(int toadox[], int toadoy[])
{
	for(int i=1; i<sl; i++)
		{
			if((toadox[0] == toadox[i]) && (toadoy[0] == toadoy[i]))
				return true;	
		}
	return false;
}

bool kt_1_trong2dk(int toadox[], int toadoy[])
{
	bool kt1 =  kt_ran_can_duoi(toadox,toadoy);
	bool kt2 =  kt_ran_cham_tuong(toadox[0], toadoy[0]);
	if(kt1 == true || kt2 == true)
		return true;
	return false;
}

//tao qua
void taoqua(int &xqua, int &yqua, int toadox[], int toadoy[])
{
  do
    {
        	//11<=xqua<=99
	xqua = rand()%(99-11+1)+11;
		 //2<=yqua<=25	
	yqua = rand()%(25-2+1)+2;
    } while (kt_ran_de_qua(xqua, yqua, toadox, toadoy) == true);
	
	int i = rand()%(15-1+1)+1;
	SetColor(i);
	gotoXY(xqua, yqua);
	cout<<"*";
	//int a = rand()%(100-2+1)+2;
	SetColor(75); //con ran luôn màu trang
}

//kiem tra vi tri ran dè len qu?
bool kt_ran_de_qua(int xqua, int yqua, int toadox[], int toadoy[])
{
	for(int i=0; i<sl; i++)
		{
			if((xqua == toadox[i]) && (yqua == toadoy[i]))
				return true;
		}
	return false;
}

//kiem tra ran an qua
bool kt_ran_an_qua(int xqua, int yqua,int x0,int y0)
{
	if(x0 == xqua && y0 == yqua)
		{
			return true;
		}
	return false;
}

//hien thi diem
/*void score(int toadox[], int toadoy[], int &xqua, int &yqua)
{
	
	int s =0;
	int xcu = 6, ycu= 0;
	if(kt_ran_an_qua(xqua, yqua, toadox[0], toadoy[0]) == true)
		s++;
	while(kt_1_trong2dk(toadox, toadoy) == false)
		{
				
			gotoXY(xcu, ycu);
			cout<<" ";
			gotoXY(6,0);
	
			cout<<s;
			xcu = ycu;
		}
	Sleep(300);
}*/
int main()
{
	srand(time(NULL));
	bool gameover = false;
	int x0, y0;
	int toadox[Max], toadoy[Max];
	ve_tuong();
	khoi_tao_ran(toadox, toadoy);
	ve_ran(toadox, toadoy);
	int xqua, yqua;
	//phai de phan tao qua o duoi phan tao ran, boi vi neu chua co ran thi khong the kiem tra dieu kien duoc
	
	
	taoqua(xqua, yqua, toadox, toadoy);
    //d? có t?a d? cu
    int x =50, y=13; //dinh hien vi tri ran di chuyen dau game
    int check = 3;
    
   	//int i=2;
    while(gameover == false)
    {   
    	/*SetColor(i);
    	if(i > 15)
    		{
    			i = 2;
			}
		i++;
		*/
		xoa_du_lieu_cu(toadox, toadoy);

    	      	if(_kbhit())
      		{
      			char kitu = _getch();
      			if(kitu==-32)
      				{
      					kitu= _getch();
      					if(kitu == 72 && check != 0 )//di len
      						{
      							check =1;
							  }
						else if(kitu == 80 && check != 1 )//di xuong
							{
								check = 0;
							}
						else if(kitu == 75 && check != 3)//qua trai
							{
								check =2;
							}
						else if(kitu == 77 && check != 2)//qua phai
							{
								check = 3;
							}
					}
			  }

		        //d? dòng ch? ch?y xu?ng, thì y nó ph?i tang lên
        //ki?m tra hu?ng len xuong
      	if(check == 0)
            {
                y++;
            }
        else if(check == 1)
            {
                y--;
            }
        //kt huong trai phai
        else if(check == 2) //qua trai
        	{
        		x--;
			}
		else if(check == 3) //qua phai
			{
				x++;
			}
		xu_li_ran(toadox, toadoy, x, y, xqua, yqua);
		//score(toadox, toadoy, xqua, yqua);
		Sleep(100);
		//kiem tra game over
		gameover = kt_1_trong2dk(toadox, toadoy);
	}
if(gameover == true)
	{
		gotoXY(50,13);
		cout<<"GAME OVER!";
	}
    getch();
    return 0;
}
