#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <conio.h>
#include <string.h>


int MAP[4][4];
int Goal;


void add(int n)//随机生成最小数字方块
{
	srand((unsigned int)time(0));//随机数种子
	int nNum_ran = 2;
	int x,y;
	int i;

	x = rand() % 4;//坐标获取，0~3
	y = rand() % 4;
	
	if (n == 0)
	{
		MAP[x][y] = nNum_ran;
	}
	else if (n == 1)
	{
		if (MAP[3][y] == 0) 
		{
			MAP[3][y] = nNum_ran;
		}
		else
		{
			for (i = 0; i < 4; i++)
			{
				if (MAP[3][i] == 0)
				{
					MAP[3][i] = nNum_ran;
					break;
				}
			}
		}
	}
	else if (n == 2)
	{
		if (MAP[0][y] == 0)
		{
			MAP[0][y] = nNum_ran;
		}
		else
		{
			for (i = 0; i < 4; i++)
			{
				if (MAP[0][i] == 0)
				{
					MAP[0][i] = nNum_ran;
					break;
				}
			}
		}
	}
	else if (n == 3)
	{
		if (MAP[x][3] == 0)
		{
			MAP[x][3] = nNum_ran;
		}
		else
		{
			for (i = 0; i < 4; i++)
			{
				if (MAP[i][3] == 0)
				{
					MAP[i][3] = nNum_ran;
					break;
				}
			}
		}
	}
	else if (n == 4)
	{
		if (MAP[x][0] == 0)
		{
			MAP[x][0] = nNum_ran;
		}
		else
		{
			for (i = 0; i < 4; i++)
			{
				if (MAP[i][0] == 0)
				{	
					MAP[i][0] = nNum_ran;
					break;
				}
			}
		}
	}
}
int movup(void)
{
	int i,k,t;
	int flag = 0;
	int n = 0;
	for (k = 0; k < 4; k++)
	{
		n = 4;
		while (n--)
		{
			for (i = 0; i < 3; i++)
			{
				if (MAP[i][k] == 0)
				{
					for (t = i; t < 3; t++)
					{
						MAP[t][k] = MAP[t + 1][k];
						MAP[t + 1][k] = 0;
						flag = 1;
					}
				}
			}
		}
		for (i = 0; i < 3; i++)
		{
			if (MAP[i][k] == MAP[i + 1][k])
			{
				MAP[i][k] *= 2;
				Goal += MAP[i][k];
				if (MAP[i][k] == 2048)
				{
					return 0;
				}
				for (t = i + 1; t < 3; t++)
				{
					MAP[t][k] = MAP[t + 1][k];
					MAP[t + 1][k] = 0;
					flag = 1;
				}
			}
		}
	}
	if (flag == 1)
	{
		add(1);
	}
	return 1;
}
int movdow(void)
{
	int i,k,t;
	int flag = 0;
	int n = 0;
	for (k = 0; k < 4; k++)
	{
		n = 4;
		while (n--)
		{
			for (i = 3; i > 0; i--)
			{
				if (MAP[i][k] == 0)
				{
					for (t = i; t > 0; t--)
					{
						MAP[t][k] = MAP[t - 1][k];
						MAP[t - 1][k] = 0;
						flag = 1;
					}
				}
			}
		}
		for (i = 3; i > 0; i--)
		{
			if (MAP[i][k] == MAP[i - 1][k])
			{
				MAP[i][k] *= 2;
				Goal += MAP[i][k];
				if (MAP[i][k] == 2048)
				{
					return 0;
				}
				for (t = i - 1; t > 0; t--)
				{
					MAP[t][k] = MAP[t - 1][k];
					MAP[t - 1][k] = 0;
					flag = 1;
				}
			}
		}
	}
	if (flag != 0)
	{
		add(2);
	}
	return 1;
}
int movlif(void)
{
	int i,k,t;
	int n = 0;
	for (i = 0; i < 4; i++)
	{
		n = 4;
		while (n--)
		{
			for (k = 0; k < 3; k++)
			{
				if(MAP[i][k] == 0)
				{
					for (t = k; t < 3; t++)
					{
						MAP[i][t] = MAP[i][t + 1];
						MAP[i][t + 1] = 0;
					}
				}
			}
		}
		for (k = 0;k < 3;k++)
		{
			if (MAP[i][k] == MAP[i][k + 1])
			{
				MAP[i][k] *= 2;
				Goal += MAP[i][k];
				if (MAP[i][k] == 2048)
				{
					return 0;
				}
				for (t = k + 1; t < 3; t++)
				{
					MAP[i][t] = MAP[i][t + 1];
					MAP[i][t + 1] = 0;
				}
			}
		}
	}
	add(3);
	return 1;
}
int movri(void)
{
	int i,k,t;
	int n = 0;
	for (i = 0; i < 4; i++)
	{
		n = 4;
		while (n--)
		{
			for (k = 3; k > 0; k--)
			{
				if(MAP[i][k] == 0)
				{
					for (t = k; t > 0; t--)
					{
						MAP[i][t] = MAP[i][t - 1];
						MAP[i][t - 1] = 0;
					}
				}
			}
		}
		for (k = 3;k > 0;k--)
		{
			if (MAP[i][k] == MAP[i][k - 1])
			{
				MAP[i][k] *= 2;
				Goal += MAP[i][k];
				if (MAP[i][k] == 2048)
				{
					return 0;
				}
				for (t = k - 1; t > 0; t--)
				{
					MAP[i][t] = MAP[i][t - 1];
					MAP[i][t - 1] = 0;
				}
			}
		}
	}
	add(4);
	return 1;
}
int GetDirection(void)
{
	fflush(stdin);//清除缓存
	char key;
	key = getch();


	int flag = 1;


	if (key == 'w')//获取输入方向
	{
		flag = movup();
	}
	else if (key == 's')
	{
		flag = movdow();
	}
	else if (key == 'a')
	{
		flag = movlif();
	}
	else if (key == 'd')
	{
		flag = movri();
	}

	if (flag == 0)//达成2048
	{
		system("CLS");
		printf (" Congratulation!!!\n");
	}
	return flag;
}
int GameOver (void)
{
	int i,k;
	for (i = 0; i < 4; i++)
	{
		for (k = 1; k < 4; k++)
		{
			if (MAP[i][k - 1] == MAP[i][k])//左右卡死
			{
				return 0;
			}
		}
	}
	for (i = 0; i < 4; i++)
	{
		for (k = 1; k < 4; k++)
		{
			if (MAP[k - 1][i] == MAP[k][i])//上下卡死
			{
				return 0;
			}
		}
	}
	system("CLS");
	printf ("Game Over！\n");
	return 1;
}
void printGameMap (void)
{
	printf("Explain:W = UP\tA = LEFT\tS = DOWN\tD = RIGHT\n");
	printf("Goal：%d\n",Goal);
	printf("\t┏━━┳━━┳━━┳━━┓\n");
	printf("\t┃%4d┃%4d┃%4d┃%4d┃\n",MAP[0][0],MAP[0][1],MAP[0][2],MAP[0][3]);
	printf("\t┣━━╋━━╋━━╋━━┫\n");
	printf("\t┃%4d┃%4d┃%4d┃%4d┃\n",MAP[1][0],MAP[1][1],MAP[1][2],MAP[1][3]);
	printf("\t┣━━╋━━╋━━╋━━┫\n");
	printf("\t┃%4d┃%4d┃%4d┃%4d┃\n",MAP[2][0],MAP[2][1],MAP[2][2],MAP[2][3]);
	printf("\t┣━━╋━━╋━━╋━━┫\n");
	printf("\t┃%4d┃%4d┃%4d┃%4d┃\n",MAP[3][0],MAP[3][1],MAP[3][2],MAP[3][3]);
	printf("\t┗━━┻━━┻━━┻━━┛\n");
}
int main()
{

	printf ("Enter any key to star:");
	
	char s;
	while (scanf ("%c",&s) != 0/*按任意键开始游戏*/)
	{
		memset (MAP,0,sizeof (MAP));//初始化地图
		Goal = 0;					//初始化得分
		system("CLS");
		add(0);
		printGameMap();				//打印地图
		while (GetDirection()/*获取移动方向*/)
		{
			fflush(stdin);//清除缓存
			system("CLS");
			printGameMap();
			if (GameOver() == 1)
			{
				break;
			}
		}
		printf ("Enter any key to continue.\nEnter zero to exit.\n");
	}

	return 0;
}