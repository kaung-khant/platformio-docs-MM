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

.. _tutorial_riscv_asm_video:

RISC-V ASM ဗီဒီယို Tutorial
=============================

Western Digital ၏ Chief Technology Officer ဖြစ်သူ Martin Fink မှ SiFive
:ref:`board_sifive_hifive1` ပေါ်တွင် :ref:`platform_sifive` နှင့် Assembly
language ကို အသုံးပြုနည်း နိဒါန်းတစ်ခု ဖြစ်ပါသည်။

Source File များ
------------------

Demo source code ကို Github တွင် ထုတ်ပြန်ထားပါသည်:
https://github.com/martin-robert-fink/superBlink.git
၎င်းသည် PlatformIO project အဖြစ် pre-configured လုပ်ပြီးသား ဖြစ်ပါသည် -

* ၎င်းကို clone လုပ်ပါ သို့မဟုတ် `download
  <https://github.com/martin-robert-fink/superBlink/archive/master.zip>`_
  လုပ်ပါ
* :ref:`ide_vscode` တွင် ဖွင့်ပါ
* coding နှင့် debugging ကို ပျော်ရွှင်စွာ လုပ်ဆောင်ပါ!

Video စုစည်းမှု
-----------------

.. image:: ../../_static/images/tutorials/riscv/riscv_asm_video_tutorial.jpg
	:target: https://www.youtube.com/playlist?list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY

* `အပိုင်း 1/12 | နိဒါန်း <https://www.youtube.com/watch?v=KLybwrpfQ3I&index=1&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY>`_
* `အပိုင်း 2/12 | စတင်ပြင်ဆင်ခြင်း <https://www.youtube.com/watch?v=daGHhrkF41U&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=2>`_
* `အပိုင်း 3/12 | PlatformIO ပတ်လည်ကြည့်ရှုခြင်း <https://www.youtube.com/watch?v=k3tpNwXEWhU&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=3>`_
* `အပိုင်း 4/12 | C Code Wrapper <https://www.youtube.com/watch?v=MnWI9qplfvA&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=4>`_
* `အပိုင်း 5/12 | HiFive Docs <https://www.youtube.com/watch?v=nqXRzUFnM9w&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=5>`_
* `အပိုင်း 6/12 | GPIO ကို နားလည်ခြင်း <https://www.youtube.com/watch?v=tthKXGxAUjY&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=6>`_
* `အပိုင်း 7/12 | setupGPIO <https://www.youtube.com/watch?v=90udyEHBiwg&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=7>`_
* `အပိုင်း 8/12 | setupGPIO ကို Debug လုပ်ခြင်း <https://www.youtube.com/watch?v=Xmes__VpfiA&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=8>`_
* `အပိုင်း 9/12 | setLED <https://www.youtube.com/watch?v=PMLqqRHpbsQ&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=9>`_
* `အပိုင်း 10/12 | setLED ကို Debug လုပ်ခြင်း <https://www.youtube.com/watch?v=6K1FZK1Kc5w&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=10>`_
* `အပိုင်း 11/12 | Delay <https://www.youtube.com/watch?v=edzX3c2r0YQ&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=11>`_
* `အပိုင်း 12/12 | နောက်ဆုံးအပိုင်းနှင့် နိဂုံးချုပ်ချက် <https://www.youtube.com/watch?v=C16UE8oTZY0&list=PL6noQ0vZDAdh_aGvqKvxd0brXImHXMuLY&index=12>`_
