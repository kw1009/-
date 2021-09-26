# Lab3 使用超音波感測器 + LED控制

## Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output 

### 用法一
![螢幕擷取畫面 2021-09-19 101731](https://user-images.githubusercontent.com/89327102/133913287-1bbceb93-6d6b-41f1-b85d-9182ae35fa4a.jpg)
### 用法二
![螢幕擷取畫面 2021-09-19 102914](https://user-images.githubusercontent.com/89327102/133913438-d50e9c6f-7d78-422b-9d1a-6b8828950498.jpg)

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

## Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 緑色LED: 亮<270cm, 藍色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output








