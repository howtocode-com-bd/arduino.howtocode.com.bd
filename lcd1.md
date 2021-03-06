# LCD (Liquid Crystal Display) ইন্টারফেসিং (প্রথম অংশ)

LCD খুবই কমন একটি মডিউল যেটা আমরা প্রায় সবক্ষেত্রে ব্যবহৃত হতে দেখি। ডিজিটাল ঘড়ি, ক্যালকুলেটরে ইত্যাদি অনেক ক্ষেত্রেই ইনফরমেশন দেখানোর জন্য ব্যবহার করা হয়। Alphanumerical ও Graphical LCD আমরা মাইক্রোকন্ট্রলার বা আর্ডুইনো দ্বারা কন্ট্রোল করতে পারি। সবার সুবিধার্থে LCD কে কয়েকটি ভাগে উপস্থাপন করা হবে। আজকে আমরা দেখব কীভাবে একটি আলফানিউমেরিক্যাল LCD আর্ডুইনোর সাথে Hookup করে এবং সাধারণ কোন লেখা ডিস্প্লে তে শো করে।

## এই পর্বে যা যা লাগবে:

###### প্র্যাক্টিক্যালি দেখার জন্য

* আর্ডুইনো (বোর্ড ও IDE)
* `USB Cable (A to B)`
* 16x2 / 16x4 / 20x4 /.. Alphanumeric Liquid Crystal Display (LCD)
    ![lcd1](http://i.imgur.com/kXbI97m.jpg)
    ![lcd2](http://i.imgur.com/ggmeaFZ.jpg)
* `10k` Ohm Pot
* `Jumper Wires (22AWG or Premium)`
* Breadboard

> যদি আপনার LCD তে Header Pin Soldered করা না থাকে তাহলে

* Soldering Iron
* সীসা
* রঞ্জন
* Header Pin
  ![header](http://i.imgur.com/ewbYgx0.jpg)

###### ভার্চুয়ালি দেখার জন্য

* Proteus ISIS
* Arduino IDE

## LCD সেট আপ:

Alphanumeric LCD গুলো খুবই কমন, এগুলোর ১৬ টি করে পিন থাকে। ১৪ টি পিন থাকার মানে হল Backlight নেই। অর্থাৎ ১৪ টি পিন + ২ টি ব্যাকলাইটের জন্য। আপনার LCD তে কোন হেডার পিন না থাকলে আপনার নিজেরই সেটা সোল্ডার করে নিতে হবে। পর্বের শেষের দিকে সোল্ডারিং ইন্সট্রাকশন দিয়ে দেওয়া হল। 

হেডার পিন আছে বা নেই বুঝতে পারছেন না? ছবির LCD টি দেখুন, তাহলেই বুঝতে পারবেন।

**গুরুত্বপূর্ণ: আপনার LCD এর ডাইমেনশন কাজ শুরুর আগেই জেনে নিন, অর্থাৎ এটা কী 16x4, 16x2 নাকি 20x2 বা 20x4, বুঝতে না পারলে LCD টা কে আলোয়ে ধরে যে কয়টা কাল ব্লকের কলাম আর রো গণনা করুন তাহলেই পেয়ে যাবেন।** 

এইবার LCD কে আর্ডুইনোর সাথে wiring করতে হবে। LCD module এর সেম পিন দিয়ে দুই ধরণের wiring করা যায়। একটি হল `4-pin` আরেকটি `8-pin` mode। সব কিছু সিম্পল রাখার সুবিধার্থে আমরা 4-pin মোডেই কাজ করব। LCD পিন আউট টেবিলটি খুব কাজে লাগবে কাজেই সেটা একবার দেখে নেওয়া ভাল:

## LCD পিন আউট ডায়াগ্রাম:
LCD এর পিন নাম্বার কাউন্টিং শুরু হয় বামপাশ থেকে, নিচের ছবি দেখলেই পরিষ্কার হবে
![lcd_pinout](http://i.imgur.com/quPwRbt.png)

## LCD পিনআউট টেবিল

| পিন নাম্বার Pin no. | পিনের নাম Pin Name | যে কাজে ব্যবহার করা হবে Pin Purpose        |
|--------------------|--------------------|-------------------------------------------|
| 1                  | VSS                | GND Connection                            |
| 2                  | VDD                | +5V Connection                            |
| 3                  | V0                 | Contrast Adjustment                       |
| 4                  | RS                 | Register selection (Character vs Command) |
| 5                  | RW                 | Read/Write                                |
| 6                  | EN                 | Enable                                    |
| 7                  | D0                 | Data Line 0  (Unused)                     |
| 8                  | D1                 | Data Line 1 (Unused)                      |
| 9                  | D2                 | Data Line 2 (Unused)                      |
| 10                 | D3                 | Data Line 3 (Unused)                      |
| 11                 | D4                 | Data Line 4                               |
| 12                 | D5                 | Data Line 5                               |
| 13                 | D6                 | Data Line 6                               |
| 14                 | D7                 | Data Line 7                               |
| 15                 | A                  | Backlight Anode (+5V Connection)          |
| 16                 | K                  | Backlight Cathode (GND Connection)        |


## পিন কানেকশন ব্যাখ্যা

##### V0 [3rd Pin]:
* V0 পিনের কাজ হল LCD এর কন্ট্রাস্ট `Contrast` কন্ট্রোল করা। এর জন্য আমাদের একটি 10KOhm Pot ব্যবহার করতে হবে। এই পট V0 বা LCD এর ৩ নাম্বার পিনের সাথে কানেক্টেড থাকবে। পটের মাধ্যমে রেজিস্ট্যান্স পরিবর্তন করলে কন্ট্রাস্ট ও পরিবর্তিত হবে। 
    * উল্লেখ্য V0 কে যদি আমরা গ্রাউন্ডে কানেক্ট করি তাহলে ফুল কন্ট্রাস্ট পাওয়া যাবে।

##### RS [4th Pin]:
* এই পিনের কাজ হল LCD কে Command বা Character mode এ সেট করা। এটা দ্বারা LCD বুঝতে পারে যে Data Line এ আসা Data set কে সে কীভাবে কাজে লাগাবে। সেটি কি কোন কমান্ড নাকি ক্যারেক্টার?

##### RW [5th Pin]:
* এই পিনটিকে সবসময়ই আমরা গ্রাউন্ডে কানেক্ট করে রাখব। মানে LCD তে আমরা সবসময় `Write` করব।

##### EN [6th Pin]:
* EN পিনের মাধ্যমে LCD কে Data Line এর স্ট্যাটাস জানানো হয়।

##### Backlight Anode & Cathode [15th & 16th Pin]:
* আগেই বলা হয়েছে এই পিনদুটো সব LCD তে নাও থাকতে পারে। যদি থাকে তাহলে 15 কে `+5V` এর সাথে কানেক্ট করুন ও `16` কে `GND` তে।

## কম্যুনিকেশন পিন কানেকশন

LCD কম্যুনিকেশনের জন্য আমরা ৬ টা পিন ব্যবহার আর্ডুইনোর নিচের পিনগুলোর সাথে কানেক্ট করব:

| LCD Pin | Arduino Pin Number |
|---------|--------------------|
| RS      | Pin 2              |
| EN      | Pin 3              |
| D4      | Pin 4              |
| D5      | Pin 5              |
| D6      | Pin 6              |
| D7      | Pin 7              |

## সার্কিট ডায়াগ্রাম

Arduino ও LCD কে নিচের ছবির মত করে কানেক্ট করে ফেলুন

![circuit](http://i.imgur.com/fe9WYcb.png)

## প্রোগ্রাম

যেহেতু আমরা কেবল LCD কানেকশন দিয়েছি ও টেস্ট করতে চাই, তাই আমরা সিম্পল কোড দিয়ে শুরু করব। এরপর আমরা আস্তে আস্তে জটিলের দিকে যাব। নিচের প্রোগ্রামটি LCD তে "Electroscholars" শো করবে আপনি সেখানে আপনার নাম বসিয়েও টেস্ট করে দেখতে পারেন।

```cpp

//Importing LiquidCrystal Library for driving the LCD

#include <LiquidCrystal.h>

//LCD Dimension
#define COLS 16
#define ROWS 4

//Creating global LCD Object
LiquidCrystal my_lcd(2, 3, 4, 5, 6, 7);

void setup()
{
    //Setting up the LCD
    my_lcd.begin(COLS, ROWS);
    
    //Setting the cursor at the beginning 
    my_lcd.setCursor(0, 0);
    
    //Printing a string on the lcd
    my_lcd.print("Electroscholars");
}

//Nothing To Loop
void loop() {}
```

## আউটপুট (প্রোটিয়াস সিমুলেশন):

![output_gif](http://i.imgur.com/dBYRj2J.gif)

## প্রোগ্রাম ওয়াকথ্রু

### `#import <LiquidCrystal.h>`

LCD চালানোর জন্য আর্ডুইনোর অফিশিয়াল LiquidCrystal লাইব্রেরি আমরা ব্যবহার করব। লাইব্রেরি ব্যবহার করার মজা হল আপনি সরাসরি অন্য প্রোগ্রামারদের করা কোড আপনার কাজে ব্যবহার করতে পারবেন। 

LiquidCrystal লাইব্রেরিতে প্রচুর ফাংশন তৈরি করে দেওয়া আছে, যেমন কার্সর ব্লিংকিং, কাস্টম ক্যারেক্টার তৈরি করা, টেক্সট ডিরেকশন পরিবর্তন করা (left to right / right to left) ইত্যাদি। এই পর্বের শেষে আমরা অ্যাভেইল্যাবল ফাংশনগুলো ও তাদের প্রয়োগ সম্পর্কে হাল্কা ধারণা নেব।


আর্ডুইনোর প্রাণ মূলত আর্ডুইনো লাইব্রেরিগুলোই, যা ওপেন-সোর্স; তারমানে আপনি লাইব্রেরি গুলো মডিফাই করে নিজের কাজে ব্যবহার করতে পারবেন ও মডিফাই করা কোড আবার অন্যদের মাঝে বিতরণও করতে পারবেন। পরবর্তী কয়েকটি পর্ব LCD নিয়েই করা হবে এবং এই লাইব্রেরিটাই ব্যবহার করা হবে। লাইব্রেরি মডিফাই করে নিজের লাইব্রেরি তৈরি করাও আমরা দেখব। 

### `#define ROWS, #define COLS`

LCD নিয়ে কাজ করতে হলে অবশ্যই ডাইমেনশন জানতে হবে। মানে আপনার LCD কয়টি ক্যারেক্টার সাপোর্ট করে। `#define` করা ভ্যারিয়েবল গুলো আর ভ্যারিয়েবল থাকে না, ওটা কনসট্যান্ট হয়ে যায়। যেহেতু আমাদের LCD এর রো আর কলাম সংখ্যা ধ্রুবক তাই সেটাকে variable হিসেবে ডিক্লেয়ার না করাই ভাল। ইচ্ছা করলে রো আর কলাম আমরা এভাবেও লিখতে পারতাম:

```cpp
const int rows = 4; 
const int cols = 16;
``` 

অথবা সরাসরি কলাম আর রো বসিয়ে দিলেও হত

```cpp
my_lcd.begin(16, 4);
```

### `LiquidCrystal my_lcd(....)` 

অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং সম্পর্কে আমরা আগেই জেনে ছিলাম। এবার সেটা প্রয়োগ করার সময় চলে এসেছে। কনস্ট্রাক্টরের কথা মনে আছে তো? না মনে থাকলে [একবার দেখে নিন](http://medialab.electroscholars.com/2015/01/20/arduino-basic-oop-1/)। 

`LiquidCrystal` হল ক্লাস যার ডেফিনিশন দেওয়া আছে `#LiquidCrystal.h` নামক হেডার ফাইলটিতে। আর অবজেক্ট তৈরি করতে হয় এভাবে:

```cpp
//Without constructor arguments
the_class objectName;

//If the constructor takes arguments
the_class objectName(1, 2, 3);
```

LiquidCrystal এ ক্লাসের Constructor ওভারলোডেড। কোনটা ইউজ হবে সেটা নির্ভর করে আপনার পাঠানো আর্গুমেন্টের উপরে্। আমরা LCD এর ৬ টা পিন আর্ডুইনোর I/O এর সাথে কানেক্ট করেছি তাই ৬ আর্গুমেন্ট বিশিষ্ট কনস্ট্রাক্টর কাজ করবে। ৬ টা পিন অবশ্যই ক্রমানুসারে পাঠাতে হবে। যেমন এই প্রোগ্রামের ক্ষেত্রে ব্যবহৃত Constructor এর পিনের ক্রম ছিল

```cpp
LiquidCrystal lcd(RS, EN, D4, D5, D6, D7);
```

খেয়াল করে দেখুন আমরা এই ক্রম অনুযায়ী পিনগুলো কানেক্ট করেছি ও পিনগুলোর তথ্য কনস্ট্রাক্টরের মাধ্যমে পাঠাচ্ছি। 

### `my_lcd.begin(COLS, ROWS);`

LCD কে ক্যারেক্টার ডিস্প্লে করার জন্য ইনিশিয়ালাইজ করতে হবে। তাই আমরা `LiquidCrystal::begin(const uint8_t, const uint8_t)` মেথডের মাধ্যমে ব্যবহৃত LCD এর ডাইমেনশন পাঠিয়ে দিলাম সব সেট করার জন্য। 

যেহেতু LCD টি কমান্ড গ্রহণ ও ক্যারেক্টার শো করার জন্য প্রস্তুত তাই আমরা এবার `LiquidCrystal::print(char* str) ও LiquidCrystal::setCursor(uint8_t x, uint8_t y)` মেথড দুটো ব্যবহার করতে পারব।


### `my_lcd.setCursor(x, y)`

এই কমান্ডের মাধ্যমে Cursor কোথায় সেট করতে হবে সেটা ঠিক করা যায়। যদি আমি কোন একটি লেখা LCD এর ৩য় সারির ২য় কলাম থেকে স্টার্ট করতে চাই তাহলে কমান্ডটি হবে 
```my_lcd.setCursor(1, 2); //1 for second column, 2 for 3rd row [zero indexing]```

### `my_lcd.print(..)`

`LiquidCrystal::print(char *str)` মেথডের মাধ্যমে আপনি LCD তে কোন লেখা শো করতে পারবেন। এর আর্গুমেন্ট স্ট্রিং টাইপ।

**যেহেতু আমাদের লুপিংয়ের কোন প্রয়োজন নেই তাই আমরা `void loop()` ফাংশনটিতে কিছু লিখিনি।**


যদি এখন LCD তে লেখা ভেসে উঠে তাহলে বুঝবেন আপনি সঠিকভাবে আপনার LCD টি আর্ডুইনোর সাথে কনফিগার করতে পেরেছেন। এই পর্যন্তই, LCD এর পরবর্তী পর্বে আমরা কিছু ছোটখাট প্রজেক্ট তৈরি করব।

## LCD Header পিন সোল্ডারিং

সোল্ডার করার জন্য [এই টিউটোরিয়ালটি](https://www.sparkfun.com/tutorials/168) ফলো করুন। অথবা ইউটিউবে সার্চ দিলেই অনেক টিউটোরিয়াল পাবেন।

## সোর্স কোড ও ডায়াগ্রাম

সোর্স কোড, ডায়াগ্রাম সবই আপ্লোড করা আছে [এখানে](https://github.com/howtocode-com-bd/arduino.howtocode.com.bd/tree/master/LiquidCrystalProjectFiles)। চাইলে নামিয়ে টেস্ট করতে পারেন।
