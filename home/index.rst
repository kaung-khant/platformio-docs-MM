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

.. |PIOHOME| replace:: **PlatformIO Home**

.. _piohome:

PlatformIO Home
================

|PIOHOME| သည် PlatformIO ပူးပေါင်းဆောင်ရွက်သည့် platform အတွက် အားကောင်းသော၊
ခေတ်မီပြီး interactive ဖြစ်သော user interface (UI) တစ်ခု ဖြစ်ပါသည်။ ၎င်းကို
`PlatformIO Labs's Modern UI Toolkit <https://piolabs.com/technology/modern-ui-toolkit.html>`_
က အားဖြည့်ပေးထားပြီး အောက်ပါ အဓိက instrument များ ပါဝင်ပါသည် -

* :ref:`pioaccount`
* Project စီမံခန့်ခွဲမှု (Project Management)
* :ref:`librarymanager`
* :ref:`platforms`၊ :ref:`frameworks` နှင့် :ref:`boards` စီမံခန့်ခွဲမှု
* :ref:`Device စီမံခန့်ခွဲမှု <cmd_device>` (serial, logical, နှင့် multicast DNS service များ)
* Static Code Analysis
* Firmware File Explorer
* Firmware Memory Inspection
* Firmware Sections & Symbols Viewer။

.. contents:: မာတိကာ
    :local:

Install ပြုလုပ်ခြင်း
----------------------

|PIOHOME| ကို သီးခြား install ပြုလုပ်ရန် မလိုအပ်ပါ၊ ၎င်းသည် :ref:`pioide`
နှင့် :ref:`piocore` တွင် built-in အဖြစ် ပါဝင်ပြီးသား ဖြစ်ပါသည်။

လျင်မြန်စွာ စတင်ခြင်း
------------------------

PlatformIO IDE
~~~~~~~~~~~~~~~

PlatformIO Toolbar ပေါ်ရှိ (HOME) ခလုတ်ကို အသုံးပြု၍ |PIOHOME| ကို
ဖွင့်ပါ -

* **VSCode**: :ref:`ide_vscode_toolbar`

PlatformIO Core
~~~~~~~~~~~~~~~~

:ref:`cmd_home` command ကို အသုံးပြု၍ |PIOHOME| Web-server ကို launch
လုပ်ပြီး သင့် browser တွင် http://127.0.0.1:8008 ကို ဖွင့်ပါ။

host နှင့် port ကို ပြောင်းလဲနိုင်ပါသည်။ အသေးစိတ်အချက်အလက်များအတွက်
:ref:`cmd_home` command ကို စစ်ဆေးပါ။

သရုပ်ပြများ
------------

Welcome & Project Manager
~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: ../_static/images/home/pio-home-welcome.png

Project Inspect
~~~~~~~~~~~~~~~

Statistics
''''''''''

.. image:: ../_static/images/home/pio-home-inspect-stats.png

code analysis (:ref:`check`) သာလျှင်

.. image:: ../_static/images/home/pio-home-inspect-stats-check.png

Firmware File Explorer
''''''''''''''''''''''

.. image:: ../_static/images/home/pio-home-inspect-firmware-file-explorer.png

File Symbols

.. image:: ../_static/images/home/pio-home-inspect-firmware-file-explorer-symbols.png

Firmware Symbols
''''''''''''''''

.. image:: ../_static/images/home/pio-home-inspect-firmware-symbols.png

Firmware Sections
''''''''''''''''''

.. image:: ../_static/images/home/pio-home-inspect-firmware-sections.png

Static Code Analysis
''''''''''''''''''''

.. image:: ../_static/images/home/pio-home-inspect-code-defects.png

Library Manager
~~~~~~~~~~~~~~~~

.. image:: ../_static/images/home/pio-home-library-stats.png

Board Explorer
~~~~~~~~~~~~~~~

.. image:: ../_static/images/home/pio-home-boards.png
