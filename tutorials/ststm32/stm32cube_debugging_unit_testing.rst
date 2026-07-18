..  မူပိုင်ခွင့် 2014-ယခုအချိန်ထိ PlatformIO <contact@platformio.org>
    Apache License, Version 2.0 ("License") အောက်တွင် လိုင်စင်ရရှိထားပါသည်;
    License နှင့် ကိုက်ညီစွာမှသာ ဤဖိုင်ကို အသုံးပြုခွင့်ရှိပါသည်။
    License မိတ္တူကို အောက်ပါနေရာတွင် ရယူနိုင်ပါသည် -
       http://www.apache.org/licenses/LICENSE-2.0
    သက်ဆိုင်ရာဥပဒေအရ လိုအပ်ခြင်း သို့မဟုတ် စာဖြင့်သဘောတူထားခြင်း မရှိပါက၊
    License အောက်တွင် ဖြန့်ချိသော software သည် "AS IS" အခြေအနေအတိုင်း
    ဖြန့်ချိသည်ဖြစ်ပြီး၊ မည်သည့်အာမခံချက် သို့မဟုတ် စည်းကမ်းသတ်မှတ်ချက်မျှ
    တိုက်ရိုက်ဖြစ်စေ၊ သွယ်ဝိုက်၍ဖြစ်စေ မပါဝင်ပါ။
    ခွင့်ပြုချက်နှင့် ကန့်သတ်ချက်များအတွက် License ကို ကြည့်ရှုပါ။

.. _tutorial_stm32cube_debugging_unit_testing:

STM32Cube HAL နှင့် Nucleo-F401RE - debugging နှင့် unit testing
====================================================================

ဤ tutorial ၏ ရည်ရွယ်ချက်မှာ ``STM32 Nucleo-F401RE`` board အတွက်
:ref:`framework_stm32cube` framework ဖြင့် အခြေခံ blink project တစ်ခုကို
develop လုပ်ခြင်း၊ run ခြင်းနှင့် debug လုပ်ရန် :ref:`ide_vscode` ကို
အသုံးပြုရန် မည်မျှလွယ်ကူကြောင်း ပြသရန် ဖြစ်ပါသည်။

* **အဆင့်:** အလယ်အလတ် (Intermediate)
* **Platform များ:** Windows, Mac OS X, Linux

**လိုအပ်ချက်များ:**

- :ref:`ide_vscode` ကို download လုပ်ပြီး install ပြုလုပ်ထားရန်
- :ref:`debugging_tool_stlink` debug tool အတွက် driver များ install လုပ်ရန်
- :ref:`board_ststm32_nucleo_f401re` development board


.. contents:: မာတိကာ
  :local:

Project ကို စတင်ပြင်ဆင်ခြင်း
------------------------------

ပထမအဆင့်တွင် PlatformIO Home Page ကို အသုံးပြု၍ project အသစ်တစ်ခု
ဖန်တီးရန် လိုအပ်ပါသည် (ဤ page ကို ဖွင့်ရန် toolbar ပေါ်ရှိ Home icon ကို
နှိပ်ရုံဖြင့် ရနိုင်ပါသည်) -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-1.png

နောက်အဆင့်တွင် development board အဖြစ် ``ST Nucleo-F401RE``၊ framework
အဖြစ် :ref:`framework_stm32cube` နှင့် project တည်နေရာလမ်းကြောင်း
(သို့မဟုတ် default ကို အသုံးပြုနိုင်သည်) ကို ရွေးချယ်ရန် လိုအပ်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-2.png

ရွေးချယ်ထားသော project ကို processing လုပ်ရန် အချိန်အနည်းငယ် ကြာနိုင်ပါသည်
(PlatformIO သည် လိုအပ်သော package အားလုံးကို download လုပ်ပြီး install
ပြုလုပ်ပါလိမ့်မည်) ဤအဆင့်များပြီးနောက် :ref:`framework_stm32cube`
framework ဖြင့် code ရေးသားရန် အသင့်ဖြစ်နေသော configuration
အပြည့်အစုံပါ project တစ်ခု ရရှိပါလိမ့်မည်။

ဖန်တီးထားသော Project ထဲသို့ Code ထည့်သွင်းခြင်း
--------------------------------------------------

Project ထဲသို့ တကယ့် code အချို့ ထည့်ကြည့်ကြပါစို့။ ပထမဦးစွာ
:ref:`projectconf_pio_src_dir` folder တွင် main file နှစ်ခု ``main.c``
နှင့် ``main.h`` ကို ဖန်တီးပါမည်။ project window ရှိ ``src`` ကို
right click နှိပ်ပါ -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-3.png

``main.h`` ထဲသို့ အောက်ပါ content ကို ထည့်ပါ -

.. code:: cpp

  #ifndef MAIN_H
  #define MAIN_H

  #include "stm32f4xx_hal.h"

  #define LED_PIN                                GPIO_PIN_5
  #define LED_GPIO_PORT                          GPIOA
  #define LED_GPIO_CLK_ENABLE()                  __HAL_RCC_GPIOA_CLK_ENABLE()

  #endif // MAIN_H


``main.c`` ထဲသို့ ဤ code ကို ထည့်ပါ -

.. code:: cpp

  #include "main.h"

  void LED_Init();

  int main(void)
  {
    HAL_Init();
    LED_Init();

    while (1)
    {
      HAL_GPIO_TogglePin(LED_GPIO_PORT, LED_PIN);
      HAL_Delay(1000);
    }
  }

  void LED_Init()
  {
    LED_GPIO_CLK_ENABLE();
    GPIO_InitTypeDef GPIO_InitStruct;
    GPIO_InitStruct.Pin = LED_PIN;
    GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
    GPIO_InitStruct.Pull = GPIO_PULLUP;
    GPIO_InitStruct.Speed = GPIO_SPEED_HIGH;
    HAL_GPIO_Init(LED_GPIO_PORT, &GPIO_InitStruct);
  }

  void SysTick_Handler(void)
  {
    HAL_IncTick();
  }

ဤအဆင့်ပြီးနောက် compile လုပ်ရန်နှင့် upload လုပ်ရန် အသင့်ဖြစ်နေသော
အခြေခံ blink project တစ်ခု ဖန်တီးပြီးပါပြီ။

Firmware ကို Compile လုပ်ခြင်းနှင့် Upload လုပ်ခြင်း
-------------------------------------------------------

ယခု project ကို build လုပ်နိုင်ပါပြီ။ firmware ကို compile လုပ်ရန်
အောက်ပါ option များကို အသုံးပြုနိုင်ပါသည် -
``Project Tasks`` menu ရှိ Build option၊ :ref:`ide_vscode_toolbar` ရှိ
Build ခလုတ်၊ Command Palette ``View: Command Palette > PlatformIO: Build``
ကို အသုံးပြု၍၊ Task Menu ``Tasks: Run Task... > PlatformIO: Build`` ကို
အသုံးပြု၍ သို့မဟုတ် hotkey ``cmd-alt-b / ctrl-alt-b`` ဖြင့် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-4.png

အားလုံးအဆင်ပြေပါက terminal window တွင် အောင်မြင်ကြောင်း ရလဒ်ကို
တွေ့ရမည် ဖြစ်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-5.png

firmware ကို board ပေါ်သို့ upload လုပ်ရန် အောက်ပါ option များကို
အသုံးပြုနိုင်ပါသည် -
``Project Tasks`` menu ရှိ Upload option၊ :ref:`ide_vscode_toolbar` ရှိ
Upload ခလုတ်၊ Command Palette ``View: Command Palette > PlatformIO: Upload``
ကို အသုံးပြု၍၊ Task Menu ``Tasks: Run Task... > PlatformIO: Upload`` ကို
အသုံးပြု၍ သို့မဟုတ် hotkey ``cmd-alt-u / ctrl-alt-u`` ဖြင့် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-6.png

upload အောင်မြင်ပြီးနောက် အစိမ်းရောင် LED2 သည် blink စတင်လုပ်သင့်ပါသည်။

Firmware ကို Debug လုပ်ခြင်း
------------------------------

သင့် board ကို debug လုပ်ရန် အလွယ်ကူဆုံးသော နည်းလမ်းကို :ref:`piodebug`
က ပေးအပ်ပါသည်။ debugging session ကို စတင်ရန် ``PlatformIO Quick Access``
menu ရှိ ``Start debugging`` option၊ top menu ရှိ ``Debug: Start
debugging`` သို့မဟုတ် hotkey ခလုတ် ``F5`` ကို အသုံးပြုနိုင်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-7.png

PlatformIO သည် debug session ကို initialize လုပ်နေစဉ် အချိန်အနည်းငယ်
စောင့်ရန် လိုအပ်ပြီး main function ၏ ပထမဆုံး line ကို highlight
ပြသောအခါ debug ပြုလုပ်ရန် အသင့်ဖြစ်ပါပြီ -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-8.png

control ခလုတ်များကို အသုံးပြု၍ code ကို တစ်လှမ်းချင်း လျှောက်ကြည့်နိုင်ပြီး၊
breakpoint များ သတ်မှတ်နိုင်ပြီး၊ peripheral register များကို ကြည့်နိုင်ပြီး
``Watch window`` သို့ variable များ ထည့်နိုင်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-9.png

Unit Test များ ရေးသားခြင်း
-----------------------------

ယခု target board ပေါ်တွင် code ကို တိုက်ရိုက် test လုပ်ရန် ကူညီပေးနိုင်သော
:ref:`unit_testing` solution ကို အသုံးပြု၍ test အချို့ ရေးကြပါစို့။
:ref:`unit_testing_frameworks_unity` testing framework ကို အသုံးပြုပါမည်။
:ref:`framework_stm32cube` framework အတွက် default configuration
မရှိသောကြောင့် :ref:`unit_testing_frameworks_unity_custom_config` ကို
ပေးအပ်ပါမည်။

ထို့အပြင် test များနှင့် custom :ref:`unit_testing_frameworks_unity`
configuration (နောက်တွင် ဖော်ပြထားသည်) ရှိမည့် folder အသစ် ``test``
ကို ဖန်တီးရန် လိုအပ်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-10.png

``ST Nucleo-F401RE`` board ပေါ်ရှိ ``USART2`` ကို အသုံးပြုပါမည်၊
အဘယ်ကြောင့်ဆိုသော် ၎င်းသည် STLink debug interface နှင့် တိုက်ရိုက်
ချိတ်ဆက်ထားပြီး OS တွင် Virtual Com Port အဖြစ် မြင်နိုင်သောကြောင့်
additional USB-UART converter မလိုအပ်ပါ။ custom
:ref:`unit_testing_frameworks_unity` configuration ကို implement
လုပ်ရန် ကျွန်ုပ်တို့၏ project ၏ root folder ရှိ
:ref:`projectconf_pio_test_dir` တွင် file နှစ်ခု ``unity_config.h``
နှင့် ``unity_config.c`` ကို ဖန်တီးပြီး ထားရန် လိုအပ်ပါသည်။

``unity_config.h`` ၏ Implementation:

.. code:: cpp

  #ifndef UNITY_CONFIG_H
  #define UNITY_CONFIG_H

  #ifndef NULL
  #ifndef __cplusplus
  #define NULL (void*)0
  #else
  #define NULL 0
  #endif
  #endif

  #ifdef __cplusplus
  extern "C"
  {
  #endif

  void unityOutputStart();
  void unityOutputChar(char);
  void unityOutputFlush();
  void unityOutputComplete();

  #define UNITY_OUTPUT_START()    unityOutputStart()
  #define UNITY_OUTPUT_CHAR(c)    unityOutputChar(c)
  #define UNITY_OUTPUT_FLUSH()    unityOutputFlush()
  #define UNITY_OUTPUT_COMPLETE() unityOutputComplete()

  #ifdef __cplusplus
  }
  #endif /* extern "C" */

  #endif /* UNITY_CONFIG_H */

``unity_config.c`` ၏ Implementation:

.. code:: cpp

  #include "unity_config.h"
  #include "stm32f4xx_hal.h"

  #define USARTx USART2
  #define USARTx_CLK_ENABLE() __HAL_RCC_USART2_CLK_ENABLE()
  #define USARTx_CLK_DISABLE() __HAL_RCC_USART2_CLK_DISABLE()
  #define USARTx_RX_GPIO_CLK_ENABLE() __HAL_RCC_GPIOA_CLK_ENABLE()
  #define USARTx_TX_GPIO_CLK_ENABLE() __HAL_RCC_GPIOA_CLK_ENABLE()
  #define USARTx_RX_GPIO_CLK_DISABLE() __HAL_RCC_GPIOA_CLK_DISABLE()
  #define USARTx_TX_GPIO_CLK_DISABLE() __HAL_RCC_GPIOA_CLK_DISABLE()

  #define USARTx_FORCE_RESET() __HAL_RCC_USART2_FORCE_RESET()
  #define USARTx_RELEASE_RESET() __HAL_RCC_USART2_RELEASE_RESET()

  #define USARTx_TX_PIN GPIO_PIN_2
  #define USARTx_TX_GPIO_PORT GPIOA
  #define USARTx_TX_AF GPIO_AF7_USART2
  #define USARTx_RX_PIN GPIO_PIN_3
  #define USARTx_RX_GPIO_PORT GPIOA
  #define USARTx_RX_AF GPIO_AF7_USART2

  static UART_HandleTypeDef UartHandle;

  void unityOutputStart()
  {
    GPIO_InitTypeDef GPIO_InitStruct;

    USARTx_TX_GPIO_CLK_ENABLE();
    USARTx_RX_GPIO_CLK_ENABLE();

    USARTx_CLK_ENABLE();

    GPIO_InitStruct.Pin = USARTx_TX_PIN;
    GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;
    GPIO_InitStruct.Pull = GPIO_PULLUP;
    GPIO_InitStruct.Speed = GPIO_SPEED_FAST;
    GPIO_InitStruct.Alternate = USARTx_TX_AF;

    HAL_GPIO_Init(USARTx_TX_GPIO_PORT, &GPIO_InitStruct);

    GPIO_InitStruct.Pin = USARTx_RX_PIN;
    GPIO_InitStruct.Alternate = USARTx_RX_AF;

    HAL_GPIO_Init(USARTx_RX_GPIO_PORT, &GPIO_InitStruct);
    UartHandle.Instance = USARTx;

    UartHandle.Init.BaudRate = 115200;
    UartHandle.Init.WordLength = UART_WORDLENGTH_8B;
    UartHandle.Init.StopBits = UART_STOPBITS_1;
    UartHandle.Init.Parity = UART_PARITY_NONE;
    UartHandle.Init.HwFlowCtl = UART_HWCONTROL_NONE;
    UartHandle.Init.Mode = UART_MODE_TX_RX;
    UartHandle.Init.OverSampling = UART_OVERSAMPLING_16;

    if (HAL_UART_Init(&UartHandle) != HAL_OK)
    {
      while (1)
      {
      }
    }
  }

  void unityOutputChar(char c)
  {
    HAL_UART_Transmit(&UartHandle, (uint8_t *)(&c), 1, 1000);
  }

  void unityOutputFlush() {}

  void unityOutputComplete()
  {
    USARTx_CLK_DISABLE();
    USARTx_RX_GPIO_CLK_DISABLE();
    USARTx_TX_GPIO_CLK_DISABLE();
  }

ယခု test case အချို့ ထည့်ရန် လိုအပ်ပါသည်။ test များကို test
အများအပြားပါဝင်နိုင်သော C file တစ်ခုတည်းထဲသို့ ထည့်နိုင်ပါသည်။
ပထမဦးစွာ default function သုံးခု ထည့်ရန် လိုအပ်ပါသည် - ``setUp``,
``tearDown`` နှင့် ``main``။ ``setUp`` နှင့် ``tearDown`` တို့ကို
test condition များ initialize လုပ်ရန်နှင့် finalize လုပ်ရန်
အသုံးပြုပါသည်။ ဤ function များကို implement လုပ်ရန် test run
ရန်အတွက် မလိုအပ်သော်လည်း test တစ်ခု run ခြင်းမပြုမီ variable
အချို့ initialize လုပ်ရန် လိုအပ်ပါက ``setUp`` function ကို
အသုံးပြုပြီး variable များ ရှင်းလင်းရန် လိုအပ်ပါက ``tearDown``
function ကို အသုံးပြုပါ။ ကျွန်ုပ်တို့၏ ဥပမာတွင် ဤ function များကို
LED ကို အသီးသီး initialize လုပ်ရန်နှင့် deinitialize လုပ်ရန်
အသုံးပြုပါမည်။ ``main`` function သည် ကျွန်ုပ်တို့၏ test plan ကို
ဖော်ပြသည့် ရိုးရှင်းသော program တစ်ခုကဲ့သို့ လုပ်ဆောင်ပါသည်။

``test`` folder ထဲသို့ file အသစ် ``test_main.c`` ကို ထည့်ကြပါစို့။
blinking routine အတွက် အခြေခံ test များကို ဤ file တွင်
အကောင်အထည်ဖော်ပါမည် -

* ``test_led_builtin_pin_number`` က ``LED_PIN`` သည် မှန်ကန်သော value
  ရှိကြောင်း သေချာစေပါသည်
* ``test_led_state_high`` က ``GPIO_PIN_SET`` value ဖြင့် function
  ``HAL_GPIO_WritePin`` နှင့် ``HAL_GPIO_ReadPin`` ကို test လုပ်ပါသည်
* ``test_led_state_low`` က ``GPIO_PIN_RESET`` value ဖြင့် function
  ``HAL_GPIO_WritePin`` နှင့် ``HAL_GPIO_ReadPin`` ကို test လုပ်ပါသည်

.. note::
  * board သည် ``Serial.DTR/RTS`` မှတစ်ဆင့် software resetting ကို
    မပံ့ပိုးသောကြောင့် ၂ စက္ကန့် delay လိုအပ်ပါသည်

.. code:: cpp

  #include "../src/main.h"
  #include <unity.h>

  void setUp(void)
  {
    LED_GPIO_CLK_ENABLE();
    GPIO_InitTypeDef GPIO_InitStruct;
    GPIO_InitStruct.Pin = LED_PIN;
    GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
    GPIO_InitStruct.Pull = GPIO_PULLUP;
    GPIO_InitStruct.Speed = GPIO_SPEED_HIGH;
    HAL_GPIO_Init(LED_GPIO_PORT, &GPIO_InitStruct);
  }

  void tearDown(void)
  {
    HAL_GPIO_DeInit(LED_GPIO_PORT, LED_PIN);
  }

  void test_led_builtin_pin_number(void)
  {
    TEST_ASSERT_EQUAL(GPIO_PIN_5, LED_PIN);
  }

  void test_led_state_high(void)
  {
    HAL_GPIO_WritePin(LED_GPIO_PORT, LED_PIN, GPIO_PIN_SET);
    TEST_ASSERT_EQUAL(GPIO_PIN_SET, HAL_GPIO_ReadPin(LED_GPIO_PORT, LED_PIN));
  }

  void test_led_state_low(void)
  {
    HAL_GPIO_WritePin(LED_GPIO_PORT, LED_PIN, GPIO_PIN_RESET);
    TEST_ASSERT_EQUAL(GPIO_PIN_RESET, HAL_GPIO_ReadPin(LED_GPIO_PORT, LED_PIN));
  }

  int main()
  {
    HAL_Init();      // HAL library ကို initialize လုပ်ပါ
    HAL_Delay(2000); // ဝန်ဆောင်မှု delay

    UNITY_BEGIN();
    RUN_TEST(test_led_builtin_pin_number);

    for (unsigned int i = 0; i < 5; i++)
    {
      RUN_TEST(test_led_state_high);
      HAL_Delay(500);
      RUN_TEST(test_led_state_low);
      HAL_Delay(500);
    }

    UNITY_END(); // unit testing ကို ရပ်တန့်ခြင်း

    while (1)
    {
    }
  }

  void SysTick_Handler(void)
  {
    HAL_IncTick();
  }


ယခု board ပေါ်သို့ test များ upload လုပ်ရန် အသင့်ဖြစ်ပါပြီ။ ၎င်းအတွက်
Project Tasks menu ရှိ ``Test`` option၊ top menu ရှိ ``Tasks: Run Task...
> PlatformIO Test`` option သို့မဟုတ် :ref:`ide_vscode_toolbar` ရှိ
Test ခလုတ်ကို အသုံးပြုနိုင်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-11.png

processing ပြီးနောက် testing ရလဒ်များအကြောင်း အသေးစိတ် report ကို
တွေ့ရမည် ဖြစ်ပါသည် -

.. image:: ../../_static/images/tutorials/ststm32/stm32cube-debugging-unit-testing-12.png

ဂုဏ်ယူပါသည်! report မှ တွေ့ရသည့်အတိုင်း ကျွန်ုပ်တို့၏ test အားလုံး
အောင်မြင်ခဲ့ပါသည်!

နိဂုံးချုပ်ချက်
----------------

ယခု ကျွန်ုပ်တို့တွင် နောက်ပိုင်း ပိုမိုရှုပ်ထွေးသော project များအတွက်
တိုးတက်အောင် ပြုလုပ်နိုင်သော လျောက်ပတ်သော template တစ်ခု ရရှိပြီ
ဖြစ်ပါသည်။

Project ၏ Source Code
------------------------

ဤ tutorial ၏ source code ကို
https://github.com/platformio/platformio-examples/tree/develop/unit-testing/stm32cube
တွင် ရနိုင်ပါသည်။
