# flappy Bird

问题 鸟图片按照书上代码遮挡后会发黑 想显示过了几根杆子得分  显示乱码 但是不强制转格式已经无法按照原先代码跑通 整体代码理解没有问题

```
#include<stdio.h>
#include<graphics.h>
#include<conio.h>
#pragma comment(lib,"Winmm.lib")
#define n 10
#define high 600
#define width 350


int score;
int bird_x, bird_y;//小鸟位置
int bar_up_x[n], bar_up_y[n];//上挡板的位置
int bar_down_x[n], bar_down_y[n];//下挡板的位置
IMAGE img_bd1, img_bd2, img_bk, img_bar_up1, img_bar_up2, img_bar_down1, img_bar_down2;




void starup()//游戏初始化 
{
	int i;
	int k = 1;//距离的倍数
	int l = 1;//距离的倍数
	mciSendString(TEXT("open E:\\background.mp3 alias bkmusic"), NULL, 0, NULL);//播放背景音乐
	mciSendString(TEXT("play bkmusic repeat"), NULL, 0, NULL);	//循环播放


	initgraph(width, high);
	loadimage(&img_bk, TEXT("E:\\background.jpg"));//读取图片到img对象中
	loadimage(&img_bd1, TEXT("E:\\bird1.jpg"));
	loadimage(&img_bd2, TEXT("E:\\flappy birdbird2.jpg"));
	loadimage(&img_bar_up1, TEXT("E:\\bar_up1.gif"));
	loadimage(&img_bar_up2, TEXT("E:\\bar_up2.gif"));
	loadimage(&img_bar_down1, TEXT("E:\\bar_down1.gif"));
	loadimage(&img_bar_down2, TEXT("E:\\bar_down2.gif"));

	bird_x = 50;
	bird_y = 200;

	bar_up_x[0] = 300;
	bar_down_x[0] = 300;
	bar_up_y[0] = -300;
	bar_down_y[0] = 400;

	score = 0;

	for (i = 1; i < n; i++)
	{
		k++;
		bar_up_x[i] = bar_up_x[0] * k;
		bar_up_y[i] = -300 - (rand() % 100);

		bar_down_x[i] = bar_down_x[0] * k;
		bar_down_y[i] = 400 + (rand() % 100);
	}

	BeginBatchDraw();
}




void show()
{
	int i, j;

	putimage(0, 0, &img_bk); //显示背景
	for (i = 0; i < n; i++)
	{
		putimage(bar_up_x[i], bar_up_y[i], &img_bar_up1, NOTSRCERASE);//显示上一半的障碍物
		putimage(bar_up_x[i], bar_up_y[i], &img_bar_up2, SRCINVERT);
	}


	for (j = 0; j < n; j++)
	{
		putimage(bar_down_x[j], bar_down_y[j], &img_bar_down1, NOTSRCERASE);//显示下一半的障碍物
		putimage(bar_down_x[j], bar_down_y[j], &img_bar_down2, SRCINVERT);
	}
	putimage(bird_x, bird_y, &img_bd1, NOTSRCERASE);//显示小鸟
	putimage(bird_x, bird_y, &img_bd2, SRCINVERT);

	/*outtextxy(10, 10, TEXT("得分：自己数！"));*/
	char s[5];
	sprintf_s(s,"%d",score);
	outtextxy(50,10,score);

	FlushBatchDraw();
	Sleep(25);
}



void updataWithoutInput()//用户无关设置
{
	int i, j;

	for (i = 0; i < n; i++)		//碰瓷而死
	{
		bar_up_x[i] = bar_up_x[i] - 1;
		bar_down_x[i] = bar_down_x[i] - 1;

		if ((bird_x > bar_up_x[i] - 30) && (bird_x < bar_up_x[i] + 140))
		{
			if ((bird_y < 600 + bar_up_y[i]) || (bird_y > bar_down_y[i] - 15))
			{
				EndBatchDraw();

				setfillcolor(BLACK);
				solidrectangle(0, 0, width, high);

				outtextxy(width / 2 - 30, high / 2, TEXT("游戏结束！"));
				outtextxy(width / 2 - 30, high / 2 + 50, TEXT("按任意键退出"));

				_getch();
				closegraph();
			}
		}
	}

	for (j = 0; j < n; j++)
	{
		if (bar_up_x[j] == 50)
			score++;
	}


	if (bird_y > high - 15)		//落入无底深渊die
	{
		EndBatchDraw();

		setfillcolor(BLACK);
		solidrectangle(0, 0, width, high);

		outtextxy(width / 2 - 30, high / 2, TEXT("游戏结束！"));
		outtextxy(width / 2 - 30, high / 2 + 50, TEXT("按任意键退出"));

		_getch();
		closegraph();
	}
	else
		bird_y = bird_y + 3;


}




void updataWithInput()//用户有关设置
{
	char input;
	if (_kbhit())//当按下键时执行
	{
		input = _getch();
		if (input == ' ' && bird_y > 20)
		{
			bird_y = bird_y - 60;

			mciSendString(TEXT("close jpmusic"), NULL, 0, NULL);//先把前面一次的音乐关闭
			mciSendString(TEXT("open E:\\Jump.mp3 alias jpmusic"), NULL, 0, NULL);//打开音乐
			mciSendString(TEXT("play jpmusic"), NULL, 0, NULL);//仅播放一次
		}
	}
}

void gameover()
{
	EndBatchDraw();
	_getch();
	closegraph();
}


void main()
{
	starup();//数据初始化
	while (1)//游戏循环 
	{
		show();//游戏显示 
		updataWithoutInput();//用户无关设置 
		updataWithInput(); //用户有关设置 
	}
	gameover();
}

```

# 飞机大战

问题 背景未自适应拉伸  我方飞机 子弹 敌方飞机都有几率重影 得分乱码 不能显示  abs()函数已经不能读取整形以外任何形式 无奈只能强制类型转换 在击中判定上有些问题 容易很多枪打不死 飞机爆炸 游戏结束没问题 整体流程没有问题  整体代码理解没有问题

![image-20211114235121239](H:/%E6%96%87%E4%BB%B6/IMG/image-20211114235121239.png)

![image-20211115001706383](H:/%E6%96%87%E4%BB%B6/IMG/image-20211115001706383.png)

# 双人游戏

```
#include <conio.h>
#include <graphics.h>
#include<windows.h>
#define High 480  // 游戏画面尺寸
#define Width 640
// 全局变量
int ball_x, ball_y; // 小球的坐标
int ball_vx, ball_vy; // 小球的速度
int radius; // 小球的半径
int bar1_left, bar1_right, bar1_top, bar1_bottom; // 挡板1的上下左右位置坐标
int bar2_left, bar2_right, bar2_top, bar2_bottom; // 挡板2的上下左右位置坐标
int bar_height, bar_width; // 挡板的高度、宽度

void startup()  // 数据初始化
{
	ball_x = Width / 2;
	ball_y = High / 2;
	ball_vx = 1;
	ball_vy = 1;
	radius = 20;

	bar_width = Width / 30;
	bar_height = High / 2;

	bar1_left = Width * 1 / 20;
	bar1_top = High / 4;
	bar1_right = bar1_left + bar_width;
	bar1_bottom = bar1_top + bar_height;

	bar2_left = Width * 18.5 / 20;
	bar2_top = High / 4;
	bar2_right = bar2_left + bar_width;
	bar2_bottom = bar2_top + bar_height;

	initgraph(Width, High);
	BeginBatchDraw();
}

void clean()  // 消除画面
{
	setcolor(BLACK);
	setfillcolor(BLACK);
	fillcircle(ball_x, ball_y, radius);
	fillcircle(ball_x, ball_y, radius);
	bar(bar1_left, bar1_top, bar1_right, bar1_bottom);
	bar(bar2_left, bar2_top, bar2_right, bar2_bottom);
}

void show()  // 显示画面
{
	setcolor(GREEN);
	setfillcolor(GREEN);
	fillcircle(ball_x, ball_y, radius);	// 绘制绿圆	

	setcolor(YELLOW);
	setfillcolor(YELLOW);
	bar(bar1_left, bar1_top, bar1_right, bar1_bottom);	// 绘制黄色挡板
	bar(bar2_left, bar2_top, bar2_right, bar2_bottom);

	FlushBatchDraw();
	// 延时
	Sleep(3);
}

void updateWithoutInput()  // 与用户输入无关的更新
{
	// 挡板和小圆碰撞，小圆反弹
	if (ball_x + radius >= bar2_left && ball_y + radius >= bar2_top && ball_y + radius <= bar2_bottom)
		ball_vx = -ball_vx;
	else if (ball_x - radius <= bar1_right && ball_y + radius >= bar1_top && ball_y + radius <= bar1_bottom)
		ball_vx = -ball_vx;

	// 更新小圆坐标
	ball_x = ball_x + ball_vx;
	ball_y = ball_y + ball_vy;

	if ((ball_x <= radius) || (ball_x >= Width - radius))
		ball_vx = -ball_vx;
	if ((ball_y <= radius) || (ball_y >= High - radius))
		ball_vy = -ball_vy;
}

void updateWithInput()  // 与用户输入有关的更新
{
	int step = 1;
	if (GetAsyncKeyState(0x57) & 0x8000)  // w
		bar1_top -= step;
	if ((GetAsyncKeyState(0x53) & 0x8000)) //s
		bar1_top += step;
	if ((GetAsyncKeyState(VK_UP) & 0x8000))     // 上方向键
		bar2_top -= step;
	if ((GetAsyncKeyState(VK_DOWN) & 0x8000))  // 下方向键
		bar2_top += step;

	bar1_bottom = bar1_top + bar_height;
	bar2_bottom = bar2_top + bar_height;
}

void gameover()
{
	EndBatchDraw();
	closegraph();
}

int main()
{
	startup();  // 数据初始化	
	while (1)  //  游戏循环执行
	{
		clean();  // 把之前绘制的内容取消
		updateWithoutInput();  // 与用户输入无关的更新
		updateWithInput();     // 与用户输入有关的更新
		show();  // 显示新画面
	}
	gameover();     // 游戏结束、后续处理
	return 0;
}

```



![image-20211115003205172](H:/%E6%96%87%E4%BB%B6/IMG/image-20211115003205172.png)

