# TrashFire 
(by trash we mean the stuff you find in the bottom of a port-o-potty!)

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
```
https://www.op-tee.org
https://github.com/OP-TEE/optee_os/blob/master/documentation/globalplatform_api.md
https://github.com/linaro-swg/hello_world
https://github.com/linaro-swg/optee_examples
https://linux.globallogic.com/materials2017/presentations/Stream%202/Igor%20Opaniuk.%20OP-TEE.pdf
```

Several OP-TEE releated artifacts can be found on the file system. 

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

Several obvious TrustZone artifacts are left around... 
```
/system/bin/xtest:TEE test application started with device [%s]

```

The output from Xtest seems to match this variant (note the repo source!)
```
BOOMERANG: Exploiting the Semantic Gap in Trusted Execution Environments
https://github.com/ucsb-seclab/boomerang/blob/master/optee/optee_test/host/xtest/xtest_1000.c#L616
```

# Facewall
![When FacePalm Isn't enough](https://img.memecdn.com/facewall_fb_708311.jpg)

That moment you need a Meat Space security helper for your Trust Zone procedures... Donny forgot to clean up the djita TZTA files!

```
$ binwalk wm230_01.00.0100/TrustZone/0388301d-7a5b-4153-968c3a668ae6cdd8.ta

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------

$ binwalk wm230_01.00.0100/TrustZone/0388301d-7a5b-4153-968c3a668ae6cdd8.ta.TZTA 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
308           0x134           ELF, 32-bit LSB shared object, ARM, version 1 (SYSV)
73588         0x11F74         CRC32 polynomial table, little endian
```

Food for thought
https://googleprojectzero.blogspot.com/2017/07/trust-issues-exploiting-trustzone-tees.html
https://www.cs.ucsb.edu/~vigna/publications/2017_NDSS_Boomerang.pdf (mentioned above)

# Trusted Applications 
https://www.ietf.org/proceedings/99/slides/slides-99-edu-sessi-trusted-execution-environments-tee-and-the-open-trust-protocol-otrp-00.pdf
https://www.owasp.org/images/c/c8/OWASP_Security_Tapas_-_TrustZone%2C_TEE_and_Mobile_Security_final.pdf
https://www.slideshare.net/linaroorg/hkg15311-optee-for-beginners-and-porting-review
https://wiki.linaro.org/GlobalPlatform
https://www.globalplatform.org/specificationsdevice.asp
https://www.commoncriteriaportal.org/files/ppfiles/PP%20TEE%20v1.2.1_20161215.pdf
https://www.slideshare.net/linaroorg/lcu14103-how-to-create-and-run-trusted-applications-on-optee
https://www.youtube.com/watch?v=QgaGJow7hws
https://github.com/OP-TEE/optee_os/commit/d0c636148b3a
https://github.com/OP-TEE/optee_os/blob/master/documentation/optee_design.md#12-trusted-applications

```There are two ways to implement Trusted Applications (TAs), pseudo TAs and user mode TAs. User mode TAs are full featured Trusted Applications as specified by the GlobalPlatform TEE specifications, these are simply referred to as 'Trusted Applications'. For most cases, user mode TAs are preferred.```

https://wiki.linaro.org/WorkingGroups/Security/OP-TEE
# How Are Trusted Applications Verified?
https://github.com/OP-TEE/optee_os/blob/master/documentation/optee_design.md#8-pager
```
ta_load >> ta_store->open >> ta_open >> check_shdr >> crypto_ops.acipher.rsassa_verify
```

https://github.com/OP-TEE/optee_os/blob/master/core/arch/arm/kernel/user_ta.c#L261
```
 * Loads TA header and hashes.
 * Verifies the TA signature.
 * Returns context ptr and TEE_Result.
static TEE_Result ta_load(const TEE_UUID *uuid,
			  const struct user_ta_store_ops *ta_store,
			  struct tee_ta_ctx **ta_ctx)
```

https://github.com/OP-TEE/optee_os/blob/master/core/arch/arm/kernel/ree_fs_ta.c#L100
```static TEE_Result ta_open(const TEE_UUID *uuid,
			  struct user_ta_store_handle **h)
          /* Request TA from tee-supplicant */
```

https://github.com/OP-TEE/optee_os/blob/master/documentation/optee_design.md#12-trusted-applications

File format of a Dynamic Trusted Application (unpacked TZTA files)
The format a TA is:
```
<Signed header>
<ELF>
Where <ELF> is the content of a standard ELF file and <Signed header> consists of:

Type	Name	Comment
uint32_t	magic	Holds the magic number 0x4f545348
uint32_t	img_type	image type, values defined by enum shdr_img_type
uint32_t	img_size	image size in bytes
uint32_t	algo	algorithm, defined by public key algorithms TEE_ALG_ from TEE Internal API specification
uint16_t	hash_size	size of the signed hash
uint16_t	sig_size	size of the signature
uint8_t[hash_size]	hash	Hash of the fields above and the <ELF> above
uint8_t[sig_size]	signature	Signature of hash
```

# What Exactly Is A Static TA Anyway? How Different Is It Than A Regular Globalplatform Defined (Dynamic) TA?
```
A static TA is just an interface exposing special services in optee_os core to dynamic TAs and clients. It is code inside the TEE core. As such, it does not have its own address space and can corrupt the whole TEE if poorly written. Also it is usually more difficult to upgrade than a dynamic (user) TA which is a file in the normal world file system.
On the other hand, a static TA can access the hardware directly by calling any driver code inside the TEE core. This means you may use a static TA to extend the services offered by the GP Internal API, without adding any new system call.
Client Applications (CAs) in the normal world can communicate with static TAs in the same way they communicate with dynamic TAs. Dynamic TAs can also communicate with static TAs in the same way they communicate with other dynamic TAs, using GP Internal API. Static TAs, however, cannot communicate back to dynamic TAs due to the absence of GP Internal API in optee_os core code.
```

