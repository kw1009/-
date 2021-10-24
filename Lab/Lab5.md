# Lab5 Servo伺服馬達, 溫度感應器 + LCD 顯示器

#### 目錄
<a name="000"/>

##### [5-1 使用伺服器馬達進行同步](#001)
##### [5-2 使用溫度感應器讓不同燈泡發亮](#002)

<a name="001"/>

## Lab 5-1 請使用兩個伺服馬達同步從 0 度逐步掃描到 180 度之後再逐步掃描回0度, 每步的間隔時間為50ms (0.05秒)

![螢幕擷取畫面 2021-10-24 095705](https://user-images.githubusercontent.com/89327102/138576953-a1f11f79-dd56-438c-8edb-3cef1a054d20.jpg)


### 程式
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

<a name="002"/>

## Lab 5-2 LCD顯示溫度感應器的溫度;若溫度<38 綠LED亮; 若大於38度, 紅色LED亮。

![螢幕擷取畫面 2021-10-24 104743](https://user-images.githubusercontent.com/89327102/138578238-1126e43a-83cb-4135-9717-0c2faa78e363.jpg)

### 程式

````c
#include <LiquidCrystal.h>

int G = 8;
int R = 9;
int reading = 0;
float voltage = 0.0;
float tempC = 0.0;

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  lcd.begin(16, 2);
  Serial.begin(9600);	
  pinMode(A1, INPUT);

}

void loop() {
  reading = analogRead(A1);
  lcd.setCursor(0,0);  
  lcd.print("TMP Sensor Demo");
  voltage = (reading/1024.0)*5;
  tempC = (voltage-0.5)*100;

  if(tempC<38)
  {
    digitalWrite(G, 1);
    digitalWrite(R, 0);
  }
  else
  {
    digitalWrite(G, 0);
    digitalWrite(R, 1);    
  }

  lcd.setCursor(0,1);
  lcd.print("Tmp:");
  lcd.print(tempC);
  lcd.print(" C");
  delay(500);
  lcd.clear();
  Serial.println(reading);
  Serial.println(voltage);  
}
````


