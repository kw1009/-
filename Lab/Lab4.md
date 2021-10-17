# Lab4 七段顯示器, LCD 顯示器 + 超音波感測器

#### 目錄
<a name="000"/>
##### [4-1 用七段顯示器來顯示數字8]<a name="001"/>





<a name="001"/>
## Lab 4-1 用七段顯示器來顯示數字"8."

![螢幕擷取畫面 2021-10-03 102341](https://user-images.githubusercontent.com/89327102/135737256-6ede2b6c-d94f-4103-8043-75bfecfa2595.jpg)

### 程式

````c
void setup()
{
for(int x = 1; x < 9; x++) {
pinMode(x,OUTPUT);
}
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
digitalWrite(1, a);
digitalWrite(2, b);
digitalWrite(3, c);
digitalWrite(4, d);
digitalWrite(5, e);
digitalWrite(6, f);
digitalWrite(7, g);
digitalWrite(8, h);
delay(200);
}

void loop()
{
//    a, b, c, d, e, f, g, h
seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
}

````
##  Lab 4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒

![螢幕擷取畫面 2021-10-03 103917](https://user-images.githubusercontent.com/89327102/135737494-98935a12-e329-4968-b4b0-9cc86543ba87.jpg)

### 程式

````c
void setup()
{
for(int x = 1; x < 9; x++) {
pinMode(x,OUTPUT);
}
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
digitalWrite(1, a);
digitalWrite(2, b);
digitalWrite(3, c);
digitalWrite(4, d);
digitalWrite(5, e);
digitalWrite(6, f);
digitalWrite(7, g);
digitalWrite(8, h);
delay(200);
}

void loop()
{
//    a, b, c, d, e, f, g, h
seg71(0, 0, 0, 0, 0, 0, 0, 1); // .
seg71(0, 1, 1, 0, 0, 0, 0, 0); // 1
seg71(1, 1, 0, 1, 1, 0, 1, 0); // 2
seg71(1, 1, 1, 1, 0, 0, 1, 0); // 3
seg71(0, 1, 1, 0, 0, 1, 1, 0); // 4
seg71(1, 0, 1, 1, 0, 1, 1, 0); // 5
seg71(1, 0, 1, 1, 1, 1, 1, 0); // 6
seg71(1, 1, 1, 0, 0, 0, 0, 0); // 7
seg71(1, 1, 1, 1, 1, 1, 1, 0); // 8
seg71(1, 1, 1, 1, 0, 1, 1, 0); // 9
seg71(1, 1, 1, 1, 1, 1, 0, 0); // 0
 
  
}
````

## Lab 4-3 LCD顯示"Hello" + 你的英文名字

![螢幕擷取畫面 2021-10-17 095430](https://user-images.githubusercontent.com/89327102/137607323-ed86b1f9-0656-4533-9053-602d6348518e.jpg)

### 程式

````C
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, Kevin!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(millis() / 100);
}
````

## Lab 4-4 整合超音波感測器 + LCD

1. **將超音波感測器傳回的距離, 在LCD上面顯示** 
2. **同時也和之前的實作一樣, 在序列輸出** 
3. **另外, 當物體的距離小於150cm時, 則亮紅色LED, 否則亮綠色LED**

![螢幕擷取畫面 2021-10-17 103417](https://user-images.githubusercontent.com/89327102/137608397-232ba439-0977-4559-ae82-85cde6ad2497.jpg)


### 程式
````c

float  duration; // time taken by the pulse to return back
float  dd; // oneway distance travelled by the pulse

int G = 8;
int R = 9;

#define echo 7
#define trig 7

#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  Serial.begin(9600);
  digitalWrite(G, OUTPUT);
  digitalWrite(R, OUTPUT);
  lcd.begin(16, 2);
  lcd.print("Distance, cm: ");
}

void time_Measurement()
  { 
    pinMode(trig, OUTPUT);
    digitalWrite(trig, LOW);
    delayMicroseconds(2);  
    digitalWrite(trig, HIGH);
    delayMicroseconds(10);
    digitalWrite(trig, LOW);
    pinMode(echo, INPUT);  
    duration = pulseIn(echo, HIGH);
  }

void loop() {
  time_Measurement();
  dd = duration * 0.01723;
  
  Serial.print("Distance, cm: ");
  Serial.print(dd);
  Serial.println();
  
  if(dd<150)
  {
    digitalWrite(G, 0);
    digitalWrite(R, 1);
  }
  else
  {
    digitalWrite(G, 1);
    digitalWrite(R, 0);    
  }
  
  lcd.setCursor(0, 1);
  lcd.print(dd);
  
  delay(200); 
}
