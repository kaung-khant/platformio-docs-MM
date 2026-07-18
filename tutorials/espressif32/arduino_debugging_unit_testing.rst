..  မူပိုင်ခွင့် 2018-ယခုအချိန်ထိ PlatformIO <contact@platformio.org>
    Apache License, Version 2.0 ("License") အောက်တွင် လိုင်စင်ရရှိထားပါသည်;
    License နှင့် ကိုက်ညီစွာမှသာ ဤဖိုင်ကို အသုံးပြုခွင့်ရှိပါသည်။
    License မိတ္တူကို အောက်ပါနေရာတွင် ရယူနိုင်ပါသည် -
       http://www.apache.org/licenses/LICENSE-2.0
    သက်ဆိုင်ရာဥပဒေအရ လိုအပ်ခြင်း သို့မဟုတ် စာဖြင့်သဘောတူထားခြင်း မရှိပါက၊
    License အောက်တွင် ဖြန့်ချိသော software သည် "AS IS" အခြေအနေအတိုင်း
    ဖြန့်ချိသည်ဖြစ်ပြီး၊ မည်သည့်အာမခံချက် သို့မဟုတ် စည်းကမ်းသတ်မှတ်ချက်မျှ
    တိုက်ရိုက်ဖြစ်စေ၊ သွယ်ဝိုက်၍ဖြစ်စေ မပါဝင်ပါ။
    ခွင့်ပြုချက်နှင့် ကန့်သတ်ချက်များအတွက် License ကို ကြည့်ရှုပါ။

.. _tutorial_espressif32_arduino_debugging_unit_testing:

Arduino နှင့် ESP32-DevKitC ဖြင့် စတင်အသုံးပြုခြင်း - debugging နှင့် unit testing
====================================================================================

ဤ tutorial ၏ ရည်ရွယ်ချက်မှာ ``ESP32-DevKitC`` board အတွက် :ref:`framework_arduino`
framework ဖြင့် ရိုးရှင်းသော project တစ်ခုကို develop လုပ်ခြင်း၊ run ခြင်းနှင့် debug
လုပ်ရန် :ref:`ide_vscode` ကို အသုံးပြုရန် မည်မျှလွယ်ကူကြောင်း ပြသရန် ဖြစ်ပါသည်။

* **အဆင့်:** အခြေခံ (Beginner)
* **Platform များ:** Windows, Mac OS X, Linux

**လိုအပ်ချက်များ:**
    - :ref:`ide_vscode` ကို download လုပ်ပြီး install ပြုလုပ်ထားရန်
    - :ref:`board_espressif32_esp32dev`
    - debugging အတွက် :ref:`debugging_tool_olimex-arm-usb-ocd` သို့မဟုတ်
      :ref:`debugging_tool_olimex-jtag-tiny` adapter


.. contents:: မာတိကာ
    :local:

Project ကို စတင်ပြင်ဆင်ခြင်း
------------------------------

ပထမဦးစွာ PlatformIO Home Page ကို အသုံးပြု၍ project အသစ်တစ်ခု ဖန်တီးရန်
လိုအပ်ပါသည် (ဤ page ကို ဖွင့်ရန် toolbar ပေါ်ရှိ Home icon ကို နှိပ်ရုံဖြင့်
ရနိုင်ပါသည်) -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-1.png

ထို့နောက် development board အဖြစ် ``Espressif ESP32 Dev Module``၊ framework
အဖြစ် :ref:`framework_arduino` နှင့် project တည်နေရာလမ်းကြောင်း (သို့မဟုတ်
default ကို အသုံးပြုနိုင်သည်) ကို ရွေးချယ်ရန် လိုအပ်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-2.png

ရွေးချယ်ထားသော project ကို processing လုပ်ရန် အချိန်အနည်းငယ် ကြာနိုင်ပါသည်
(PlatformIO သည် လိုအပ်သော package အားလုံးကို download လုပ်ပြီး install
ပြုလုပ်ပါလိမ့်မည်)။ ထို့နောက် :ref:`framework_arduino` framework ဖြင့် code
ရေးသားရန် အသင့်ဖြစ်နေသော configuration အပြည့်အစုံပါ project တစ်ခု
ရရှိပါလိမ့်မည်။

ဖန်တီးထားသော Project ထဲသို့ Code ထည့်သွင်းခြင်း
--------------------------------------------------

Project ထဲသို့ တကယ့် code အချို့ ထည့်ကြည့်ကြပါစို့။ ပထမဦးစွာ
:ref:`projectconf_pio_src_dir` folder ရှိ default main file ``main.cpp`` ကို
ဖွင့်ပြီး ၎င်း၏ content ကို အောက်ပါအတိုင်း အစားထိုးပါ -

.. code-block:: cpp

    #include <Arduino.h>

    void setup()
    {
        Serial.begin(9600);
    }

    void loop()
    {
        Serial.println("Hello world!");
        delay(1000);
    }

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-3.png

ယခုအခါ compile လုပ်ရန်နှင့် upload လုပ်ရန် အသင့်ဖြစ်နေသော အခြေခံ project
တစ်ခု ဖန်တီးပြီးပါပြီ။

Firmware ကို Compile လုပ်ခြင်းနှင့် Upload လုပ်ခြင်း
-------------------------------------------------------

ယခု project ကို build လုပ်နိုင်ပါပြီ။ firmware ကို compile လုပ်ရန်
နည်းလမ်းများစွာ ရှိပါသည် -

* ``Project Tasks`` menu ရှိ Build option
* :ref:`ide_vscode_toolbar` ရှိ Build ခလုတ်
* Task Menu: ``Tasks: Run Task... > PlatformIO: Build`` (သို့) :ref:`ide_vscode_toolbar` တွင်
* Command Palette: ``View: Command Palette > PlatformIO: Build``
* hotkey ``cmd-alt-b / ctrl-alt-b`` ဖြင့်

အနီရောင်ဖြင့် အမှတ်အသားပြုထားသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-4.png

အားလုံးအဆင်ပြေပါက terminal window တွင် Success message ကို တွေ့ရမည်
ဖြစ်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-5.png

firmware ကို board ပေါ်သို့ upload လုပ်ရန်လည်း နည်းလမ်းများစွာ ရှိပါသည် -

* ``Project Tasks`` menu ရှိ Upload option
* :ref:`ide_vscode_toolbar` ရှိ Upload ခလုတ်
* Command Palette: ``View: Command Palette > PlatformIO: Upload``
* Task Menu ကို အသုံးပြု၍: ``Tasks: Run Task... > PlatformIO: Upload``
* hotkey: ``cmd-alt-u / ctrl-alt-u`` ဖြင့် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-6.png

upload လုပ်ပြီးနောက် firmware ကို မှန်ကန်စွာ upload လုပ်ပြီးမပြီး
စစ်ဆေးရန် လိုအပ်ပါသည်။ ၎င်းအတွက် serial monitor ကို ဖွင့်ပြီး board မှ
message ကို လက်ခံရရှိကြောင်း စစ်ဆေးပါ။ serial monitor ကို ဖွင့်ရန်
အောက်ပါ option များကို အသုံးပြုနိုင်ပါသည် -

* ``Project Tasks`` menu ရှိ Monitor option
* :ref:`ide_vscode_toolbar` ရှိ Serial Monitor ခလုတ်
* Command Palette: ``View: Command Palette > PlatformIO: Monitor``
* Task Menu: ``Tasks: Run Task... > PlatformIO: Monitor`` -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-7.png

firmware သည် မျှော်လင့်ထားသည့်အတိုင်း အလုပ်လုပ်ပါက board မှ message ကို
terminal window တွင် တွေ့မြင်နိုင်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-8.png

Firmware ကို Debug လုပ်ခြင်း
------------------------------

Hardware ကို စတင်ပြင်ဆင်ခြင်း
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ESP32 နှင့် JTAG probe ကို အသုံးပြုရန်အတွက် အောက်ပါ pin များကို
ချိတ်ဆက်ရန် လိုအပ်ပါသည် -

.. list-table::
    :header-rows:  1

    * - ESP32 ရှိ Pin
      - JTAG probe ရှိ Pin

    * - ``3.3V``
      - ``Pin 1(VTref)``

    * - ``GPIO 9 (EN)``
      - ``Pin 3 (nTRST)``

    * - ``GND``
      - ``Pin 4 (GND)``

    * - ``GPIO 12 (TDI)``
      - ``Pin 5 (TDI)``

    * - ``GPIO 14 (TMS)``
      - ``Pin 7 (TMS)``

    * - ``GPIO 13 (TCK)``
      - ``Pin 9 (TCK)``

    * - ``GPIO 15 (TDO)``
      - ``Pin 13 (TDO)``

board ကို debug လုပ်ရန် အလွယ်ကူဆုံးသော နည်းလမ်းကို :ref:`piodebug` က
ပေးအပ်ပါသည်။ ပထမဦးစွာ :ref:`projectconf` တွင် :ref:`projectconf_debug_tool`
ကို သတ်မှတ်ပေးရန် လိုအပ်ပါသည်။ ဤ tutorial တွင် :ref:`debugging_tool_olimex-arm-usb-ocd-h`
debug probe ကို အသုံးပြုထားပါသည် -

.. code-block:: ini

    [env:esp32dev]
    platform = espressif32
    board = esp32dev
    framework = arduino
    debug_tool = olimex-arm-usb-ocd-h

debug session ကို စတင်ရန် အောက်ပါ method များကို အသုံးပြုနိုင်ပါသည် -

* top menu ရှိ ``Debug: Start debugging``
* Quick Access menu ရှိ ``Start Debugging`` option
* hotkey ခလုတ် ``F5`` -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-9.png

PlatformIO သည် debug session ကို initialize လုပ်နေစဉ် အချိန်အနည်းငယ်
စောင့်ရန် လိုအပ်ပြီး main function ၏ ပထမဆုံး line ကို highlight ပြသောအခါ
debug ပြုလုပ်ရန် အသင့်ဖြစ်ပါပြီ။

1. debugging session သည် ``app_main()`` function ၏ ပထမဆုံး line တွင်
   ရပ်တန့်သည်အထိ စောင့်ပါ
2. **သတိပေးချက်!** ``void loopTask(void *pvParameters)`` (အောက်ဖော်ပြပါ
   screenshot တွင် line 13 - ဤ line သည် release တစ်ခုနှင့်တစ်ခု
   ကွာခြားနိုင်ပါသည်) တွင် breakpoint တစ်ခု သတ်မှတ်ပါ
3. ယခု debugging toolbar ရှိ CONTINUE/RUN ခလုတ် (right arrow icon) ကို
   နှိပ်ပါ
4. debugging session သည် ``void loopTask(void *pvParameters)`` function ၏
   ပထမဆုံး line တွင် ရပ်တန့်သင့်ပါသည်
5. ယခု သင့် Arduino setup/loop code သို့ သွားပြီး ရိုးရာ debugging
   ပြုလုပ်ပါ။

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-10.png

control ခလုတ်များကို အသုံးပြု၍ code ကို တစ်လှမ်းချင်း လျှောက်ကြည့်နိုင်ပြီး၊
breakpoint များ သတ်မှတ်နိုင်ပြီး ``Watch window`` သို့ variable များ
ထည့်နိုင်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-11.png

Unit Test များ ရေးသားခြင်း
-----------------------------

:ref:`unit_testing` test case များကို test အများအပြားပါဝင်နိုင်သော file
တစ်ခုတည်းထဲသို့ ထည့်နိုင်ပါသည်။ ပထမဦးစွာ ဤ file တွင် default function
လေးခု ထည့်ရန် လိုအပ်ပါသည် - ``setUp``, ``tearDown``, ``setup`` နှင့်
``loop``။ function ``setUp`` နှင့် ``tearDown`` တို့ကို test condition
များ initialize လုပ်ရန်နှင့် finalize လုပ်ရန် အသုံးပြုပါသည်။ ဤ function
များကို implement လုပ်ရန် test run ရန်အတွက် မလိုအပ်သော်လည်း test တစ်ခု
run ခြင်းမပြုမီ variable အချို့ initialize လုပ်ရန် လိုအပ်ပါက ``setUp``
function ကို အသုံးပြုပါ။ ထိုနည်းတူစွာ variable များ ရှင်းလင်းရန်
လိုအပ်ပါက ``tearDown`` function ကို အသုံးပြုပါ။ ကျွန်ုပ်တို့၏ ဥပမာတွင်
ဤ function များကို LED state များအား အသီးသီး initialize လုပ်ရန်နှင့်
deinitialize လုပ်ရန် အသုံးပြုပါမည်။ ``setup`` နှင့် ``loop`` function
များသည် ကျွန်ုပ်တို့၏ test plan ကို ဖော်ပြသည့် ရိုးရှင်းသော Arduino
program တစ်ခုကဲ့သို့ လုပ်ဆောင်ပါသည်။

project ၏ root တွင် ``test`` folder တစ်ခု ဖန်တီးပြီး ဤ folder ထဲသို့
file အသစ် ``test_main.cpp`` ကို ထည့်ကြပါစို့။ ထို့နောက် ``String`` class
အတွက် အခြေခံ test များကို ဤ file တွင် အကောင်အထည်ဖော်ပါမည် -

* ``test_string_concat`` က string နှစ်ခု ပေါင်းစပ်ခြင်း (concatenation)
  ကို test လုပ်ပါသည်
* ``test_string_substring`` က substring ထုတ်ယူခြင်း၏ မှန်ကန်မှုကို test
  လုပ်ပါသည်
* ``test_string_index_of`` က string သည် သတ်မှတ်ထားသော symbol ၏ မှန်ကန်သော
  index ကို ပြန်ပေးကြောင်း သေချာစေပါသည်
* ``test_string_equal_ignore_case`` က string နှစ်ခု၏ case-insensitive
  နှိုင်းယှဉ်မှုကို test လုပ်ပါသည်
* ``test_string_to_upper_case`` က string ကို upper-case သို့
  ပြောင်းလဲခြင်းကို test လုပ်ပါသည်
* ``test_string_replace`` က replace လုပ်ဆောင်ချက်၏ မှန်ကန်မှုကို test
  လုပ်ပါသည်

.. code-block:: cpp

    #include <Arduino.h>
    #include <unity.h>

    String STR_TO_TEST;

    void setUp(void) {
        // ဒီနေရာမှာ လိုအပ်တာတွေ setup လုပ်ပါ
        STR_TO_TEST = "Hello, world!";
    }

    void tearDown(void) {
        // ဒီနေရာမှာ ရှင်းလင်းရမယ့်အရာတွေ ရှင်းလင်းပါ
        STR_TO_TEST = "";
    }

    void test_string_concat(void) {
        String hello = "Hello, ";
        String world = "world!";
        TEST_ASSERT_EQUAL_STRING(STR_TO_TEST.c_str(), (hello + world).c_str());
    }

    void test_string_substring(void) {
        TEST_ASSERT_EQUAL_STRING("Hello", STR_TO_TEST.substring(0, 5).c_str());
    }

    void test_string_index_of(void) {
        TEST_ASSERT_EQUAL(7, STR_TO_TEST.indexOf('w'));
    }

    void test_string_equal_ignore_case(void) {
        TEST_ASSERT_TRUE(STR_TO_TEST.equalsIgnoreCase("HELLO, WORLD!"));
    }

    void test_string_to_upper_case(void) {
        STR_TO_TEST.toUpperCase();
        TEST_ASSERT_EQUAL_STRING("HELLO, WORLD!", STR_TO_TEST.c_str());
    }

    void test_string_replace(void) {
        STR_TO_TEST.replace('!', '?');
        TEST_ASSERT_EQUAL_STRING("Hello, world?", STR_TO_TEST.c_str());
    }

    void setup()
    {
        delay(2000); // ဝန်ဆောင်မှု delay
        UNITY_BEGIN();

        RUN_TEST(test_string_concat);
        RUN_TEST(test_string_substring);
        RUN_TEST(test_string_index_of);
        RUN_TEST(test_string_equal_ignore_case);
        RUN_TEST(test_string_to_upper_case);
        RUN_TEST(test_string_replace);

        UNITY_END(); // unit testing ကို ရပ်တန့်ခြင်း
    }

    void loop()
    {
    }


ယခု board ပေါ်သို့ test များ upload လုပ်ရန် အသင့်ဖြစ်ပါပြီ။ ၎င်းအတွက်
အောက်ပါတို့ကို အသုံးပြုနိုင်ပါသည် -

* :ref:`ide_vscode_toolbar` ရှိ Test ခလုတ်
* ``Project Tasks`` menu ရှိ Test option
* top menu ရှိ ``Tasks: Run Task... > PlatformIO Test`` -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-12.png

processing ပြီးနောက် testing ရလဒ်များအကြောင်း အသေးစိတ် report ကို တွေ့ရမည်
ဖြစ်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-13.png

report မှ တွေ့ရသည့်အတိုင်း ကျွန်ုပ်တို့၏ test အားလုံး အောင်မြင်ခဲ့ပါသည်!

Bluetooth LE Feature များ ထည့်သွင်းခြင်း
-------------------------------------------

ယခု အခြား BLE device များ (ဥပမာ ဖုန်းများ) နှင့် အပြန်အလှန်ဆက်သွယ်နိုင်သော
အခြေခံ application တစ်ခုကို ဖန်တီးကြပါစို့။ ဥပမာအားဖြင့် အောက်ပါ code
သည် value ကို serial port သို့ print ထုတ်နိုင်သော BLE characteristic
တစ်ခုကို declare လုပ်ပါသည် -

.. code-block:: cpp

    #include <Arduino.h>
    #include <BLEDevice.h>
    #include <BLEUtils.h>
    #include <BLEServer.h>

    #define SERVICE_UUID        "4fafc201-1fb5-459e-8fcc-c5c9c331914b"
    #define CHARACTERISTIC_UUID "beb5483e-36e1-4688-b7f5-ea07361b26a8"

    class MyCallbacks: public BLECharacteristicCallbacks {
        void onWrite(BLECharacteristic *pCharacteristic) {
          std::string value = pCharacteristic->getValue();
          if (value.length() > 0) {
            Serial.print("\r\nNew value: ");
            for (int i = 0; i < value.length(); i++)
              Serial.print(value[i]);
            Serial.println();
          }
        }
    };

    void setup() {
      Serial.begin(9600);

      BLEDevice::init("ESP32 BLE example");
      BLEServer *pServer = BLEDevice::createServer();
      BLEService *pService = pServer->createService(SERVICE_UUID);
      BLECharacteristic *pCharacteristic = pService->createCharacteristic(
                                             CHARACTERISTIC_UUID,
                                             BLECharacteristic::PROPERTY_READ |
                                             BLECharacteristic::PROPERTY_WRITE
                                           );

      pCharacteristic->setCallbacks(new MyCallbacks());

      pCharacteristic->setValue("Hello World");
      pService->start();

      BLEAdvertising *pAdvertising = pServer->getAdvertising();
      pAdvertising->start();
    }

    void loop() {
      delay(2000);
    }

ယခု ယခင် section များတွင် ဖော်ပြခဲ့သည့်အတိုင်း ဤ program ကို board
ပေါ်တွင် compile လုပ်ပြီး upload လုပ်နိုင်ပါသည်။ ကျွန်ုပ်တို့၏ application
သည် မျှော်လင့်ထားသည့်အတိုင်း အလုပ်လုပ်ကြောင်း အတည်ပြုရန် BLE feature
ပါရှိသော Android smartphone မည်သည့်တစ်ခုနှင့် `Nordic nRF Connect tool
<https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp&hl=en>`_
ကို အသုံးပြုနိုင်ပါသည်။

ပထမဦးစွာ advertising BLE device အားလုံးကို scan လုပ်ပြီး ``ESP32 BLE
example`` ဟု အမည်ရှိသော device သို့ connect လုပ်ရန် လိုအပ်ပါသည်။ board
သို့ connection အောင်မြင်ပြီးနောက် "Unknown Service" တစ်ခုနှင့် "Unknown
Characteristic" field တစ်ခုကို တွေ့ရမည် ဖြစ်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-14.png

value ကို သတ်မှတ်ရန် BLE characteristic သို့ text အသစ် ပို့ရန်
လိုအပ်ပါသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-15.png

value ၏ ပြောင်းလဲမှုကို serial monitor တွင် print ထုတ်ပြသည် -

.. image:: ../../_static/images/tutorials/espressif32/arduino-debugging-unit-testing-16.png

နိဂုံးချုပ်ချက်
----------------

ယခု ကျွန်ုပ်တို့တွင် ``ESP32-DevKitC`` board အတွက် နောက်ပိုင်း project
များအတွက် boilerplate အဖြစ် အသုံးပြုနိုင်သော project template တစ်ခု
ရရှိပြီ ဖြစ်ပါသည်။
