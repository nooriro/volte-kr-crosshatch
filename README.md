# VoLTE in KR for Pixel 3/XL

Systemlessly activates __VoLTE__ (Voice over LTE) on South Korean carriers

* __SKT__ (SK Telecom)
* __KT__
* __LGU__ (LG Uplus)

for __blueline__ (Google Pixel 3) and __crosshatch__ (Google Pixel 3 XL).


## Prerequisite

If you're using __PQ2A.190205.001 (February 2019 build) or later__ build, __flash “radio-180917”__  first (or anytime) via fastboot mode.
```
adb reboot bootloader <Enter>
fastboot flash radio radio-crosshatch-g845-00023-180917-b-5014671.img <Enter>
fastboot reboot <Enter>
```
* You can get `radio-crosshatch-g845-00023-180917-b-5014671.img` (simply __“radio-180917”__) file from [the factory image of PQ1A.190105.004 (January 2019 build)](https://dl.google.com/dl/android/aosp/crosshatch-pq1a.190105.004-factory-7165155c.zip). See [Factory Images for Nexus and Pixel Devices](https://developers.google.com/android/images) webpage.

* For use on the __SKT__ network, this is __not mandatory__. But doing this is recommended in case of replacing SKT SIM card with KT/LGU SIM card.


## VoLTE Activation
[Install Magisk](https://topjohnwu.github.io/Magisk/install.html) if [Magisk](https://github.com/topjohnwu/Magisk/releases) is not installed, since this is a Magisk module. Then,
1. __Install__ this module on Magisk and __reboot__ system.
2. After reboot, unlock the screen and __wait 15 seconds__.
3. Test VoLTE call and SMS. (optional)
4. __Uninstall__ this module on Magisk and __reboot__ system.
   * Even if you uninstall this module from Magisk, you can still use VoLTE on KR carriers.  

After VoLTE activation, you may uninstall Magisk. Without Magisk you can still use VoLTE, again. Of course, you can continue to use Magisk without uninstalling it, for root features and so on.


## OTA System Updates

1. For system updates via OTA, you need to __restore the stock radio of current build__.
   ```
   adb reboot bootloader <Enter>
   fastboot flash radio stock-radio-of-current-build.img <Enter>
   fastboot reboot <Enter>
   ```

   * You can get `stock-radio-of-current-build.img` file from the factory image with build number you're currently using. __Know your build number__ and see [Factory Images for Nexus and Pixel Devices](https://developers.google.com/android/images) page again.


2. Do OTA __system updates completely__, including reboot system.

3. After system updates, __flash “radio-180917”__ (`radio-crosshatch-g845-00023-180917-b-5014671.img`) __again__ via fastboot mode. (See above [Prerequisite](https://github.com/Magisk-Modules-Repo/volte-kr-crosshatch/blob/master/README.md#prerequisite))

4. __Test VoLTE__ call and SMS.

5. If VoLTE is not working correctly, __re-activate VoLTE with Magisk and this module__. (See above [VoLTE Activation](https://github.com/Magisk-Modules-Repo/volte-kr-crosshatch/blob/master/README.md#volte-activation).)


## Known Issues

Switching between __SKT__ SIM and __KT__ SIM repeatedly, __VoLTE__ works on __one carrier__ and __CSFB__(circuit-switched fallback) occurs on __other carrier__.
* SKT (First, VoLTE) > __KT (VoLTE)__ > __SKT (CSFB to 3G)__ > KT (VoLTE) > ⋯
* KT (First, VoLTE) > __SKT (VoLTE)__ > __KT (CSFB to 3G)__ > SKT (VoLTE) > ⋯

If you have an __LGU__ SIM card, you can bypass this problem by __sandwitching__ it.
* ⋯ > KT (VoLTE) > SKT (CSFB to 3G) > ⋯
* ⋯ > __KT (VoLTE)__ > `LGU (VoLTE)` > __SKT (VoLTE)__ > ⋯
* ⋯ > SKT (VoLTE) > KT (CSFB to 3G) > ⋯
* ⋯ > __SKT (VoLTE)__ > `LGU (VoLTE)` > __KT (VoLTE)__ > ⋯

Otherwise, __re-activate VoLTE using Magisk and this module__ with proper SIM card inserted. (See above [VoLTE Activation](https://github.com/Magisk-Modules-Repo/volte-kr-crosshatch/blob/master/README.md#volte-activation).)


## VoLTE Deactivation

1. If you didn't uninstall this module yet, uninstall it and reboot system.
2. Remove `fdr_check` file in `/data/vendor/modem_fdr` directory (Root required.) and reboot system.

Note that uninstalling only this module does not deactivate VoLTE on KR carriers.


## Update History

#### v1.01-20190630
* Support device check on Android Q

#### v1.00-20190601
* First release
* Source(s) of __carrier-specific modem configuration__ (`mcfg_sw.mbn`) files :
  * SKT, KT : [Razer Phone 2 - Global Factory Image](https://developer.razer.com/razer-phone-dev-tools/factory-images/) | [P-MR1-RC003-RZR-190305.3110](https://s3.amazonaws.com/cheryl-factory-images/aura-p-global-3110.zip)
  * LGU : [Xiaomi Poco F1 - Global Stable ROM](https://en.miui.com/download-355.html) | [V10.3.4.0.PEJMIXM](http://bigota.d.miui.com/V10.3.4.0.PEJMIXM/miui_POCOF1Global_V10.3.4.0.PEJMIXM_13b169ae13_9.0.zip)


## Acknowledgments

Thanks to : [Occy](https://m.cafe.naver.com/CommentView.nhn?search.clubid=26545115&search.articleid=159482&search.refcommentid=34700816&search.commentid=34700816&search.menuid=454&search.focus=true&search.showCafeHome=true&search.perPage=5#focusing) and [Chinese developers](https://www.google.com/search?newwindow=1&q=fdr_check)
