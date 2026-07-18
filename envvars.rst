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

.. _envvars:

Environment Variables (ပတ်ဝန်းကျင်ကိန်းရှင်များ)
==================================================

`Environment variables (ပတ်ဝန်းကျင်ကိန်းရှင်များ)
<http://en.wikipedia.org/wiki/Environment_variable>`_ ဆိုသည်မှာ
ကွန်ပျူတာပေါ်တွင် အလုပ်လုပ်နေသော process များ၏ အပြုအမူကို အကျိုးသက်ရောက်စေနိုင်သည့်
dynamic အမည်ပါ value အစုအဝေးများ ဖြစ်ပါသည်။ PlatformIO သည် ``PLATFORMIO_``
ဟူသော prefix ဖြင့်စတင်သော variable များကို ကိုင်တွယ်ပါသည်။

environment variable ကို မည်သို့ set လုပ်ရမည်နည်း။

.. code-block:: bash

    # Windows တွင်
    set VARIABLE_NAME=VALUE

    # Windows GUI ဖြင့် -> https://www.youtube.com/watch?v=bEroNNzqlF4

    # Unix (bash, zsh) တွင်
    export VARIABLE_NAME=VALUE

    # Unix (fish) တွင်
    set -x VARIABLE_NAME VALUE

.. contents:: မာတိကာ
    :local:

အထွေထွေ
-------

PlatformIO သည် ဘုံလုပ်ဆောင်ချက်/command များအတွက် *General* (အထွေထွေ)
environment variable များကို အသုံးပြုပါသည်။

.. envvar:: CI

PlatformIO သည် `Continuous Integration (ဆက်တိုက်ပေါင်းစည်းခြင်း)
<http://en.wikipedia.org/wiki/Continuous_integration>`_ (Travis, Circle
စသည်) system များက setup လုပ်ပေးသော ``CI`` variable ကို ကိုင်တွယ်ပါသည်။
PlatformIO သည် prompt များနှင့် progress bar များကို ပိတ်ရန် ၎င်းကို
အသုံးပြုပါသည်။ တစ်နည်းအားဖြင့် ``CI=true`` သည် :envvar:`PLATFORMIO_DISABLE_PROGRESSBAR`
ကို ``true`` အဖြစ် အလိုအလျောက် setup လုပ်ပေးပါသည်။

.. envvar:: PLATFORMIO_AUTH_TOKEN

:ref:`pioaccount` သို့ auto login ဝင်ရောက်ရန် အသုံးပြုနိုင်သော Personal
Authentication Token ကို သတ်မှတ်ခွင့်ပြုပါသည်။ ၎င်းသည် ကိုယ်တိုင် authorize
လုပ်ရန် မဖြစ်နိုင်သည့် :ref:`ci` system များနှင့် :ref:`pioremote`
operation များအတွက် အလွန်အသုံးဝင်ပါသည်။

သင့်ကိုယ်ပိုင် Personal Authentication Token ကို :ref:`cmd_account_token`
command ဖြင့် ရယူနိုင်ပါသည်။

.. envvar:: PLATFORMIO_FORCE_ANSI

output သည် ``tty`` မဟုတ်ဘဲ ``pipe`` ဖြစ်နေလျှင်တောင် ANSI control character
ကို output ထုတ်ရန် အတင်းအကြပ်ပြုလုပ်ပါသည်။ ဖြစ်နိုင်သော value များမှာ
``true`` နှင့် ``false`` ဖြစ်ပါသည်။ Default မှာ ``PLATFORMIO_FORCE_ANSI=false``
ဖြစ်ပါသည်။

.. envvar:: PLATFORMIO_NO_ANSI

ANSI control character များကို မထုတ်ပြပါနှင့်။ ဖြစ်နိုင်သော value များမှာ
``true`` နှင့် ``false`` ဖြစ်ပါသည်။ Default မှာ ``PLATFORMIO_NO_ANSI=false``
ဖြစ်ပါသည်။

:ref:`piocore` အတွက် :option:`pio --no-ansi` flag ကိုလည်း အသုံးပြုနိုင်ပါသည်။

.. envvar:: PLATFORMIO_DISABLE_PROGRESSBAR

package/library downloader နှင့် uploader အတွက် progress bar ကို ပိတ်ပါသည်။
၎င်းသည် PlatformIO ကို subprocess မှ ခေါ်ယူပြီး output သည် ``tty`` မဟုတ်ဘဲ
``pipe`` ဖြစ်နေချိန်တွင် အသုံးဝင်ပါသည်။ ဖြစ်နိုင်သော value များမှာ ``true``
နှင့် ``false`` ဖြစ်ပါသည်။ Default မှာ ``PLATFORMIO_DISABLE_PROGRESSBAR=false``
ဖြစ်ပါသည်။

.. envvar:: PLATFORMIO_DISABLE_UPGRADE_CHECK

upgrade availability စစ်ဆေးမှုများကို ပိတ်ပါသည်။ ဖြစ်နိုင်သော value များမှာ
``true`` နှင့် ``false`` ဖြစ်ပါသည်။ Default မှာ
``PLATFORMIO_DISABLE_UPGRADE_CHECK=false`` ဖြစ်ပါသည်။

.. envvar:: PLATFORMIO_SYSTEM_TYPE

ဤ environment variable သည် automatic detection ကို override လုပ်ပြီး
system type ကို ကိုယ်တိုင် သတ်မှတ်ခွင့်ပြုပါသည်။
ဥပမာများ -

* ``windows_amd64``
* ``windows_arm64``
* ``linux_x86_64``
* ``linux_armv7l``
* ``darwin_arm64``

.. envvar:: PLATFORMIO_RUN_JOBS

:option:`pio run --jobs` ကို override လုပ်ခွင့်ပြုပါသည်။

Directory များ
---------------

.. envvar:: PLATFORMIO_CORE_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_core_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

အကျိုးသက်ရောက်ရန် :ref:`piocore` ကို ပြန်လည် install ပြုလုပ်ရန် (default
core directory ကို ဖျက်ရန်) လိုအပ်နိုင်ပါသည်။

.. envvar:: PLATFORMIO_GLOBALLIB_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_globallib_dir` option ကို
override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_PLATFORMS_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_platforms_dir` option ကို
override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_PACKAGES_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_packages_dir` option ကို
override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_CACHE_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_cache_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_BUILD_CACHE_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_build_cache_dir` option ကို
override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_WORKSPACE_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_workspace_dir` option ကို
override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_INCLUDE_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_include_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SRC_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_src_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_LIB_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_lib_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_LIBDEPS_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_libdeps_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_BUILD_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_build_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_DATA_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_data_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_TEST_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_test_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_BOARDS_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_boards_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_MONITOR_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_monitor_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SHARED_DIR

:ref:`projectconf` ၏ :ref:`projectconf_pio_shared_dir` option ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_REMOTE_AGENT_DIR

:option:`pio remote agent start --working-dir` ကို override လုပ်ခွင့်ပြုပါသည်။

Build ပြုလုပ်ခြင်း
--------------------

.. envvar:: PLATFORMIO_BUILD_FLAGS

:ref:`projectconf` ၏ :ref:`projectconf_build_flags` option ကို set
လုပ်ခွင့်ပြုပါသည်။

ဥပမာများ -

.. code-block:: bash

    # Unix တွင်:
    export PLATFORMIO_BUILD_FLAGS=-DFOO
    export PLATFORMIO_BUILD_FLAGS=-DFOO -DBAR=1 -Wall

    # Windows တွင်:
    SET PLATFORMIO_BUILD_FLAGS=-DFOO
    SET PLATFORMIO_BUILD_FLAGS=-DFOO -DBAR=1 -Wall

.. warning::

    ထပ်ဆောင်း build flag များတွင် special character (``$``၊ ``&``၊ ``~``
    စသည်) ပါဝင်သော preprocessor directive များပါလျှင် ``PLATFORMIO_BUILD_FLAGS``
    environment variable အစား :ref:`projectconf_interpolation` ကို
    အသုံးပြုရန် စဉ်းစားပါ။

.. envvar:: PLATFORMIO_BUILD_SRC_FLAGS

:ref:`projectconf` ၏ :ref:`projectconf_build_src_flags` option ကို set
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_BUILD_SRC_FILTER

:ref:`projectconf` ၏ :ref:`projectconf_build_src_filter` option ကို set
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_EXTRA_SCRIPTS

:ref:`projectconf` ၏ :ref:`projectconf_extra_scripts` option ကို set
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_DEFAULT_ENVS

:ref:`projectconf` ၏ :ref:`projectconf_pio_default_envs` option ကို set
လုပ်ခွင့်ပြုပါသည်။

Upload ပြုလုပ်ခြင်း
---------------------

.. envvar:: PLATFORMIO_UPLOAD_PORT

:ref:`projectconf` ၏ :ref:`projectconf_upload_port` option ကို set
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_UPLOAD_FLAGS

:ref:`projectconf` ၏ :ref:`projectconf_upload_flags` option ကို set
လုပ်ခွင့်ပြုပါသည်။


Setting များ
-------------

PlatformIO setting များကို override လုပ်ခွင့်ပြုပါသည်။ ၎င်းတို့ကို
:ref:`cmd_settings` command ဖြင့် စီမံခန့်ခွဲနိုင်ပါသည်။

.. envvar:: PLATFORMIO_SETTING_CHECK_PLATFORMIO_INTERVAL

setting :ref:`setting_check_platformio_interval` ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_CHECK_PRUNE_SYSTEM_THRESHOLD

setting :ref:`setting_check_prune_system_threshold` ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_ENABLE_CACHE

setting :ref:`setting_enable_cache` ကို override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_ENABLE_TELEMETRY

setting :ref:`setting_enable_telemetry` ကို override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_FORCE_VERBOSE

setting :ref:`setting_force_verbose` ကို override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_PROJECTS_DIR

setting :ref:`setting_projects_dir` ကို override လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_ENABLE_PROXY_STRICT_SSL

setting :ref:`setting_enable_proxy_strict_ssl` ကို override
လုပ်ခွင့်ပြုပါသည်။

.. envvar:: PLATFORMIO_SETTING_DISABLE_UDEV_RULES_CHECK

setting :ref:`setting_disable_udev_rules_check` ကို override
လုပ်ခွင့်ပြုပါသည်။
