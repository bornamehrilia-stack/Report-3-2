# Report-3-2




---

# گزارش پروژه: تاس الکترونیکی با آردوینو

## ۱. مقدمه  
در این پروژه، یک **تاس الکترونیکی** ساخته شده است که با استفاده از ۶ عدد LED و یک دکمه، عددی تصادفی بین ۱ تا ۶ را نمایش می‌دهد. .


## ۳. قطعات مورد استفاده  
- برد آردوینو Uno  
- ۶ عدد LED   
- ۶ عدد مقاومت ۲۲۰ اهم (برای هر LED یک عدد)  
- یک دکمه (Push Button)(در این مورد ، بجای استفاده از push button، ما a0 را مستقیم به زمین وصل کرده و برای فعال شدن برنامه، دکمه قرمز آردوینو را کلیک میکنیم)
- برد برد (Breadboard)  
- سیم‌های جامپر (jumper wires)

## ۴. نحوه‌ی ساخت مدار  
- **LEDها**:  
  - هر LED به یکی از پین‌های دیجیتال ۲ تا ۷ آردوینو متصل شده است.  
  - هر LED با یک مقاومت ۲۲۰ اهم به GND متصل شده است.  
- **دکمه**:  
  - دکمه ای در این مورد استفاده نشده است.ما از a0 مستقیم به زمین چصل کردیم.  
  - دکمه با یک مقاومت pull-down (مثلاً ۱۰k اهم) به GND متصل شده است تا در حالت عادی ولتاژ پایین (LOW) داشته باشد.



## ۵. کد برنامه :

```cpp
int led1 = 2;
int led2 = 3;
int led3 = 4;
int led4 = 5;
int led5 = 6;
int led6 = 7;

int val, i;
long unsigned randNumber;

void setup() {
  Serial.begin(9600);
  randomSeed(analogRead(0));  // تنظیم بذر تصادفی با استفاده از نویز آنالوگ

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);
  pinMode(led5, OUTPUT);
  pinMode(led6, OUTPUT);

  pinMode(A0, INPUT);  // دکمه به A0 متصل شده است
}

void loop() {
  if (digitalRead(A0) == LOW) {  // اگر دکمه فشرده شده باشد
    randNumber = random(1, 7);   // تولید عدد تصادفی بین ۱ تا ۶ (عدد ۷ شامل نمی‌شود)

    Serial.print("randNumber=");
    Serial.println(randNumber);

    // خاموش کردن تمام LEDها
    for (i = 2; i <= 7; i++) {
      digitalWrite(i, LOW);
    }

    // روشن کردن LEDهای مربوط به عدد تصادفی
    switch (randNumber) {
      case 1:
        digitalWrite(led1, HIGH);
        break;
      case 2:
        digitalWrite(led2, HIGH);
        break;
      case 3:
        digitalWrite(led3, HIGH);
        break;
      case 4:
        digitalWrite(led4, HIGH);
        break;
      case 5:
        digitalWrite(led5, HIGH);
        break;
      case 6:
        digitalWrite(led6, HIGH);
        break;
    }

    delay(2000);  // نمایش عدد برای ۲ ثانیه
  }
}
```



## ۶. نحوه‌ی کارکرد  
- پس از آپلود کد، دکمه را فشار دهید.  
- یک عدد تصادفی بین ۱ تا ۶ تولید می‌شود و LED مربوطه روشن می‌شود.  
- عدد برای ۲ ثانیه نمایش داده می‌شود و سپس خاموش می‌شود.  
- برای ریست کردن و تولید عدد جدید، دوباره دکمه را فشار دهید.

## ۷. نتایج  
- با فشار دادن دکمه(و یا در این مورد، وقتی که پوش باتون نداریم، با وصل کردن a0 به زمین و زدن دکمه قرمز ریست کردن قژعه) ، یک LED روشن می‌شود که نشان‌دهنده‌ی عدد تصادفی است.  
- اعداد به صورت تصادفی و با احتمال یکسان تولید می‌شوند.  


---
