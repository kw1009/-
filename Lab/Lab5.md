# Lab5 Servo伺服馬達, 溫度感應器 + LCD 顯示器





## Lab 5-1 請使用兩個伺服馬達同步從 0 度逐步掃描到 180 度之後再逐步掃描回0度, 每步的間隔時間為50ms (0.05秒)

![螢幕擷取畫面 2021-10-24 095705](https://user-images.githubusercontent.com/89327102/138576953-a1f11f79-dd56-438c-8edb-3cef1a054d20.jpg)


````c

#include <Servo.h>

int pos = 0;

Servo servo_8;
Servo servo_9;


void setup()
{
  
  servo_8.attach(8, 500, 2500);
  servo_9.attach(9, 500, 2500);

}

void loop()
{
 
  for (pos = 0; pos <= 180; pos += 1) {
    
    servo_8.write(pos);
    servo_9.write(pos);
   
    delay(15); 
  }
  for (pos = 180; pos >= 0; pos -= 1) {
    
    servo_8.write(pos);
    servo_9.write(pos);
  
    delay(15); 
  }
}
````

