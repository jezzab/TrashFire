# TrashFire (by trash we mean the stuff you find in the bottom of a port-o-potty!)
Mavic Air Firmware modules packaged with a system running GPL busy box binaries... 

DJI is currently in *active* violation of GPL *again*... these binaries are intended to be distributed to end users that have purchased a Mavic Air drone,and are seeking to downgrade their aircraft back to its factory state.

![Fresh Steamy Hot Trash](https://pbs.twimg.com/media/DV3mfwTVwAAiA_w.jpg)

This is a continuation of the flagrant disregard for GPL that has been going on for a number of years by DJI as a company. It was a pile of poo last summer, why not light it on fire!? 


DJI has been made aware that they are in violation a number of times, they flat out do NOT care:
https://github.com/MAVProxyUser/dji_system.bin/blob/master/GPL.md

# Current Firmware
```
Drones:
wm230 - Mavic Air

Folder: 	   Version:
wm230_00.02.0026 - V00.02.0026
wm230_00.02.0032 - V00.02.0032
wm230_01.00.0100 - V01.00.0100	
wm230_01.00.0200 - V01.00.0200
```

# DJI GPL Team 
If you are having problems getting responses from opensource@dji.com regarding GPL issues, use these addresses for the @dji-sdk OpenSource Team: 
```
Yin.Cheung <Yin.Cheung@dji.com>
Logan Wang <xiaodan.wang@dji.com>
Owen <cheng.ouyang@dji.com>
Ted.Liu(刘岿然) <ted.liu@dji.com>
```

This "Open Source Software" page by DJI is a joke... https://www.dji.com/opensource

Several of *us* (Slack OGs) will continue to practice "compliance via 0day" until DJI stops the egregious and cavalier violations. 

# TrustZone

Rather than do the right thing, and comply with GPL, DJI has decided to step up the game on its local security
https://www.arm.com/products/security-on-arm/trustzone

Each firmware folder above will also inclue an archive of the .tz files and any other TrustZone artifacts that DJI leaves behind. 

We can already tell they have added OP-TEE support to busybox ftpd for encryption of the files. 
https://www.op-tee.org
https://github.com/OP-TEE/optee_os/blob/master/documentation/globalplatform_api.md
https://github.com/linaro-swg/hello_world
https://github.com/linaro-swg/optee_examples
https://linux.globallogic.com/materials2017/presentations/Stream%202/Igor%20Opaniuk.%20OP-TEE.pdf

```
root@eagle_wm230:/ # busybox find / -name "*tee*"
/data/tee
/data/teec.log
/system/bin/tee
/system/bin/tee-supplicant
/system/bin/tee_helloworld
/system/lib/libteec.so
/sys/bus/platform/devices/optee
/sys/bus/platform/drivers/optee
/sys/bus/platform/drivers/optee/optee
/sys/devices/platform/optee
/sys/devices/platform/optee/tee
/sys/devices/platform/optee/tee/tee0
/sys/devices/platform/optee/tee/teepriv0
/sys/class/tee
/sys/class/tee/tee0
/sys/class/tee/teepriv0
/sys/firmware/devicetree/base/optee
/sys/firmware/devicetree/base/reserved-memory/optee_ramconsole
/sys/firmware/devicetree/base/reserved-memory/optee_rsv_region
/sys/kernel/debug/clk/tee_cc_ao_clk
/sys/kernel/debug/clk/tee_clk
/sys/module/tee
/sys/module/optee
/dev/teepriv0
/dev/tee0
```

