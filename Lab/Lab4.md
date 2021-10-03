# Lab4 七段顯示器, LCD 顯示器 + 超音波感測器

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

````c

##  Lab 4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒
