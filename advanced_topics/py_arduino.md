# Python দিয়ে আর্ডুইনোর সাথে সিরিয়াল কমিউনেকশন, আর্ডুইনো সিরিয়াল ইভেন্ট পরিচিতি ও PyQt4 দিয়ে ডেস্কটপ অ

## পাইথনে আর্ডুইনোর সাথে সিরিয়াল কমিউনিকেশন ও আর্ডুইনোর সিরিয়াল ইভেন্ট পরিচিতি

পাইথনে সিরিয়াল কম্যুনিকেশনের জন্য আমরা ব্যবহার করব পাইথনের `PySerial` লাইব্রেরি।

### যা যা লাগবে:

* পাইথন জানতে হবে - না জানলে [এই কোর্সটি করুন](http://python.howtocode.com.bd)
* পাইথন ২.৭ - আপনার পিসিতে পাইথন না সেটাপ দেয়া থাকলে [এখান](http://python.howtocode.com.bd/installation.html) থেকে দেখে নিন।
* একটি আর্ডুইনো বোর্ড 
* নেট কানেকশন বা PySerial লাইব্রেরি
* `PyQt4` \[optional\]

পাইসিরিয়াল সেটাপ দেব আমরা `pip` পাইথন প্যাকেজ ইন্সটলারের মাধ্যমে। আপনার পিসিতে যদি `pip` ইন্সটলড না করা থাকে তাহলে [এখানে](https://pip.pypa.io/en/stable/installing/) দেখুন।

পাইসিরিয়াল ইন্সটল করার জন্য টার্মিনাল\(লিনাক্স\) বা কমান্ড প্রম্পট \(উইন্ডোজ\) ওপেন করে নিচের কমান্ডটি রান করুন

`pip install pyserial`

কিছুক্ষণের মধ্যে পাইসিরিয়াল সেটাপ হয়ে যাবে।

পাইথন দিয়ে সিরিয়াল কম্যুনিকেশন অন্যান্য ল্যাঙ্গুয়েজ দিয়ে কমিউনিকেট করার মতই। নিচে আর্ডুইনোর কোডটা দেখা যাক,

```text
#define led 13
#define baud 9600

void setup() {
  pinMode(led, OUTPUT);
  Serial.begin(baud);
}

void loop() { /*Nothing to do*/ }

void serialEvent(){
  if (Serial.available() > 0){
    //Reading string until '\n' is encountered
    String command = Serial.readStringUntil('\n');

    //Sending a reply after executing the function
    if (command.equals("on")) { digitalWrite(led, HIGH); Serial.println("LED ON"); }
    else if (command.equals("off")) { digitalWrite(led, LOW); Serial.println("LED OFF"); }
  }
}
```

#### লাইন ১ থেকে ৭

আগের আর্ডুইনো পর্বগুলি দেখে নিন।

#### লাইন ৯ - `void loop() {}`

আমরা সিরিয়াল কম্যুনিকেশন হ্যান্ডেল করব `serialEvent()` নামক ইন্টারাপ্ট হ্যান্ডলার ফাংশন দিয়ে। লুপে কিছু না লিখলেও এই ইন্টারাপ্ট ফাংশনের মাধ্যমে আমরা কিভাবে কম্যুনিকেট করব সেটাই দেখানো মূখ্য উদ্দেশ্য।

#### লাইন ১১ - `void serialEvent(){`

সিরিয়াল ইভেন্ট ফাংশনের শুরু। এটা একটা ইন্টারাপ্ট ফাংশন। মাইক্রোকন্ট্রোলার/মাইক্রোপ্রসেসরে ইন্টারাপ্ট থাকেই। ইন্টারাপ্ট আসলে এমন ধরণের সিগনাল যেটার প্রায়োরিটি নরমাল ফাংশনের চেয়ে বেশি।

একটা উদাহরণের মাধ্যমে ব্যাখ্যা করা যাক, ধরুন আপনি বই পড়ছেন এবং পাশে আপনার মোবাইল। এখন যদি মোবাইলে কোন Call আসে তাহলে মোবাইলটি বেজে উঠবে, সাধারণত যে কেউ বই পড়া বন্ধ করে মোবাইলে কথা সেরে তারপর বই পড়বে।

এখানে মোবাইলের রিংয়িং কে আমরা `Interrupt Signal` বলতে পারি এবং আপনি যে কথা বললেন সেটাকে আমরা `Interrupt Function` বলতে পারি।

ঠিক তেমনই, আর্ডুইনোতে সিরিয়ালে কোন ডেটা আসে তাহলে ইন্টারাপ্ট টেবিলের প্রায়োরিটি লিস্ট অনুযায়ী `serialEvent()` ফাংশনটি অটো কল হয়।

#### লাইন ১৪ - `String command = Serial.readStringUntil('\n')`

এর অর্থ হচ্ছে যতক্ষণ না পর্যন্ত আর্ডুইনো `\n` ক্যারেক্টারটি ডিটেক্ট করছে, ততক্ষণ পর্যন্ত সে সিরিয়ালের ডেটা রিড করে `command` নামের `String` ভ্যারিয়েবলে রাখছে।

#### লাইন ১৭ - `if (command.equals("on")) ...`

`equals` হল `String` ক্লাসের একটা ফাংশন। যেহেতু `command` হল `String` ক্লাসের অবজেক্ট তাই আমরা `command.equals(another_string)` এভাবে কল করতে পারি।

`equals` ফাংশনের ইনপুট প্যারামিটার হল আরেকটি স্ট্রিং, যেটার সাথে তুলনা করা হবে। `equals` এর রিটার্ন টাইপ `boolean`। অর্থাৎ, দুইটা স্ট্রিংয়ের প্রতিটি ক্যারেক্টার যদি সমান হয় তাহলে `equals` রিটার্ন করে `true` অথবা এটা `false` রিটার্ন করবে।

#### `digitalWrite ... ; Serial.println ...`

যদি আর্ডুইনো `on` স্ট্রিং টা রিসিভ করে তাহলে সে `13 no LED` অন করবে এবং একটা রিপ্লাই দিয়ে দেবে যে `LED` অন হয়েছে।

আর যদি `off` রিসিভ করে.... এটা আশা করি বলা লাগবে না। :P

### পাইথন প্রোগ্রাম

আমরা এতক্ষণ আর্ডুইনো প্রোগ্রাম নিয়ে আলোচনা করলাম, এবার একটু পাইথন প্রোগ্রাম দেখা যাক।

```python
# Importing the pyserial library
import serial

# My arduino is connected to COM3, check device manager for yours
arduino = serial.Serial("COM3")

# Closing the arduino serialport just in case
arduino.close()

# Setting baudrate to 9600
arduino.baudrate = 9600

# If not open then try to open it
if not arduino.is_open:
    arduino.open()

# While the port is opened, play with it by sending string commands
while True:
    command = raw_input('Enter command: ')
    arduino.write(command + '\n')
    print arduino.readline()
```

#### লাইন ২ - `import serial`

লাইব্রেরি ইম্পোর্ট করলাম।

#### লাইন ৫ - `arduino = serial.Serial(com_port)`

সিরিয়াল ক্লাস দিয়ে `Serial` টাইপ অবজেক্ট তৈরি করলাম ও ইনপুট প্যারামিটার দিলাম আমার পিসির যে পোর্টে `Arduino` কানেক্টেড হয়েছে। অর্থাৎ আমার পিসিতে কানেক্ট হয়েছে `COM3` তে, আপনার পিসি যদি উইন্ডোজ হয় তাহলে নতুন আর্ডুইনো IDE ওপেন করেই দেখতে পারেন, অথবা `Device manager > Ports` এ গেলেও দেখতে পাবেন \(আর্ডুইনো অবশ্যই কানেক্টেড থাকতে হবে\)

![comport](http://i.imgur.com/AF4HM5w.png)

#### লাইন ৮ - `arduino.close()`

অনেক সময় আর্ডুইনো পোর্ট কারণে অকারণে বিজি থাকে, সেটা বিজি থাকুক কি না থাকুক, তাকে ফ্রি করার জন্য আমরা ফাংশনটা কল করলাম। এতে করে পোর্ট যদি বিজিও থাকে তাহলেও সেটা ফ্রি হয়ে যাবে। Safety check হিসেবেও নেয়া যেতে পারে।

#### লাইন ১১ - `arduino.baudrate = 9600`

আর্ডুইনো কোডে নিশ্চয়ই দেখেছেন, আমি বডরেট `9600` দিয়েছি, তাই পাইথনেও একই স্পিড রাখলাম।

#### লাইন ১৪-১৫ - `if not ...`

যদি আর্ডুইনো পোর্ট ওপেন না থাকে তাহলে ওপেন করব। \(ডেটা রিড রাইটের জন্য\)

#### লাইন ১৮ - `while True:`

আমরা বেশ কিছু স্ট্রিং পাঠাতে চাচ্ছি তাই ইনফিনিট লুপ দিয়ে ভেতরের প্রোগ্রামটা লিখছি।

#### লাইন ১৯ - `command = raw_input('Enter command: ')`

বেসিক পাইথন জানলে এটা অবশ্যই জানবেন, না জানলে বলি, কনসোল থেকে ইনপুট নেওয়ার জন্যই এই স্টেটমেন্ট।

#### লাইন ২০ - `arduino.write(command + '\n')`

সিরিয়ালে ডেটা রাইট করার জন্য আমরা `write` ফাংশনটি কল করেছি। আর ভিতরে কনসোলে ইনপুট দেয়া স্ট্রিংটি পাঠাচ্ছি।

শেষে `+ \n` দেওয়ার উদ্দেশ্য হল, আর্ডুইনো সাইডে কোড লেখার সময় আমরা শর্ত দিয়েছিলাম `readStringUntil('\n')`, তাই স্ট্রিং পাঠানোর আগে একটা 'ডেলিমিটার' জুড়ে দিচ্ছি। আপনি `\n` এর বদলে `;, -, +` যেটা খুশি সেটাই বসাতে পারবেন, শর্ত হল পাইথন থেকে স্ট্রিং পাঠানোর সময় যেন ডেলিমিটারটা স্ট্রিংয়ের শেষে থাকে এবং আর্ডুইনোতে `readStringUntil(delimiter)` ডেলিমিটার একই থাকে।

#### লাইন ২১ - `print arduino.readline()`

আর্ডুইনো যদি কোন কিছু পাঠায় তাহলে সেটা প্রিন্ট হবে।

### টেস্টিং

![arduino2](http://i.imgur.com/akG7qIC.gif)

## PyQt4 দিয়ে আর্ডুইনোর জন্য অ্যাপ্লিকেশন তৈরি

আপনার যদি PyQt4 সম্পর্কে ধারণা থাকে তাহলে এই কোড মডিফাই করে খুব সহজেই আপনার কাজের জন্য পাইথন দিয়ে আর্ডুইনোর গুই তৈরি করতে পারবেন। [**সম্পূর্ণ প্রজেক্ট পাবেন এখানে**](https://github.com/manashmndl/PyDuino)**।**

এখানে আর্ডুইনো সাইডের কোড উপরের দেওয়া কোডটাই ব্যবহার করা হয়েছে।

### অ্যাপ্লিকেশন ডেমো

![demo](http://i.imgur.com/dlLJiw8.gif)

### `PySerial`

এখানে বেসিক কিছু আইডিয়া দেয়া হল, ভালভাবে জানতে দেখুন [অফিশিয়াল ডকুমেন্টেশন](https://pythonhosted.org/pyserial/)।

