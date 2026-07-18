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

.. _tutorial_espressif32_espidf_debugging_unit_testing_analysis:

ESP-IDF နှင့် ESP32-DevKitC ဖြင့် စတင်အသုံးပြုခြင်း - debugging၊ unit testing၊ project analysis
====================================================================================================

ဤ tutorial ၏ ရည်ရွယ်ချက်မှာ ``ESP32-DevKitC`` board အတွက် :ref:`framework_espidf`
framework ဖြင့် ရိုးရှင်းသော Wi-Fi project တစ်ခုကို develop လုပ်ခြင်း၊ run
ခြင်းနှင့် debug လုပ်ရန် :ref:`ide_vscode` ကို အသုံးပြုရန် မည်မျှလွယ်ကူကြောင်း
ပြသရန် ဖြစ်ပါသည်။

* **အဆင့်:** အလယ်အလတ် (Intermediate)
* **Platform များ:** Windows, Mac OS X, Linux

**လိုအပ်ချက်များ:**

- :ref:`ide_vscode` ကို download လုပ်ပြီး install ပြုလုပ်ထားရန်
- :ref:`board_espressif32_esp32dev`
- ပြင်ပ debug adapter တစ်ခု (ဥပမာ - :ref:`debugging_tool_olimex-arm-usb-ocd`)

.. contents:: မာတိကာ
    :local:

Project ကို စတင်ပြင်ဆင်ခြင်း
------------------------------

#.  PlatformIO Toolbar အောက်ခြေရှိ "PlatformIO Home" ခလုတ်ကို နှိပ်ပါ -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-1.png

#.  "New Project" ကို နှိပ်ပြီး development board အဖြစ် ``Espressif ESP32
    Dev Module``၊ framework အဖြစ် :ref:`framework_espidf` နှင့် project
    တည်နေရာလမ်းကြောင်း (သို့မဟုတ် default ကို အသုံးပြုနိုင်သည်) ကို
    ရွေးချယ်ပါ -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-2.png

ဖန်တီးထားသော Project ထဲသို့ Code ထည့်သွင်းခြင်း
--------------------------------------------------

#.  :ref:`projectconf_pio_src_dir` folder တွင် file အသစ် ``main.c`` ကို
    ဖန်တီးပြီး အောက်ပါ code ကို ထည့်ပါ -

    .. code-block:: c

        /*  WiFi softAP ဥပမာ

           ဤ ဥပမာ code သည် Public Domain တွင်ရှိသည် (သို့မဟုတ် သင့်ရွေးချယ်မှု
           အလိုက် CC0 လိုင်စင်ရရှိသည်။)

           သက်ဆိုင်ရာဥပဒေအရ လိုအပ်ခြင်း သို့မဟုတ် စာဖြင့်သဘောတူထားခြင်း
           မရှိပါက၊ ဤ software သည် "AS IS" အခြေအနေအတိုင်း ဖြန့်ချိသည်ဖြစ်ပြီး၊
           မည်သည့်အာမခံချက် သို့မဟုတ် စည်းကမ်းသတ်မှတ်ချက်မျှ တိုက်ရိုက်ဖြစ်စေ၊
           သွယ်ဝိုက်၍ဖြစ်စေ မပါဝင်ပါ။
        */
        #include <string.h>
        #include "freertos/FreeRTOS.h"
        #include "freertos/task.h"
        #include "esp_mac.h"
        #include "esp_wifi.h"
        #include "esp_event.h"
        #include "esp_log.h"
        #include "nvs_flash.h"

        #include "lwip/err.h"
        #include "lwip/sys.h"

        /* ဤ ဥပမာများသည် project configuration menu မှတစ်ဆင့် သတ်မှတ်နိုင်သော
           WiFi configuration ကို အသုံးပြုပါသည်။

           သင်ထိုသို့ မလိုလားပါက အောက်ပါ entry များကို သင်လိုချင်သော config
           ပါသော string များအဖြစ် ပြောင်းလိုက်ရုံပါပဲ - ဥပမာ #define
           EXAMPLE_WIFI_SSID "mywifissid"
        */
        #define EXAMPLE_ESP_WIFI_SSID      "mywifissid"
        #define EXAMPLE_ESP_WIFI_PASS      "mywifipass"
        #define EXAMPLE_ESP_WIFI_CHANNEL   1
        #define EXAMPLE_MAX_STA_CONN       4

        static const char *TAG = "wifi softAP";

        static void wifi_event_handler(void* arg, esp_event_base_t event_base,
                                            int32_t event_id, void* event_data)
        {
            if (event_id == WIFI_EVENT_AP_STACONNECTED) {
                wifi_event_ap_staconnected_t* event = (wifi_event_ap_staconnected_t*) event_data;
                ESP_LOGI(TAG, "station "MACSTR" join, AID=%d",
                         MAC2STR(event->mac), event->aid);
            } else if (event_id == WIFI_EVENT_AP_STADISCONNECTED) {
                wifi_event_ap_stadisconnected_t* event = (wifi_event_ap_stadisconnected_t*) event_data;
                ESP_LOGI(TAG, "station "MACSTR" leave, AID=%d",
                         MAC2STR(event->mac), event->aid);
            }
        }

        void wifi_init_softap(void)
        {
            ESP_ERROR_CHECK(esp_netif_init());
            ESP_ERROR_CHECK(esp_event_loop_create_default());
            esp_netif_create_default_wifi_ap();

            wifi_init_config_t cfg = WIFI_INIT_CONFIG_DEFAULT();
            ESP_ERROR_CHECK(esp_wifi_init(&cfg));

            ESP_ERROR_CHECK(esp_event_handler_instance_register(WIFI_EVENT,
                                                                ESP_EVENT_ANY_ID,
                                                                &wifi_event_handler,
                                                                NULL,
                                                                NULL));

            wifi_config_t wifi_config = {
                .ap = {
                    .ssid = EXAMPLE_ESP_WIFI_SSID,
                    .ssid_len = strlen(EXAMPLE_ESP_WIFI_SSID),
                    .channel = EXAMPLE_ESP_WIFI_CHANNEL,
                    .password = EXAMPLE_ESP_WIFI_PASS,
                    .max_connection = EXAMPLE_MAX_STA_CONN,
                    .authmode = WIFI_AUTH_WPA_WPA2_PSK,
                    .pmf_cfg = {
                            .required = false,
                    },
                },
            };
            if (strlen(EXAMPLE_ESP_WIFI_PASS) == 0) {
                wifi_config.ap.authmode = WIFI_AUTH_OPEN;
            }

            ESP_ERROR_CHECK(esp_wifi_set_mode(WIFI_MODE_AP));
            ESP_ERROR_CHECK(esp_wifi_set_config(WIFI_IF_AP, &wifi_config));
            ESP_ERROR_CHECK(esp_wifi_start());

            ESP_LOGI(TAG, "wifi_init_softap finished. SSID:%s password:%s channel:%d",
                     EXAMPLE_ESP_WIFI_SSID, EXAMPLE_ESP_WIFI_PASS, EXAMPLE_ESP_WIFI_CHANNEL);
        }

        void app_main(void)
        {
            //NVS ကို Initialize လုပ်ပါ
            esp_err_t ret = nvs_flash_init();
            if (ret == ESP_ERR_NVS_NO_FREE_PAGES || ret == ESP_ERR_NVS_NEW_VERSION_FOUND) {
              ESP_ERROR_CHECK(nvs_flash_erase());
              ret = nvs_flash_init();
            }
            ESP_ERROR_CHECK(ret);

            ESP_LOGI(TAG, "ESP_WIFI_MODE_AP");
            wifi_init_softap();
        }

    .. warning::
        ဤ file အသစ် ``main.c`` ကို ``src/CMakeLists.txt`` file ရှိ
        ``idf_component_register`` function ဖြင့် source file အဖြစ်
        register လုပ်ထားကြောင်း သေချာပါစေ -

        .. code-block:: cmake

          idf_component_register(SRCS "main.c")

#.  project ကို compile လုပ်ရန် အောက်ပါ option များထဲမှ တစ်ခုကို
    အသုံးပြုပါ -

    - ``Project Tasks`` menu ရှိ Build option
    - :ref:`ide_vscode_toolbar` ရှိ Build ခလုတ်
    - Task Menu ``Tasks: Run Task... > PlatformIO: Build`` (သို့) :ref:`ide_vscode_toolbar` တွင်
    - Command Palette ``View: Command Palette > PlatformIO: Build``
    - Hotkeys ``cmd-alt-b / ctrl-alt-b``:

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-3.png

#.  အားလုံးအဆင်ပြေပါက terminal window တွင် အောင်မြင်ကြောင်း ရလဒ် message
    ကို တွေ့ရမည် ဖြစ်ပါသည် -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-4.png

#.  firmware ကို board ပေါ်သို့ upload လုပ်ရန် အောက်ပါ option များကို
    အသုံးပြုနိုင်ပါသည် -

    - ``Project Tasks`` menu ရှိ Upload option
    - :ref:`ide_vscode_toolbar` ရှိ Upload ခလုတ်
    - Command Palette ``View: Command Palette > PlatformIO: Upload``
    - Task Menu ``Tasks: Run Task... > PlatformIO: Upload``
    - Hotkeys ``cmd-alt-u / ctrl-alt-u``:

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-5.png

#.  board ကို သင့် ကွန်ပျူတာသို့ ချိတ်ဆက်ပြီး ``platformio.ini`` file ရှိ
    default monitor speed ကို ``115200`` သို့ update လုပ်ပါ -

    .. code-block:: ini

      [env:esp32dev]
      platform = espressif32
      board = esp32dev
      framework = espidf
      monitor_speed = 115200

#.  board မှ output ကို ကြည့်ရှုရန် Serial Monitor ကို ဖွင့်ပါ -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-6.png

#.  အားလုံးအဆင်ပြေပါက board သည် WiFi access point တစ်ခုအဖြစ် မြင်နိုင်သင့်ပါသည် -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-7.png

Firmware ကို Debug လုပ်ခြင်း
------------------------------

Hardware ကို စတင်ပြင်ဆင်ခြင်း
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`piodebug` ကို အသုံးပြုရန်အတွက် ပြင်ပ JTAG probe နှင့် board ကို
အောက်ပါ pin များဖြင့် ချိတ်ဆက်ရန် လိုအပ်ပါသည် -

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

#.  :ref:`projectconf` တွင် :ref:`projectconf_debug_tool` ကို သတ်မှတ်ပါ။
    ဤ tutorial တွင် :ref:`debugging_tool_olimex-arm-usb-ocd-h` debug probe
    ကို အသုံးပြုထားပါသည် -

    .. code-block:: ini

      [env:esp32dev]
      platform = espressif32
      board = esp32dev
      framework = espidf
      monitor_speed = 115200
      debug_tool = olimex-arm-usb-ocd-h

#.  debug session ကို စတင်ရန် အောက်ပါ method များကို အသုံးပြုနိုင်ပါသည် -

    * top menu ရှိ ``Debug: Start debugging``
    * Quick Access menu ရှိ ``Start Debugging`` option
    * hotkey ခလုတ် ``F5``:

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-8.png

#.  control ခလုတ်များကို အသုံးပြု၍ code ကို တစ်လှမ်းချင်း လျှောက်ကြည့်ပါ၊
    breakpoint များ သတ်မှတ်ပြီး ``Watch window`` သို့ variable များ
    ထည့်ပါ -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-9.png

Unit Test များ ရေးသားခြင်း
-----------------------------

.. note::
    function ``setUp`` နှင့် ``tearDown`` တို့ကို test condition များ
    initialize လုပ်ရန်နှင့် finalize လုပ်ရန် အသုံးပြုပါသည်။ ဤ function
    များကို implement လုပ်ရန် test run ရန်အတွက် မလိုအပ်သော်လည်း test
    တစ်ခု run ခြင်းမပြုမီ variable အချို့ initialize လုပ်ရန် လိုအပ်ပါက
    ``setUp`` function ကို အသုံးပြုပြီး variable များ ရှင်းလင်းရန်
    လိုအပ်ပါက ``tearDown`` function ကို အသုံးပြုပါ။

ရိုးရှင်းစေရန် ``calculator`` ဟု အမည်ရှိသော library သေးငယ်တစ်ခု
ဖန်တီးပြီး အခြေခံ function များ ``addition``, ``subtraction``,
``multiplication``, ``division`` တို့ကို implement လုပ်ကာ PlatformIO
:ref:`unit_testing` solution ကို အသုံးပြု၍ ၎င်းတို့ကို test လုပ်ကြပါစို့။

#.  :ref:`projectconf_pio_lib_dir` folder တွင် folder အသစ် ``calculator``
    ကို ဖန်တီးပြီး file အသစ်နှစ်ခု ``calculator.h`` နှင့် ``calculator.c``
    ကို အောက်ပါ content များဖြင့် ထည့်ပါ -

    ``calculator.h``:

    .. code-block:: c

      #ifndef _CALCULATOR_H_
      #define _CALCULATOR_H_

      #ifdef __cplusplus
      extern "C"
      {
      #endif

        int addition(int a, int b);
        int subtraction(int a, int b);
        int multiplication(int a, int b);
        int division(int a, int b);

      #ifdef __cplusplus
      }
      #endif

      #endif // _CALCULATOR_H_


    ``calculator.c``:

    .. code-block:: c

      #include "calculator.h"

      int addition(int a, int b)
      {
        return a + b;
      }

      int subtraction(int a, int b)
      {
        return a - b;
      }

      int multiplication(int a, int b)
      {
        return a * b;
      }

      int division(int a, int b)
      {
        return a / b;
      }

#.  :ref:`projectconf_pio_test_dir` folder တွင် file အသစ် ``test_calc.c``
    ကို ဖန်တီးပြီး ``calculator`` library အတွက် အခြေခံ test များ ထည့်ပါ -

    .. code-block:: c

      #include <calculator.h>
      #include <unity.h>

      void setUp(void)
      {
        // ဒီနေရာမှာ လိုအပ်တာတွေ setup လုပ်ပါ
      }

      void tearDown(void)
      {
        // ဒီနေရာမှာ ရှင်းလင်းရမယ့်အရာတွေ ရှင်းလင်းပါ
      }

      void test_function_calculator_addition(void)
      {
        TEST_ASSERT_EQUAL(32, addition(25, 7));
      }

      void test_function_calculator_subtraction(void)
      {
        TEST_ASSERT_EQUAL(20, subtraction(23, 3));
      }

      void test_function_calculator_multiplication(void)
      {
        TEST_ASSERT_EQUAL(50, multiplication(25, 2));
      }

      void test_function_calculator_division(void)
      {
        TEST_ASSERT_EQUAL(32, division(100, 3));
      }

      void app_main()
      {
        UNITY_BEGIN();

        RUN_TEST(test_function_calculator_addition);
        RUN_TEST(test_function_calculator_subtraction);
        RUN_TEST(test_function_calculator_multiplication);
        RUN_TEST(test_function_calculator_division);

        UNITY_END();
      }

#.  board ပေါ်တွင် test များကို run ပြီး ရလဒ်များကို စစ်ဆေးကြပါစို့။
    ``test_function_calculator_division`` test တွင် ပြဿနာတစ်ခု
    ရှိသင့်ပါသည် -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-10.png

#.  မှားယွင်းနေသော expected value ကို ပြင်ဆင်ပြီး test များကို ထပ်မံ
    run ကြပါစို့။ processing ပြီးနောက် ရလဒ်များ မှန်ကန်သင့်ပါသည် -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-11.png

Project စစ်ဆေးခြင်း (Inspection)
-----------------------------------

ရှင်းလင်းပြရန်အတွက် memory footprint အကြီးဆုံးရှိသော function တစ်ခုကို
ရှာဖွေရန် လိုအပ်သည်ဟု စိတ်ကူးကြပါစို့။ ထို့အပြင် :ref:`check` က report
တင်နိုင်ရန် ကျွန်ုပ်တို့၏ project ထဲသို့ bug တစ်ခု ထည့်ကြပါစို့။

#.  ``PlatformIO Home`` ကို ဖွင့်ပြီး ``Inspect`` section သို့ သွားကာ
    လက်ရှိ project ကို ရွေးချယ်ပြီး ``Inspect`` ခလုတ်ကို နှိပ်ပါ -

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-12.png

#.  Project စာရင်းအင်းများ (Statistics):

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-13.png

#.  အကြီးဆုံး function:

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-14.png

#.  ဖြစ်နိုင်ချေရှိသော bug များ:

    .. image:: ../../_static/images/tutorials/espressif32/espidf-debugging-unit-testing-analysis-15.png

နိဂုံးချုပ်ချက်
----------------

ယခု ကျွန်ုပ်တို့တွင် ``ESP32-DevKitC`` board အတွက် နောက်ပိုင်း project
များအတွက် boilerplate အဖြစ် အသုံးပြုနိုင်သော project template တစ်ခု
ရရှိပြီ ဖြစ်ပါသည်။
