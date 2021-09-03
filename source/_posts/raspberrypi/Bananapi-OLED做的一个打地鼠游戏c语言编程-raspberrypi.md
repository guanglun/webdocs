---
title: Bananapi+OLED做的一个打地鼠游戏c语言编程(raspberrypi)
date: 2021-05-10 10:05:59
categories: raspberrypi
tags: 
    - raspberrypi 
---
# Whac-a-BPI  
[Git](https://github.com/guanglun/Whac-a-BPI)

* 大学期间2015年1月玩Bananapi的时候写的，年代久远，现在挖出来保存一下
* game1.c是游戏源码
* oled.c是OLED的驱动demo

## 说明

* BPI是对拍死的BPI的计数,对应最终的成绩
* RANK是难度 数值越低难度越高 每当打死10个BPI以后就会减一即难度高一级 默认初始化RANK等于15
* DIE是存在的BPI数量,一旦数量大于或者等于5就GameOver了..........
* 最后会把最终成绩打印在屏幕和终端上

## 编译执行

```
gcc game1.c -o game1 -lwiringPi
./game1
```

贴上主函数  

```c
int main(int argc,char **argv)
{
    byte xx=0,yy=0,BPI[8]={0,0,0,0,0},A_BPI_Start[8]={0,0,0,0,0},A_BPI_Stop[8]={0,0,0,0,0},A_BPI_ii=0;
    byte AA0=0,AA1=0,AA2=0,AA3=0,AA4=0,AA5=0,AA6=0,AA7=0,Rank=15,NumString_Rank[10]={0,0,0,0,0,0,0,0,0,0},NumString_BPI[10]={0,0,0,0,0,0,0,0,0,0};
    byte NumString_Die_Cnt[10];
    byte Die_Cnt[8]={0,0,0,0,0},Die_Num=0,ca=0;
    dword CNT=1,Rand_Cnt=0,BPI_Cnt=0;
    pthread_t pid1, pid2; //thread
 
    LCD_Init();
 
     
 
    Num2String(BPI_Cnt,3,NumString_BPI);
    Num2String(Rank,3,NumString_Rank);
    if(pthread_create(&pid1, NULL, thread_mice, NULL))
    {
        return -1;
    }
    Draw_BMP(bananapi);
    sleep(2);
    Draw_BMP(gImage_start);
    sleep(1);
    Draw_BMP(gImage_start);
    sleep(1);
    Draw_BMP(gImage_anykey);
     
    while(1)
    {
         if(Left_Check==1)
         {
             Left_Check=0;
             break;
         }
    }
    srand((int) time(0));
    while(1)
    {
      if(Pos_Mark)
      {
           
          if(X_LCD_Pos>119)X_LCD_Pos=119;
          if(Y_LCD_Pos>55)Y_LCD_Pos=55;
           
          old_X_LCD_Pos=X_LCD_Pos;
          old_Y_LCD_Pos=Y_LCD_Pos;
          Pos_Mark = 0;
      }
       
      CNT++;
      Rand_Cnt++;
      Num2String(Die_Num,1,NumString_Die_Cnt);
      LCD_W_BMP(0,16,24,24,gImage_A_BPI[BPI[0]],1);
      LCD_W_BMP(30,16,24,24,gImage_A_BPI[BPI[1]],1);
      LCD_W_BMP(60,16,24,24,gImage_A_BPI[BPI[2]],1);
      LCD_W_BMP(90,16,24,24,gImage_A_BPI[BPI[3]],1);
       
      LCD_W_BMP(0,40,24,24,gImage_A_BPI[BPI[4]],1);
      LCD_W_BMP(30,40,24,24,gImage_A_BPI[BPI[5]],1);
      LCD_W_BMP(60,40,24,24,gImage_A_BPI[BPI[6]],1);
      LCD_W_BMP(90,40,24,24,gImage_A_BPI[BPI[7]],1);
       
      LCD_P6x8Str(0,0,"BPI:",1);
      LCD_P6x8Str(0,1,"RANK:",1);
      LCD_P6x8Str(60,1,"DIE:",1);
      LCD_P6x8Str(60,0,"Whac-a-BPI",1);
      LCD_P6x8Str(30,0,NumString_BPI,1);
      LCD_P6x8Str(30,1,NumString_Rank,1);
      LCD_P6x8Str(90,1,NumString_Die_Cnt,1);
       
      LCD_W_BMP(X_LCD_Pos,Y_LCD_Pos,8,8,OLED_mice,1);
       
      Draw_BMP(LCD_Buffer);
      LCD_W_BMP(old_X_LCD_Pos,old_Y_LCD_Pos,8,8,OLED_mice,0);
       
       
       
      LCD_P6x8Str(0,0,"BPI:",0);
      LCD_P6x8Str(0,1,"RANK:",0);
      LCD_P6x8Str(90,1,"DIE:",0);
      LCD_P6x8Str(60,0,"Whac-a-BPI",1);
      LCD_P6x8Str(30,0,NumString_BPI,0);
      LCD_P6x8Str(30,1,NumString_Rank,0);
      LCD_P6x8Str(80,1,NumString_Die_Cnt,0);
       
      LCD_W_BMP(0,16,24,24,gImage_A_BPI[BPI[0]],0);
      LCD_W_BMP(30,16,24,24,gImage_A_BPI[BPI[1]],0);
      LCD_W_BMP(60,16,24,24,gImage_A_BPI[BPI[2]],0);
      LCD_W_BMP(90,16,24,24,gImage_A_BPI[BPI[3]],0);
       
      LCD_W_BMP(0,40,24,24,gImage_A_BPI[BPI[4]],0);
      LCD_W_BMP(30,40,24,24,gImage_A_BPI[BPI[5]],0);
      LCD_W_BMP(60,40,24,24,gImage_A_BPI[BPI[6]],0);
      LCD_W_BMP(90,40,24,24,gImage_A_BPI[BPI[7]],0);
         
      if(Rand_Cnt >= Rank)
      {
          Rand_Cnt=0;
          switch(rand()%8)
          {
              case 0:if(A_BPI_Stop[0]==0) A_BPI_Stop[0]=1,A_BPI_Start[0]=1;break;
              case 1:if(A_BPI_Stop[1]==0) A_BPI_Stop[1]=1,A_BPI_Start[1]=1;break;
              case 2:if(A_BPI_Stop[2]==0) A_BPI_Stop[2]=1,A_BPI_Start[2]=1;break;
              case 3:if(A_BPI_Stop[3]==0) A_BPI_Stop[3]=1,A_BPI_Start[3]=1;break;
              case 4:if(A_BPI_Stop[4]==0) A_BPI_Stop[4]=1,A_BPI_Start[4]=1;break;
              case 5:if(A_BPI_Stop[5]==0) A_BPI_Stop[5]=1,A_BPI_Start[5]=1;break;
              case 6:if(A_BPI_Stop[6]==0) A_BPI_Stop[6]=1,A_BPI_Start[6]=1;break;
              case 7:if(A_BPI_Stop[7]==0) A_BPI_Stop[7]=1,A_BPI_Start[7]=1;break;
              default:break;      
          }
      }
      if(CNT==2)
      {
          for(A_BPI_ii=0;A_BPI_ii<8;A_BPI_ii++)
          {
              if(A_BPI_Start[A_BPI_ii]==1)  
              {
                    if(BPI[A_BPI_ii]<4)BPI[A_BPI_ii]++;
                    else
                    {
                        Die_Num++;
                        A_BPI_Start[A_BPI_ii]=2;
                    }
                         
              }        
              if(A_BPI_Stop[A_BPI_ii]==2)
              {
                  if(BPI[A_BPI_ii]<8)
                      BPI[A_BPI_ii]++;
                  else
                  {
                        BPI[A_BPI_ii]=0;
                        A_BPI_Stop[A_BPI_ii]=0;
                        A_BPI_Start[A_BPI_ii]=0;
                  }
              }
                       
          }
          if(Right_Check==1)
          {
              LCD_Init();
              Right_Check=0;
          }
          if(Left_Check==1)
          {
              if( 4 <Left_Check_X&& 24 >Left_Check_X&& 18 <Left_Check_Y&&35>Left_Check_Y&&A_BPI_Stop[0]==1)
              {
                      A_BPI_Stop[0]=2;
                      BPI[0]=5;
                      BPI_Cnt++;
                      Die_Num--;
                      ca=1;
              }
              else if( 34 <Left_Check_X&& 49 >Left_Check_X&& 18 <Left_Check_Y&& 35 >Left_Check_Y&&A_BPI_Stop[1]==1)
              {
                  A_BPI_Stop[1]=2;
                  BPI[1]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }  
              else if( 63 <Left_Check_X&& 80 >Left_Check_X&& 18 <Left_Check_Y&& 35 >Left_Check_Y&&A_BPI_Stop[2]==1)
              {
                  A_BPI_Stop[2]=2;
                  BPI[2]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }  
              else if( 93 <Left_Check_X&& 109 >Left_Check_X&& 18 <Left_Check_Y&& 35 >Left_Check_Y&&A_BPI_Stop[3]==1)
              {
                  A_BPI_Stop[3]=2;
                  BPI[3]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }  
              else if( 4 <Left_Check_X&& 24 >Left_Check_X&& 43 <Left_Check_Y&&67>Left_Check_Y&&A_BPI_Stop[4]==1)
              {
                  A_BPI_Stop[4]=2;
                  BPI[4]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }
              else if( 34 <Left_Check_X&& 49 >Left_Check_X&& 43 <Left_Check_Y&& 67 >Left_Check_Y&&A_BPI_Stop[5]==1)
              {
                  A_BPI_Stop[5]=2;
                  BPI[5]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }  
              else if( 63 <Left_Check_X&& 80 >Left_Check_X&& 43 <Left_Check_Y&& 67 >Left_Check_Y&&A_BPI_Stop[6]==1)
              {
                  A_BPI_Stop[6]=2;
                  BPI[6]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }  
              else if( 93 <Left_Check_X&& 109 >Left_Check_X&& 43 <Left_Check_Y&& 67 >Left_Check_Y&&A_BPI_Stop[7]==1)
              {
                  A_BPI_Stop[7]=2;
                  BPI[7]=5;
                  BPI_Cnt++;
                  Die_Num--;
                  ca=1;
              }  
              if(ca)
              {
                  if(!(BPI_Cnt%11)) Rank--;
                  Num2String(BPI_Cnt,3,NumString_BPI);
                  Num2String(Rank,3,NumString_Rank);
                  Left_Check=0;
                  ca=0;
              }
          }
 
          CNT=0;
      }
      if(Die_Num>=5)
      {
       
            Draw_BMP(gImage_gameover);
            LCD_P8x16Str(75,5,NumString_BPI);
            printf("Game Score:%d\n",BPI_Cnt);
            return 0;
      }
    }
    return 0;
}
```
使用软SPI驱动OLED,有时会出现花屏的现象,一直没查明白这个bug原因也就先这样了....视频里也可以看到突然会全屏花.为了继续游戏我把右击鼠标写成了对OLED重新初始化一次,所以花屏以后需要再右击一下就OK啦,就当这是给游戏提高难度了吧........
源码见[Git](https://github.com/guanglun/Whac-a-BPI)  

需要wiringBPI的库,不知道的可以参考这里
https://www.cirmall.com/bbs/thread-40235-1-2.html  
  
![i](https://github.com/guanglun/Whac-a-BPI/blob/master/show1.png?raw=true)
![i](https://github.com/guanglun/Whac-a-BPI/blob/master/show2.png?raw=true)
![i](https://github.com/guanglun/Whac-a-BPI/blob/master/show3.png?raw=true)
![i](https://github.com/guanglun/Whac-a-BPI/blob/master/show4.png?raw=true)
![i](https://github.com/guanglun/Whac-a-BPI/blob/master/show5.png?raw=true)