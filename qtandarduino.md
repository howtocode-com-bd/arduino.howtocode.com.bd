# Qt ও Arduino বেসিক

## যা যা প্রয়োজন:
* Qt 4 বা 5 [ডাউনলোড ও ইন্সটলেশন টিউটোরিয়ালের জন্য দেখুন [এখানে]()]
* C++ প্রোগ্রামিং ল্যাঙ্গুয়েজ সম্পর্কে ধারণা (বেসিক অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং জ্ঞানসহ, যদি কনসেপ্টগুলো ঝালাই করতে চান তাহলে ভিসিট করুন [এখানে]()]
* Arduino Board (সিম্যুলেশন করার জন্য অতিরিক্ত কিছু কাজ করতে হবে তাই আপাতত একটি বোর্ড থাকলে কাজ করতে সুবিধা হবে)
* Usb A to B Cable
* Arduino IDE

## Qt কী?

Qt হল (উচ্চারণ হবে "কিউট" বা "কিউ-টি" (আনঅফিশিয়াল)) ক্রস প্ল্যাটফর্ম অ্যাপ্লিকেশন ফ্রেমওয়ার্ক যেটা দিয়ে যেকোন সফটওয়্যার বা হার্ডওয়্যার প্ল্যাটফর্মে সেম কোড বা অল্প পরিবর্তিত কোড দিয়েই সফটওয়্যার ডেভেলপ করা যায় যেগুলোর স্পিড নেটিভ অ্যাপের সমান। 

C++ এ GUI Based প্রোগ্রামিং টা বেশ ঝামেলাকর বলে মনে হলেও Qt Framework যারা ব্যবহার করেন তাদের ক্ষেত্রে গুই প্রোগ্রামিং খুবই সহজ। কয়েক লাইন লিখেই চমৎকার সব অ্যাপ ডেভেলপ করা যায়। অন্যান্য ফ্রেমওয়ার্কের সাথে এর বেশ কিছু মিল ও অমিল আছে। Qt Framework এর ইউনিক ফিচারের মধ্যে একটি signal ও slot। এছাড়াও অনেক ফিচার আছে কিন্তু যেহেতু এটা মূলত Arduino বেজড তাই কিউট নিয়ে একটু কম ই বলা হবে।

## Qt First Run

* কিউট ফ্রেমওয়ার্ক ওপেন করুন -> New Project -> Application -> Qt Widgets Application -> Choose -> Name -> Next -> Next -> Next -> Finish দিলে আপনাকে MainWindow.cpp ফাইলে নিয়ে আসবে
![qt-1](http://i.imgur.com/Mrl4oVZ.gif)

* এবার বামের ফাইল ডিরেক্টরি থেকে main.cpp সিলেক্ট করুন ডাবল ক্লিক করে তারপর নিচে-বামে-কোণায় দেখুন প্লে আইকন আছে সবুজ রংয়ের, সেটাতে ক্লিক করুন অথবা Ctrl+R চাপুন তাহলে প্রোগ্রামটি রান হবে ও আপনি একটি MainWindow দেখতে পাবেন
![qt-2](http://i.imgur.com/rWKYWEy.gif)

চালু হলে মেইনউইন্ডো ক্লোজ করে দিন। এতে বুঝা গেল আপনার Qt ঠিকঠাক ইন্সটলড হয়েছে এবং আপনি কাজ করার জন্য প্রস্তুত।

## Qt প্রথম প্রোগ্রাম

* আগের প্রোজেক্টটি থেকে main.cpp ফাইলটি সিলেক্ট করুন ও নিচের কোডটি লিখে রান করুন

```cpp
#include "mainwindow.h"
#include <QApplication>
#include <QLabel>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QLabel label("Electroscholars");
    label.show();
    return a.exec();
}
```

![qt-3](http://i.imgur.com/9M1wqNs.gif)

প্রোগ্রামটিতে আমরা কী করলাম? সাধারণত নতুন কোন ল্যাঙ্গুয়েজ শুরু করার সময় আমরা "Hello World" জাতীয় কিছু প্রিন্ট করি। Minimum Qt GUI অ্যাপ ডেভেলপ করার জন্যও আমরা সিম্পল GUI বেজড একটা টেক্সট শো করলাম। হ্যাঁ, লেবেলে "Electroscholars" রিপ্লেস করে আপনার নামও বসিয়ে দেখতে পারেন। 

## Walkthru

### `#include "mainwindow.h"` 
প্রোজেক্ট ক্রিয়েট করার সময় এই ফাইলটা main.cpp ফাইলে আইডিই অটো অ্যাড করে দিয়েছে। আমরা এই ফাইলে আপাতত কিছু লিখিনি তাই অ্যাড করলে বা না করলে কিছু যায় আসে না। আপনি ইচ্ছা করলে ডিলিট করে দিতে পারেন।

### `#include <QApplication>`

Qt এ গুই প্রোগ্রামিং করতে হলে এই Header টা অবশ্যই অ্যাড করতে হবে। কারণ নিচে বলা হল।

### `#include <QLabel>`

Qt এর ক্ষেত্রে দুইটা জিনিস খেয়াল করে দেখবেন, Header এর নাম আর Class এর নাম একই হয়। আর সব কম্পোনেন্টগুলোর আগে Q থাকে। যেহেতু এইখানে Label কম্পোনেন্টটা নিয়ে কাজ করা হচ্ছে তাই আমরা Label এর Qt Variant QLabel ক্লাসটি ব্যবহার করার জন্য Header টি অ্যাড করেছি।

### `QApplication a(argc, argv);`

 শুরুতেই আমরা একটি টিপিক্যাল মেইন ফাংশন দেখলাম। এই মেইন ফাংশনের ভিতরে দেখা যাচ্ছে  QApplication এর একটি অবজেক্ট a ক্রিয়েট করে কন্সট্রাক্টর হিসেবে আমরা কমান্ড লাইন আর্গুমেন্ট গুলো পাস করছি (argc, argv)। QApplication অবজেক্ট ছাড়া কোন গুই প্রোগ্রাম চলবে না। কারণ অন্যসবকিছুর পাশাপাশি QApplication একটা Event Loop তৈরি করে। এই ইভেন্ট লুপের কাজ হল অ্যাপ্লিকেশন ততক্ষণ পর্যন্ত রান করা যতক্ষণ পর্যন্ত আপনি window এর ক্লোজ বাটনটি না চাপছেন।

### `QLabel label("....");`

এখানে আমরা QLabel একটা অবজেক্ট তৈরি করেছি এবং কনস্ট্রাক্টর হিসেবে লেবেলে কী দেখাবে সেটি আর্গুমেন্ট হিসেবে দিয়েছি। এই অবজেক্টটি ক্রিয়েট করার সময় Invisible থাকে। তাই একে Visible করার জন্য আমরা label.show() মেথড টি ব্যবহার করেছি।

### `return a.exec()`

এই মেথডটা মূলত Event Loop শুরু করে যেটা অ্যাপ্লিকেশনের Event গুলো অ্যাপ্রোপ্রিয়েট অবজেক্টগুলোর কাছে ফরওয়ার্ড করে। এই সব ইভেন্টকে User Action এর মাধ্যমে তৈরি হয় যেমন বাটনে ক্লিক করা। আমরা বাটনে ক্লিক করে কীভাবে আর্ডুইনো LED অফ ও অন করা যায় সেটা এই পর্বে দেখব। Event Loop তখন টার্মিনেট হয় যখন QApplication অবজেক্টের quit ফাংশনটি কল করা হয়।

বলাই বাহুল্য কিউটের অনেক কিছু এখানে স্কিপ করা হয়েছে। কিউট শেখার জন্য কিউট ডকুমেন্টেশন এর চেয়ে ভাল কিছু হতে পারে না। প্রজেক্ট বেজড কাজ শেখার জন্য Qt এর উপর নিচের বই ও ইউটিউব চ্যানেলগুলো দেখতে পারেন।

#### বইয়ের ও ডকুমেন্টেশনের তালিকা

* The Book of Qt 4  - The Art of Building Qt Application
* C++ GUI Programming in Qt - Summerfield
* [Official Qt Documentation]() 

#### ইউটিউব লিঙ্ক

* [VoidRealms এর ১০০+ কিউট টিউটোরিয়াল]()
* [Qt BootCamp]()

## Qt Designer ব্যবহার করে সিম্পল Event Driven GUI অ্যাপ্লিকেশন

এখন আমরা এমন একটি অ্যাপ বানাব যার দুইটা বাটন থাকবে, একটি বাটনে ক্লিক করলে মেসেজ শো করবে Led On ও আরেকটি বাটনে ক্লিক করলে  মেসেজ শো করবে Led Off। তাহলে শুরু করা যাক।

* আগের প্রজেক্টটি ওপেন করা থাকলে সেটাকে এডিট করেই কাজ করা যাবে। চাইলে আপনি নতুন প্রজেক্ট তৈরি করে নিচের স্টেপ ফলো করতে পারেন। বামপাশের Forms ফোল্ডারের ভিতরে দেখুন mainwindow.ui ফাইলটি আছে, সেটাতে ডাবল ক্লিক করুন ও ইমেজ দেখে ঝটপট দুইটা বাটন ও একটি লেবেল বসিয়ে দিন
![qt-4](http://i.imgur.com/xyKhRQ2.gif)

* দ্রষ্টব্য: বাটনের উপরের টেক্সট পরিবর্তন করা হয়েছে, অবজেক্টের নাম কিন্তু নয়। অবজেক্টের নাম পরিবর্তন করার জন্য এই কাজ করুন:
![qt-5](http://i.imgur.com/sC7xrQL.gif)

* এবার বাটনে ক্লিক করলে যাতে কাজ হয় আমরা সেই লজিক বসাব। সেজন্য যেটা করতে হবে, বাটনের উপর রাইট ক্লিক করুন ও go to slot -> clicked() এ গেলে IDE আপনাকে একটি কোড ব্লকে নিয়ে যাবে যেখানে বাটনে ক্লিক করলে কী হবে সে কোড আপনি বসাবেন

![qt-6](http://i.imgur.com/wsYf4eX.gif)

দ্রষ্টব্য: qDebug() কে কিউটের cout মনে করতে পারেন। কনসোলে আউটপুট দেখানোর কাজ করে এটা। যদি এরর দেখায় তাহলে `#include <QDebug>` লাইনটা প্রোগ্রামের শুরুতে বসিয়ে নিন

* একই ভাবে led off বাটনের লজিক বসান

![qt-7](http://i.imgur.com/ag3xw9w.gif)

* এবার আমাদের কাজ হবে ledStatus নামক QLabel এ আমাদের ইচ্ছামত টেক্সট বসানো। মনে রাখবেন, গুই ডিজাইনারে আপনি অবজেক্ট ড্র্যাগ ড্রপ করলে অটোমেটিক ui_mainwindow.h ফাইলে সবকিছু অ্যাড হয়ে যায়। এগুলো সব করে দেয় Qt IDE তাই আমাদের অনেক কাজ ই করা লাগবে না। এই পোস্টটি অনেক কমপ্যাক্ট বিধায় অনেক এক্সপ্লেনেশন স্কিপ করা হয়েছে, তবে যতটুকু না বুঝলেই নয় ততটাই বলা হয়েছে। আরেকটু জানতে চাইলে গুগল, বই কিংবা ডকুমেন্টেশন ঘেঁটে দেখতে পারেন।
	* ledStatus নামের QLabel অবজেক্টের টেক্সট চেঞ্জ করার জন্য setText মেথডটি আছে। কিন্তু সমস্যা হল আপনি কীভাবে ledStatus অবজেক্টকে ধরে তার মেথড কল করবেন? আসলে  আমরা যখন প্রজেক্ট তৈরি করি তখন অটোমেটিক MainWindow / Widget / Dialog কে Ui নেমস্পেসের ভিতরে নিয়ে আসে এবং private অ্যাকসেস মডিফায়ারের ভিতরে *ui নামে একটি অবজেক্ট ক্রিয়েট করে। আপাতত এইটুকু জানুন, আপনি ডিজাইনার দিয়ে যত কম্পোনেন্ট অ্যাড করবেন সেগুলো ui এর মধ্যে চলে আসে। ফলে আমরা যদি কোন কম্পোনেন্টের মেথড কল করতে চাই তাহলে ui->object->objectMethod() অর্থাৎ আমি যদি ledStatus এর টেক্সট পরিবর্তন করতে চাই তাহলে লিখব ui->ledStatus->setText("Some text")।

![qt-8-png](http://i.imgur.com/baPzL9r.jpg)

* বাটন দুইটায় আমরা নিচের ছবির মত করে দুইটা লাইন অ্যাড করে দেই
![qt-9-png](http://i.imgur.com/06gODkv.jpg)

* ফলাফল
![qt-10](http://i.imgur.com/EUz8Rfj.gif)

তাহলে আমরা দেখলাম কীভাবে দুইটা বাটন ও লেবেল দিয়ে একটা গুই অ্যাপ তৈরি করা যায়। এবার আর্ডুইনোর সাথে কমিউনিকেট করে আর্ডুইনো led off ও on করতে পারে এমন একটি অ্যাপ আমরা তৈরি করব।
  
## QSerialPort ও Arduino

* সিরিয়াল কম্যুনিকেশন এস্টাব্লিশ করার জন্য আমরা কিউট অফিশিয়াল QSerialPort লাইব্রেরিটা ব্যবহার করব। লাইব্রেরিটা ব্যবহার করার আগে আপনার প্রজেক্টের .pro ফাইলে serialport অ্যাড করতে হবে।

![qserialport_pro](http://i.imgur.com/xqA7sG3.gif)

* এখন আপনি QSerialPort লাইব্রেরি ব্যবহার করার জন্য প্রস্তুত। mainwindow.h Header ফাইলটা ওপেন করুন `#include <QSerialPort>` সবার উপরে লিখুন Header ফাইলটা অ্যাড করার জন্য ও QSerialPort নামের একটি অবজেক্ট পয়েন্টার তৈরি করুন। এধরণের অবজেক্টে সাধারণত private access modifier ব্যবহার করা হয়। আপনি চাইলে public ও ব্যবহার করতে পারেন

![qserialport_11](http://i.imgur.com/wWkx29t.gif)

* **গুরুত্বপূর্ণ:** আমরা Arduino ও Qt কে ডিফল্ট কম্যুনিকেশন সেটিংসে কম্যুনিকেট করব। যদি আপনি আর্ডুইনোর অফিশিয়াল ওয়েবসাইটে সিরিয়াল চ্যাপ্টারটি দেখেন তাহলে দেখবেন বলা আছে `An optional second argument configures the data, parity, and stop bits. The default is 8 data bits, no parity, one stop bit.` অর্থাৎ, dataBits এর সংখ্যা ৮ বা এক ফ্রেমে ৮ বিট পাস হবে, কোন এক্সট্রা বা Parity বিট নাই এবং স্টপ বিট one stop। 
যেহেতু আমরা এখন ডিফল্ট কনফিগারেশন জানি তাহলে এই কনফিগারেশনে আমাদের কিউট অ্যাপটা ডেভেলপ করলেই হচ্ছে। যদি আপনি কনফিগ পরিবর্তন করতে চান সেক্ষেত্রে আপনার আর্ডুইনো কোডে Serial.begin মেথডে baudRate পাঠানোর পাশাপাশি কাস্টম কনফিগারেশন পাঠাতে হবে।
    * আমরা Qt এর সিরিয়ালপোর্টে এই প্রোপার্টিগুলো সেট করে দিতে পারি। যেহেতু তৈরি করা QSerialPort অবজেক্টের নাম দেওয়া হয়েছে arduino, তাই আমরা একটি বাটন তৈরি করব Connect নামে যাতে সেটাতে ক্লিক করলে Connection Established হয়। 
    
আর্ডুইনোর সাথে সিরিয়াল কানেকশন তৈরি করার জন্য (ডিফল্ট কনফিগারেশনে) প্রয়োজনীয় মেথড ও আর্গুমেন্ট:

```cpp
    arduino->setPortName("COM12"); //yours maybe different, please check by connecting it to your pc
    arduino->setBaudRate(QSerialPort::Baud9600);
    arduino->setDataBits(QSerialPort::Data8);
    arduino->setParity(QSerialPort::NoParity);
    arduino->setStopBits(QSerialPort::OneStop);
    // Skipping hw/sw control
    arduino->setFlowControl(QSerialPort::NoFlowControl);
```
* Connect বাটন বসানোর আগে কনস্ট্রাক্টরে (mainwindow.cpp তে) আপনি QSerialPort অবজেক্টটি ইনিশিয়ালাইজ করতে পারেন নিচের কোডের মাধ্যমে। তারপর এর সিরিয়াল পোর্ট নেম বসিয়ে দিতে পারেন। আমার ক্ষেত্রে COM12।

```cpp
arduino = new QSerialPort(this);
arduino->setPortName("COM12");
```

![settingPortname](http://i.imgur.com/ZAl4siE.gif)

* দ্রষ্টব্য: পোর্ট দেখার জন্য 

![showport](http://i.imgur.com/HwC3kDD.gif)

* এবার mainwindow.ui ফাইল সিলেক্ট করুন ও আরেকটি পুশ বাটন অ্যাড করে দিন। QPushButton এর ObjectName পরিবর্তন করে connectArduino বা যেকোন কিছু দিন আর উপরের Text পরিবর্তন করে Connect লিখে দিন তারপর রাইট ক্লিক করে go to slot দিন

![connectbutton](http://i.imgur.com/vIXOM4v.gif)

* বাটনটি ক্লিক করলে আমরা প্রথমে QSerialPort টা আগে ক্লোজ করে দিব। কারণ যদি কোন কারণে ওপেন থাকে তাহলে সেটা কাজ করবে না। ক্লোজ করে তারপর কানেকশন Establish করব। আর কানেক্ট করার আগে দেখে নিব সে ReadWrite Mode এ ওপেন হচ্ছে কিনা। যদি ওপেন হয় তাহলে তার ডিফল্ট প্রোপার্টিগুলো সেট করে দিব:

![connectArduino](http://i.imgur.com/n4aPaYj.gif)


* কানেক্ট করার পর মেসেজ শো করানোর জন্য আমরা QMessageBox ব্যবহার করতে পারি। এর মেথড ও প্রোপার্টি Qt Docs এ পাওয়া যাবে।
![messagebox](http://i.imgur.com/aVf03lP.gif)

* প্রায় সব কাজ শেষ, এখন LED ON বাটন চাপ দিলে যাতে এমন কোন ডেটা পাস হয় যেটা আর্ডুইনো চিহ্নিত করে Led জ্বালাতে পারে সেই কোডটি বসাব। LED OFF এর ক্ষেত্রে অন্য যেকোন ডেটার জন্য আর্ডুইনো LED নিভিয়ে দিবে। Arduino তে ডেটা রাইট করার জন্য write() ফাংশনটি ব্যবহার করব

![write](http://i.imgur.com/BZkMwto.gif)

* আর্ডুইনো সাইডের কোড। সিম্পল LED জ্বলা নেভার কোড, [সিরিয়াল কম্যুনিকেশনে]() Serial এর মেথডগুলো সম্পর্কে জানা যাবে। কোডটি আর্ডুইনোতে আপ্লোড করুন ও কানেক্ট করে রাখুন। তারপর Qt এ প্রোগ্রামটি রান করুন:
```cpp
//Arduino Side
// Baud Rate 9600
int led = 13;
char command;

void setup() {
  Serial.begin(9600);
  pinMode(led, OUTPUT);
}

void loop() {
  if (Serial.available()){
  x = Serial.read();
  if (x == 'a') digitalWrite(led, HIGH);
  else digitalWrite(led, LOW);
  }
}

```

* আর্ডুইনোতে কোড আপ্লোড:
![arduinocode](http://i.imgur.com/fPdHQvj.gif)


* আর্ডুইনো ঠিকভাবে কানেক্টেড হলে এইরকম একটা মেসেজ দেখতে পারবেন, আর Led অন ও অফ বাটনে ক্লিক করলে অফ অন দেখতে পারবেন


![arduinowithqt](http://i.imgur.com/IfY9DYs.gif)


আবারও বলা হচ্ছে, আলোচনা শর্ট ও সিম্পল রাখার জন্য এই অ্যাপ তৈরি করা হয়েছে। ইউজার ইন্টারফেস ও প্রোগ্রাম ডিজাইনিংয়ে মনযোগ না দিয়ে প্রসিডিউরের উপরে জোড় দেওয়া হয়েছে। পরবর্তী পর্বে আমরা দেখব Arduino কে LCD এর সাথে ইন্টারফেস করে Qt Desktop App এর মাধ্যমে Wirelessly মেসেজ শো করানো যায়। প্রচুর F.A.Q থাকতে পারে ভেবেই সেগুলো অ্যাড করা হল না। এইখানে যে কম্যুনিকেশন দেখানো হল সেটা আপাতত one way। সিগনাল ও স্লট ব্যবহার করে duplex কম্যুনিকেশনও দেখানো হবে পরবর্তীতে।

সম্পূর্ণ প্রজেক্ট কোড পাওয়া যাবে [এখানে]()



