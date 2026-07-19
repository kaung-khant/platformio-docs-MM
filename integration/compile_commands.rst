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

.. _compilation_db:

Compilation Database ``compile_commands.json``
------------------------------------------------

`compilation database <https://clang.llvm.org/docs/JSONCompilationDatabase.html>`_
ဆိုသည်မှာ သင့် project ရှိ compilation unit တိုင်း၏ ဖွဲ့စည်းထားသော data
ကို ပါဝင်သည့် ``compile_commands.json`` ဟု အမည်ရှိသော `JSON-formatted
<https://www.json.org/>`_ file တစ်ခု ဖြစ်ပါသည်။

:option:`pio run --target` command နှင့် ``compiledb`` target ကို
အသုံးပြု၍ project ``compile_commands.json`` ကို generate လုပ်နိုင်ပါသည်။

``compile_commands.json`` အတွက် default တည်နေရာမှာ project directory
ဖြစ်ပါသည်။

:ref:`scripting` ကို အသုံးပြု၍ customization အတွက် အောက်ပါ build
variable များကို အသုံးပြုနိုင်ပါသည် -

.. list-table::
    :header-rows:  1
    :widths: 25 75

    * - Variable
      - ဖော်ပြချက် (Description)

    * - ``COMPILATIONDB_PATH``
      - ``compile_commands.json`` file ကို သိမ်းဆည်းသင့်သည့် path။
        default တည်နေရာမှာ project ၏ root ဖြစ်ပါသည်

    * - ``COMPILATIONDB_INCLUDE_TOOLCHAIN``
      - compilation unit တွင် toolchain path များ ထည့်သွင်းသင့်မသင့်
        ထိန်းချုပ်ရန် boolean flag။ default value မှာ ``False``
        ဖြစ်ပြီး project-dependent include များကိုသာ export လုပ်ပါသည်။

**ဥပမာ**

project environment တစ်ခုစီအတွက် toolchain include များပါသော
``compile_commands.json`` ကို generate လုပ်ပြီး database ကို
":ref:`projectconf_pio_build_dir`/envname" folder သို့ သိမ်းဆည်းပါ -

``platformio.ini``:

.. code-block:: ini

    [env:myenv]
    platform = ...
    board = ...
    extra_scripts = pre:extra_script.py

``extra_script.py``:

.. code-block:: python

    import os
    Import("env")

    # toolchain path များ ထည့်ပါ
    env.Replace(COMPILATIONDB_INCLUDE_TOOLCHAIN=True)

    # compilation DB path ကို override လုပ်ပါ
    env.Replace(COMPILATIONDB_PATH=os.path.join("$BUILD_DIR", "compile_commands.json"))

``compile_commands.json`` ကို Generate လုပ်ခြင်း

.. code::

  > pio run -t compiledb
