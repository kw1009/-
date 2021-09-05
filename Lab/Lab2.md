# Lab2 會呼吸的RGB LED,  按鍵控制, 狀態輸出

## 2-1 analogWrite(): 並且觀查LED亮度變化是否有像"呼吸的效果"和示波器的波形有什麼關連性?

![image](https://user-images.githubusercontent.com/89327102/132112778-84441431-1758-4613-841f-012d42b53cea.png)

````
int brightness = 0;

void setup()
{
  pinMode(9, OUTPUT);
}

  for (brightness = 0; brightness <=255; brightness +=5){
       analogWrite(9, brightness);
       delay(30); 
  }    
  
  for (brightness = 255; brightness >=0; brightness -=5){
       analogWrite(9, brightness);
       delay(30); 
  }
}
````
## 2-2 RGB LED燈全彩模組, 分別讓LED輪流表現正紅、正綠、正藍，三個顏色，時間間隔1秒鐘。並且觀查LED顏色和波形或是電壓有什麼關連性? 可將個人說明在更新GitHub時一起加入

![螢幕擷取畫面 2021-09-05 221227](https://user-images.githubusercontent.com/89327102/132130159-f9dc4170-d263-4ca5-90d7-becb6a0b3daf.jpg)

````
const int R = 9 ;
const int G = 10 ;
const int B = 11 ;

  void setup()
{
  pinMode(R, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(B, OUTPUT);
}

void loop()
{
  analogWrite(R,255);
  analogWrite(G,0);
  analogWrite(B,0);
    
    delay(1000);
  analogWrite(R,0);
  analogWrite(G,255);
  analogWrite(G,255);
    
    delay(1000); 
  analogWrite(R,0);
  analogWrite(G,0);
  analogWrite(B,255);
  
   delay(1000); 
}
````
