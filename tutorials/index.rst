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

.. _tutorials:

Tutorial များနှင့် ဥပမာများ
============================

တရားဝင် (Official)
--------------------

Tutorial များ
~~~~~~~~~~~~~~

.. toctree::
    :maxdepth: 1

    espressif32/arduino_debugging_unit_testing
    espressif32/espidf_debugging_unit_testing_analysis
    ststm32/stm32cube_debugging_unit_testing
    nordicnrf52/arduino_debugging_unit_testing
    nordicnrf52/zephyr_debugging_unit_testing_inspect
    core/unit_testing_blink
    riscv/riscv_asm_video_tutorial

Project ဥပမာများ
~~~~~~~~~~~~~~~~~~

source code ပါသော pre-configured project များကို `PlatformIO Examples
<https://github.com/platformio/platformio-examples>`_ repository တွင်
ရနိုင်ပါသည်။

အသိုင်းအဝိုင်း (Community)
----------------------------

စာအုပ်များ
~~~~~~~~~~~

* `Developing IoT Projects with ESP32: Automate your home or business with inexpensive Wi-Fi devices <https://www.amazon.com/Developing-IoT-Projects-ESP32-inexpensive-ebook-dp-B093CCWGDP/dp/B093CCWGDP/>`_
  (:ref:`framework_espidf` ပါ PlatformIO ကို အသုံးပြုထားသည်)

Tutorial များ
~~~~~~~~~~~~~~

* `PlatformIO DIY Projects & Tutorials at Hackster.io <https://www.hackster.io/platformio/projects?utm_source=platformio.org&utm_medium=docs>`_

Video Tutorial များ
~~~~~~~~~~~~~~~~~~~~

* `Getting Started with PlatformIO <https://www.youtube.com/watch?v=JmvMvIphMnY>`_ - **အခြေခံလူသစ်များအတွက် အထူးအကြံပြုပါသည်**
* `PlatformIO Video Collection on YouTube <https://www.youtube.com/playlist?list=PLLnAiBnVrkALvk_IJhDBAQQuDozkj6C34>`_
* `Next-generation IDE for your RISC-V Product in 20 Minutes by CEO of PlatformIO <https://www.youtube.com/watch?v=0eYDKION0Bs>`_
* `Use the PlatformIO Debugger on the ESP32 Using an ESP-prog <https://www.hackster.io/brian-lough/use-the-platformio-debugger-on-the-esp32-using-an-esp-prog-f633b6>`_
* `RISC-V ASM Tutorial <https://www.youtube.com/playlist?list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY>`_
* `PlatformIO for Arduino, ESP8266, and ESP32 Tutorial <https://www.youtube.com/watch?v=0poh_2rBq7E>`_
* `Free Inline Debugging for ESP32 and Arduino Sketches <https://www.youtube.com/watch?v=psMqilqlrRQ>`__
* `PlatformIO или прощай, Arduino IDE <https://www.youtube.com/watch?v=OGCyKncOyNU>`_
* `Отладка ESP32 в PlatformIO <https://www.youtube.com/watch?v=rreMOwEJcII>`_
* `A Better Arduino IDE - Getting Started with PlatformIO <https://www.youtube.com/watch?v=EIkGTwLOD7o>`_
* `PlatformIO - Using External Libraries <https://www.youtube.com/watch?v=EBlHNBNHESQ>`_

Project များ
~~~~~~~~~~~~~

* `arendst/tasmota <https://github.com/arendst/tasmota/>`_ - webUI ဖြင့် လွယ်ကူသော
  configuration၊ OTA update များ၊ timer သို့မဟုတ် rule များကို အသုံးပြု၍
  automation၊ extensibility နှင့် MQTT၊ HTTP၊ Serial သို့မဟုတ် KNX
  အပေါ် လုံးဝ local ထိန်းချုပ်မှုပါရှိသော ESP8266 အတွက် အခြားရွေးချယ်စရာ
  firmware တစ်ခု
* `MarlinFirmware/Marlin <https://github.com/MarlinFirmware/Marlin>`_ - Arduino
  platform ကို အခြေခံသော RepRap 3D printer များအတွက် optimize
  ပြုလုပ်ထားသော firmware
* `scottbez1/smartknob <https://github.com/scottbez1/smartknob>`_ - software
  ဖြင့် သတ်မှတ်ထားသော endstop များနှင့် virtual detent များပါရှိသော
  haptic input knob
* `esphome/esphome <https://github.com/esphome/esphome>`_ - ရိုးရှင်းသော်လည်း
  အားကောင်းသော configuration file များဖြင့် သင့် ESP8266/ESP32 ကို
  ထိန်းချုပ်နိုင်ပြီး Home Automation system များမှတစ်ဆင့် အဝေးမှ
  ထိန်းချုပ်နိုင်သော system တစ်ခု
* `xoseperez/espurna <https://github.com/xoseperez/espurna>`_ - ESP8266
  အခြေခံ device များအတွက် home automation firmware တစ်ခု
* `1technophile/OpenMQTTGateway <https://github.com/1technophile/OpenMQTTGateway>`_ -
  bidirectional 433mhz/315mhz/868mhz၊ Infrared ဆက်သွယ်ရေး၊ BLE၊
  Bluetooth၊ beacon detection၊ mi flora၊ mi jia၊ LYWSD02၊ LYWSD03MMC၊
  Mi Scale၊ TPMS၊ BBQ thermometer နှင့် ကိုက်ညီမှု၊ SMS & LORA
  တို့ပါရှိသော ESP8266၊ ESP32၊ Sonoff RF Bridge သို့မဟုတ် Arduino
  အတွက် MQTT gateway
* `cyberman54/ESP32-Paxcounter <https://github.com/cyberman54/ESP32-Paxcounter>`_ -
  စျေးသက်သာသော ESP32 board များဖြင့် Wifi & BLE ကို အသုံးပြု၍
  ခရီးသည်စီးဆင်းမှု တိုင်းတာခြင်း။
