..  မူပိုင်ခွင့် (c) 2014-ယခုအချိန်ထိ PlatformIO <contact@platformio.org>
    Apache License, Version 2.0 ("License") အောက်တွင် လိုင်စင်ရရှိထားပါသည်;
    License နှင့် ကိုက်ညီစွာမှသာ ဤဖိုင်ကို အသုံးပြုခွင့်ရှိပါသည်။
    License မိတ္တူကို အောက်ပါနေရာတွင် ရယူနိုင်ပါသည် -
       http://www.apache.org/licenses/LICENSE-2.0
    သက်ဆိုင်ရာဥပဒေအရ လိုအပ်ခြင်း သို့မဟုတ် စာဖြင့်သဘောတူထားခြင်း မရှိပါက၊
    License အောက်တွင် ဖြန့်ချိသော software သည် "AS IS" အခြေအနေအတိုင်း
    ဖြန့်ချိသည်ဖြစ်ပြီး၊ မည်သည့်အာမခံချက် သို့မဟုတ် စည်းကမ်းသတ်မှတ်ချက်မျှ
    တိုက်ရိုက်ဖြစ်စေ၊ သွယ်ဝိုက်၍ဖြစ်စေ မပါဝင်ပါ။
    ခွင့်ပြုချက်နှင့် ကန့်သတ်ချက်များအတွက် License ကို ကြည့်ရှုပါ။

.. _tutorial_unit_testing_blink:

"Blink" Project တစ်ခုအတွက် Unit Testing ပြုလုပ်ခြင်း
=====================================================

ဤ tutorial ၏ ရည်ရွယ်ချက်မှာ :ref:`unit_testing` ကို အသုံးပြုရန် မည်မျှလွယ်ကူကြောင်း
ပြသရန် ဖြစ်ပါသည်။

* **အဆင့်:** အခြေခံ (Beginner)
* **Platform များ:** Windows, macOS, Linux

.. contents:: မာတိကာ
    :local:

Project ကို စတင်ပြင်ဆင်ခြင်း
------------------------------

1. :ref:`core_quickstart` section သို့ သွားပြီး "Blink Project" ကို ဖန်တီးပါ။
2. Project တွင် root ``test`` directory ကို ဖန်တီးပါ (``src`` နှင့် တစ်လှမ်းတည်းတွင်)
3. test ``test_blink`` directory တစ်ခု ဖန်တီးပါ (အမည်ကို ``test_`` ဖြင့်
   စတင်ရမည်) ထို့နောက် ၎င်းထဲတွင် ``test_main.cpp`` ဖိုင်တစ်ခု ထားပါ
   (source code ကို အောက်တွင် တွေ့နိုင်ပါသည်)။
4. :ref:`cmd_test` command ကို အသုံးပြု၍ test များကို run ပါ။

Project ဖွဲ့စည်းပုံ
---------------------

.. code-block:: bash

    project_dir
    ├── platformio.ini
    └── test
        └── test_blink
            └── test_main.cpp

Source ဖိုင်များ
-----------------

* :ref:`projectconf`

  .. code-block:: ini

    [env:uno]
    platform = atmelavr
    framework = arduino
    board = uno

* ``test/test_blink/test_main.cpp``

  .. code-block:: cpp

    #include <Arduino.h>
    #include <unity.h>

    void setUp(void)
    {
      // ဒီနေရာမှာ လိုအပ်တာတွေ setup လုပ်ပါ
    }

    void tearDown(void)
    {
      // ဒီနေရာမှာ ရှင်းလင်းရမယ့်အရာတွေ ရှင်းလင်းပါ
    }

    void test_led_builtin_pin_number(void)
    {
      TEST_ASSERT_EQUAL(13, LED_BUILTIN);
    }

    void test_led_state_high(void)
    {
      digitalWrite(LED_BUILTIN, HIGH);
      TEST_ASSERT_EQUAL(HIGH, digitalRead(LED_BUILTIN));
    }

    void test_led_state_low(void)
    {
      digitalWrite(LED_BUILTIN, LOW);
      TEST_ASSERT_EQUAL(LOW, digitalRead(LED_BUILTIN));
    }

    void setup()
    {
      // မှတ်ချက်!!! ၂ စက္ကန့်ထက် စောင့်ပါ
      // board သည် Serial.DTR/RTS မှတစ်ဆင့် software reset ကို မပံ့ပိုးပါက
      delay(2000);

      pinMode(LED_BUILTIN, OUTPUT);

      UNITY_BEGIN(); // အရေးကြီးသော line!
      RUN_TEST(test_led_builtin_pin_number);
    }

    uint8_t i = 0;
    uint8_t max_blinks = 5;

    void loop()
    {
      if (i < max_blinks)
      {
        RUN_TEST(test_led_state_high);
        delay(500);
        RUN_TEST(test_led_state_low);
        delay(500);
        i++;
      }
      else if (i == max_blinks)
      {
        UNITY_END(); // unit testing ကို ရပ်တန့်ခြင်း
      }
    }

Test ရလဒ်များ
---------------

.. code::

  > pio test

  Verbose mode can be enabled via `-v, --verbose` option
  Collected 1 tests

  Processing test_blink in uno environment
  ----------------------------------------
  Building...
  Uploading...
  Testing...
  If you don't see any output for the first 10 secs, please reset board (press reset button)

  test/test_blink/test_main.cpp:34: test_led_builtin_pin_number	[PASSED]
  test/test_blink/test_main.cpp:43: test_led_state_high	[PASSED]
  test/test_blink/test_main.cpp:45: test_led_state_low	[PASSED]
  test/test_blink/test_main.cpp:43: test_led_state_high	[PASSED]
  test/test_blink/test_main.cpp:45: test_led_state_low	[PASSED]
  test/test_blink/test_main.cpp:43: test_led_state_high	[PASSED]
  test/test_blink/test_main.cpp:45: test_led_state_low	[PASSED]
  test/test_blink/test_main.cpp:43: test_led_state_high	[PASSED]
  test/test_blink/test_main.cpp:45: test_led_state_low	[PASSED]
  test/test_blink/test_main.cpp:43: test_led_state_high	[PASSED]
  test/test_blink/test_main.cpp:45: test_led_state_low	[PASSED]
  ----------------- uno:test_blink [PASSED] Took 16.51 seconds -----------------

  Environment    Test        Status    Duration
  -------------  ----------  --------  ------------
  uno            test_blink  PASSED    00:00:16.514

  =================== 11 test cases: 11 succeeded in 00:00:16.514 ===================
