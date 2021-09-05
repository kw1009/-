# Lab1: LED Practice

## 在TinkerCAD開一個新的Circuit, 加上一個外部的LED, 並且ON (亮) 1秒, OFF(滅) 1秒

![螢幕擷取畫面 2021-08-29 100708](https://user-images.githubusercontent.com/89327102/131235843-8b5f62d0-4cf0-4cc6-b454-9489f1bd436a.jpg)
## 在TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, ON (亮) 0.5秒, OFF(滅) 0.5秒

### 程式
````C
/*
  This program blinks pin 13 of the Arduino (the
  built-in LED)
*/

void setup()
{
  pinMode(13, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(9, OUTPUT);  
}

void loop()
{
  
  digitalWrite(13, HIGH);
  delay(500);
  digitalWrite(13, LOW);
  delay(500);
  digitalWrite(11, HIGH);
  delay(500);
  digitalWrite(11, LOW);  
  delay(500); 
  digitalWrite(9, HIGH);
  delay(500);
  digitalWrite(9, LOW);  
  delay(500); 
}
````

![螢幕擷取畫面 2021-08-29 103439](https://user-images.githubusercontent.com/89327102/131236340-6aa4a6ea-8a24-49a1-8618-5e65afd68bab.jpg)
## 在TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, 讓LED ON, OFF的順序為R >> G >> B >> G >> R .... 無限循環

![螢幕擷取畫面 2021-09-05 091139](https://user-images.githubusercontent.com/89327102/132111729-2ef75fd7-43e5-4710-a5b1-d4caa7d0e6ce.jpg)

````C
/*
  This program blinks pin 13 of the Arduino (the
  built-in LED)
*/
void setup() 
{
  pinMode(13,OUTPUT);
}

void loop() 
{
  digitalWrite(13,HIGH);
  delay(500);
  digitalWrite(13,LOW);
  delay(500);
  digitalWrite(11,HIGH);
  delay(500);
  digitalWrite(11,LOW);
  delay(500);
  digitalWrite(9,HIGH);
  delay(500);
  digitalWrite(9,LOW);
  delay(500);
  digitalWrite(11,HIGH);
  delay(500);
  digitalWrite(11,LOW);
  delay(500);
 
}
````
