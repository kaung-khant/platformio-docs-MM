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

.. _what_is_pio:

PlatformIO ဆိုတာ ဘာလဲ?
========================

**Developer များနှင့် Team များ အစစ်အမှန် လွတ်လပ်မှုရရှိနိုင်သည့် နေရာ! Vendor တစ်ခုတည်းကိုသာ မှီခိုနေရတော့မည် မဟုတ်ပါ!**

.. contents:: မာတိကာ
    :local:

PlatformIO သည် embedded systems အင်ဂျင်နီယာများနှင့် embedded ထုတ်ကုန်များအတွက်
application များ ရေးသားသည့် software developer များအတွက် ရည်ရွယ်သော
cross-platform၊ cross-architecture၊ framework အမျိုးမျိုးကို ပံ့ပိုးပေးသည့်
ပရော်ဖက်ရှင်နယ် tool တစ်ခု ဖြစ်ပါသည်။

ဆုများ
------

PlatformIO သည် `2015/16 IoT Awards တွင် အကောင်းဆုံး Software and Tools
<http://www.postscapes.com/2015-16/best-iot-software-and-tools/>`_ အဖြစ်
ကိုယ်စားလှယ်အဖြစ် ရွေးချယ်ခံခဲ့ရပါသည်။

Microsoft :ref:`ide_vscode` editor အတွက် native `PlatformIO IDE extension
<https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide>`__
သည် Microsoft Marketplace တစ်ခုလုံးတွင် ငါးကြယ်ပွင့် review 2,500 ကျော်ဖြင့်
အများဆုံး rating/review ရရှိထားသော extension ဖြစ်ပါသည်။ ထို့အပြင် ကမ္ဘာတစ်ဝှမ်းရှိ
developer 3,000,000 ကျော်ကလည်း install လုပ်ခဲ့ကြပါသည်။

ဒဿနအယူအဆ
----------

embedded market တွင် PlatformIO ၏ထူးခြားသော ဒဿနအယူအဆက developer များအား
cross-platform အဖြစ် အလုပ်လုပ်နိုင်သည့်၊ software development kit (SDK)
သို့မဟုတ် :ref:`frameworks` အမျိုးမျိုးကို ပံ့ပိုးပေးနိုင်သည့်၊ ခေတ်မီသော
integrated development environment (:ref:`ide`) တစ်ခုကို ပေးအပ်ပါသည်။
၎င်းတွင် ကျွမ်းကျင်သော debugging (:ref:`piodebug`)၊ unit testing
(:ref:`unit_testing`)၊ automated code analysis (:ref:`check`) နှင့်
remote management (:ref:`pioremote`) တို့ ပါဝင်ပါသည်။ ၎င်းကို graphical
သို့မဟုတ် command line editor (:ref:`piocore`) တစ်ခုခု (သို့) နှစ်ခုလုံးကို
ရွေးချယ်အသုံးပြုနိုင်သော developer များအတွက် flexibility နှင့် ရွေးချယ်ခွင့်ကို
အများဆုံးရရှိစေရန် ဒီဇိုင်းပြုလုပ်ထားပါသည်။

PlatformIO သည် platform တစ်ခုထက်ပို၍ solution များ ဖန်တီးသော ပရော်ဖက်ရှင်နယ်
embedded systems အင်ဂျင်နီယာများအတွက် မရှိမဖြစ် လိုအပ်သော tool တစ်ခု ဖြစ်ပါသည်။
ထို့အပြင် decentralized architecture ရှိခြင်းကြောင့် PlatformIO သည် developer
အသစ်များနှင့် လက်ရှိ developer များအတွက် commercial ဖြစ်ရန် အသင့်ဖြစ်နေသော
ထုတ်ကုန်များ ဖန်တီးရန် လျင်မြန်သော ပေါင်းစည်းလမ်းကြောင်းကို ပေးအပ်ပြီး၊
overall time-to-market ကို လျှော့ချပေးပါသည်။

ထို့ပြင် ၎င်းသည် သင်နှစ်သက်ရာ ခေတ်မီ operating system (macOS၊ MS Windows၊
Linux၊ FreeBSD) မည်သည့်တစ်ခုပေါ်တွင်မဆို run နိုင်ပါသည်။

နည်းပညာများ
------------

PlatformIO သည် အတွေ့အကြုံရင့်ကျက်သော hardware အင်ဂျင်နီယာများက အချိန်ကြာမြင့်စွာ
(မကြာခဏ ဆင်းရဲဒုက္ခခံ၍) လေ့လာသင်ယူခဲ့ရသည့် ရှုပ်ထွေးသော software tool များဖြင့်
ရိုးရာအားဖြင့် ဝန်ဆောင်မှုပေးလာခဲ့သည့် embedded market အတွက် နောက်ဆုံးပေါ်
scalable ဖြစ်ပြီး flexible ဖြစ်သော software နည်းပညာကို အသုံးချပါသည်။
ထိုအစား PlatformIO ဖြင့် အသုံးပြုသူများသည် hobbyist ဖြစ်စေ၊ ပရော်ဖက်ရှင်နယ်
ဖြစ်စေ ဖြစ်နိုင်ပါသည်။ သူတို့သည် ရိုးရာ Arduino "Blink" sketch ကို import
လုပ်နိုင်သလို commercial ထုတ်ကုန်တစ်ခုအတွက် ကျွမ်းကျင်သော low-level embedded
C program ကိုလည်း ဖန်တီးနိုင်ပါသည်။ ပံ့ပိုးပေးထားသော framework မည်သည့်
တစ်ခုအတွက်မဆို ဥပမာ code ကို compile လုပ်ပြီး မိနစ်အနည်းငယ်အတွင်း target
platform သို့ upload လုပ်နိုင်ပါသည်။

build system ဖွဲ့စည်းပုံသည် software dependency များကို အလိုအလျောက် tag
လုပ်ပြီး ပုံမှန်ရှုပ်ထွေးမှုနှင့် ဒုက္ခများကို ဖယ်ရှားပေးသည့် modular
hierarchy တစ်ခုကို အသုံးပြု၍ ၎င်းတို့ကို အသုံးချပေးပါသည်။ Developer
များသည် သတ်မှတ်ထားသော target အတွက် application များ ဖန်တီးရန် toolchain၊
compiler နှင့် library dependency များ၏ environment ကို ကိုယ်တိုင်
ရှာဖွေစုစည်းရန် မလိုအပ်တော့ပါ။ PlatformIO ဖြင့် compile ခလုတ်ကို
နှိပ်လိုက်ရုံဖြင့် လိုအပ်သော dependency အားလုံးကို အလိုအလျောက်
ယူဆောင်လာပေးပါသည်။ ဥပမာဆိုရလျှင် သင်သည် ပရိဘောဂဒီဇိုင်နာတစ်ဦးဖြစ်ပြီး
သင့် CAD program တွင် "build" ခလုတ်တစ်ခုရှိကာ ၎င်းက robot တစ်ခုအား
လိုအပ်သော အစိတ်အပိုင်းများနှင့် ပစ္စည်းများ အားလုံးကို ယူဆောင်စေပြီး
မှန်ကန်စွာ တပ်ဆင်ပေးစေသကဲ့သို့ ဖြစ်ပါသည်။

:ref:`piocore` သည် developer များက သတ်မှတ်ထားသော SDK သို့မဟုတ် ဥပမာ
embedded application တစ်ခု၏ နယ်နိမိတ်ကို ကျော်လွန်သွားချိန်တွင် ကြုံတွေ့ရလေ့
ရှိသော software integration၊ packaging နှင့် library dependency များ၏
ပုံမှန်ဒုက္ခများကို ဖယ်ရှားပေးသည့် အစအဆုံး ကိုယ်တိုင်တီထွင်ထားသော ထူးခြားသည့်
build system တစ်ခု ဖြစ်ပါသည်။ ၎င်းကို code development environment
အမျိုးမျိုးနှင့်အတူ အသုံးပြုနိုင်ပြီး cloud platform နှင့် web service
feed များစွာနှင့် လွယ်ကူစွာ ပေါင်းစည်းနိုင်စေပါသည်။ အသုံးပြုသူသည်
လျင်မြန်စွာ စတင်ရာတွင် မည်သည့်အတားအဆီးမျှ ကြုံတွေ့ရမည် မဟုတ်ပါ -
**license ကြေးလည်း မရှိ၊ ဥပဒေရေးရာ စာချုပ်များလည်း မရှိပါ**။ tool
များသည် open source ဖြစ်ပြီး ပွင့်လင်းစွာ လိုင်စင်ရရှိထားသောကြောင့်
(ပြင်ဆင်ရန် ခွင့်ပြုချက် မလိုအပ်ဘဲ၊ ပြောင်းလဲချက်များကို မျှဝေရန်လည်း
မလိုအပ်ပါ) အသုံးပြုသူသည် build environment ၏ အပြည့်အဝ flexibility ကို
ထိန်းသိမ်းထားနိုင်ပါသည်။

ပြဿနာရှိသောအချက်များ
---------------------

* embedded ကမ္ဘာမှ လူများကို ဝေးကွာစေသော အဓိကပြဿနာမှာ သတ်မှတ်ထားသော
  MCU/board တစ်ခုအတွက် development software ကို setup လုပ်ရသည့်
  ရှုပ်ထွေးသော လုပ်ငန်းစဉ် ဖြစ်ပါသည် - toolchain များ၊ (တစ်ခါတစ်ရံ
  အခမဲ့မဟုတ်သော) vendor ပိုင်ဆိုင်သည့် IDE၊ ထို့အပြင် ထို software ကို
  ပံ့ပိုးပေးနိုင်သည့် OS ပါသော ကွန်ပျူတာတစ်လုံးကို ရရှိရန်ပါဝင်ပါသည်။
* Hardware platform များစွာ (MCU၊ board) တို့သည် toolchain၊ IDE
  စသည်တို့ ကွဲပြားစွာ လိုအပ်ပြီး၊ ယင်းအတွက် development environment
  အသစ်များကို လေ့လာရန် အချိန်ကုန်ရပါသည်။
* လူကြိုက်များသော sensor၊ actuator စသည်တို့ကို မည်သို့အသုံးပြုရမည်ကို
  ပြသသည့် သင့်လျော်သော library များနှင့် code sample များကို
  ရှာဖွေရခြင်း။
* team member များ ကြိုက်နှစ်သက်သည့် operating system မည်သည့်တစ်ခု
  ဖြစ်စေ၊ ၎င်းတို့ကြား embedded project များကို မျှဝေရခြင်း။

ဘယ်လိုအလုပ်လုပ်သလဲ?
--------------------

PlatformIO ၏ အသေးစိတ် အကောင်အထည်ဖော်မှုထဲသို့ အလွန်နက်နက်ရှိုင်းရှိုင်း
မဝင်ဘဲ၊ PlatformIO ကို အသုံးပြု၍ ဖန်တီးထားသော project တစ်ခု၏ လုပ်ငန်းစဉ်မှာ
အောက်ပါအတိုင်း ဖြစ်ပါသည် -

* အသုံးပြုသူများသည် :ref:`projectconf` တွင် စိတ်ဝင်စားသော board(s) ကို
  ရွေးချယ်ပါသည်
* ဤ board စာရင်းကို အခြေခံ၍ PlatformIO သည် လိုအပ်သော toolchain များကို
  download လုပ်ပြီး အလိုအလျောက် install လုပ်ပါသည်။
* အသုံးပြုသူများသည် code ကို ဖန်တီးကြပြီး PlatformIO က ၎င်းကို compile
  လုပ်ခြင်း၊ ပြင်ဆင်ခြင်းနှင့် စိတ်ဝင်စားသော board အားလုံးသို့ upload
  လုပ်ခြင်းတို့ ဖြစ်စေကြောင်း သေချာစေပါသည်။
