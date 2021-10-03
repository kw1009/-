# Lab3 使用超音波感測器 + LED控制, 常用的C語言程式介紹

### 如何使用目錄
<a name="000"/>

#### 目錄

##### [Lab 3-1 超音波感測器 ](#001)
##### [Lab 3-2 超音波感測器 + LED ](#002)
##### [Lab 3-3 九九乘法表應用 ](#003)

<a name="001"/>

### Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output 

### 用法一
![螢幕擷取畫面 2021-09-19 101731](https://user-images.githubusercontent.com/89327102/133913287-1bbceb93-6d6b-41f1-b85d-9182ae35fa4a.jpg)
### 用法二
![螢幕擷取畫面 2021-09-19 102914](https://user-images.githubusercontent.com/89327102/133913438-d50e9c6f-7d78-422b-9d1a-6b8828950498.jpg)

### 程式

````c
int inches = 0;

int cm = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);

}

void loop()
{
  // measure the ping time in cm
  cm = 0.01723 * readUltrasonicDistance(7, 7);
  // convert to inches by dividing by 2.54
  inches = (cm / 2.54);
  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  Serial.println("cm");
  delay(100); // Wait for 100 millisecond(s)
}
````
<a name="002"/>
### Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 緑色LED: 亮<270cm, 藍色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output

![螢幕擷取畫面 2021-09-26 100801](https://user-images.githubusercontent.com/89327102/134790768-ab79f95f-8ab7-47db-9457-70e270d6b439.jpg)

### 程式

````c
int cm = 0;

void LED(int RH, int BH, int GH)
{
  analogWrite(12, RH);
  analogWrite(10, BH);
  analogWrite(9, GH);
}

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);
  pinMode(9, OUTPUT); // G
  pinMode(10, OUTPUT);// B
  pinMode(12, OUTPUT);// R
}

void loop()
{
  cm = 0.01723 * readUltrasonicDistance(7, 7);
  Serial.print(cm);
  Serial.println("cm");
  delay(100);
  
 if(cm < 70)
	LED(255,0,0);
  else if(cm > 270)
  	LED(0,255,0);
  else 
  	LED(0,0,255);
 
}
 ````
<a name="003"/>
### Lab 3-3: Arudino常用的C語言程式介紹與實作

![image](https://user-images.githubusercontent.com/89327102/134792132-9f4f1b94-aaf8-48e9-9476-a431a93047df.png)


### 程式

````c
int result, result2, result3;
String d0 = "****** 9X9 Multiplication table ******";
String d1, d2, d3;
void setup()
{
  pinMode(12, OUTPUT);   // R
  pinMode(9, OUTPUT);    // G
  
  Serial.begin(9600);

}

void loop()
{
  int aa = 0;

  Serial.println(d0); 
  
  digitalWrite(12, HIGH);
  analogWrite(9, aa); 
  
  for (int i=1;i<=9; i=i+3){
    for (int j=1;j<=9; j++){
      
      result = i*j;
      result2 = (i+1)*j;
      result3 = (i+2)*j;
      
      d1 = String(String(i) + "X" + String(j) + "=" + String(result));
      d2 = String(String(i+1) + "X" + String(j) + "=" + String(result2));
      d3 = String(String(i+2) + "X" + String(j) + "=" + String(result3));
      
      Serial.println(d1 + ", " + d2 + ", " + d3);
      
      aa+=1;
      
      delay(100);
    } // loop j
    analogWrite(9, aa*3); 
    Serial.println("");
  } // loop i

  digitalWrite(12, LOW);
  analogWrite(9, 255); 
  delay(500);	
  analogWrite(9, 0);
}
````
