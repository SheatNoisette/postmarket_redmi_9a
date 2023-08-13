# Xiaomi Redmi 9a hardware specifications

The phone is the EU version
Model: M2006C3LG
Codename: Dandelion

## How to be in preloader mode

Press and hold the both of the volume buttons while plugging the phone to 
the computer.

## Hardware

- Mediatek Helio G25 (MT6762G)
    - 12 nm
    - 400 - 2001 Mhz
    - AES/ASMID/NEON/PMULL/SHA1/SHA2
    - 2 Clusters (A53)
    - Revision r0p4
    - 8 cores
    - PowerVR Rogue GE8320 GLES 3.2 / OpenCL 1.2
    - CPUID: 0xF18B822D4CC42F1FAE4C3D17B9EC1285A30B0725
    - L1 data: 16ko
    - L1 Instruction: 16ko
    - L2: 256ko
- 2GB LPDDR3
    - 1795MB usable for Android
- NFC: No
- Modem
    - Bluetooth 5.0
    - Wifi
        - 2.4 Ghz: Yes
        - 5 Ghz: No
- 32GB eMMC storage
- 1600x720 IPS LCD (68x151mm / 269dpi / 60hz): nt36525b ???
    - hx83102d Controller ?
- 5000 mAh battery LiPo
- Rear-Facing Camera: Hynix hi1337
    - 13 MP Photo
    - 2.1 MP Video
    - 3.43 mm focal
    - Focus: Infinity, auto, macro, constinuous-video, continuous-picture
    - Flash
- Front Camera: hynix_hi259 ??? / ov ov02b ???
    - 5.0 MP Photo
    - 2.1 MP Video
    - 2.23mm focal
    - focus: Fixed, infinity
- Accelerometer: ???
- Proximity: ???
- Light sensors: ???
- Haptic motor
- FM Radio: MT6631_FM ???
- GPS
- OTG Support (From Android)
- Headphone jack

Others:
- 2 UARTS ? MT6577
- RT5509 Amplifier

## Software Out-Of-The-Box

Before messing with the phone, I made a backup of the system partition using
mtkclient. This will be useful if something goes wrong.

Everything presented here is from the stock ROM in the EU version of the phone
without any updates (Out-Of-The-Box).
This may not be the same for other versions released in other countries.

### Android reported

The phone is running Android 11, which is quite slow (but it's Android, so it's).

Some data from the phone:
- Android 11 (RP1A.200720.011)
    - Android ID: 13676d16cfe1d57d
- MIUI Global 12.5.5 Stable (V125)
- Android Security Update 2022-07-01
- Broadband version MOLY.LR12A.R3.MP.V134.1.P69
- Kernel 4.19.127-pref-g7288046673d5 (armv8l)

### boot.img

Reported by `file` on Linux:
```
boot.bin: Android bootimg, kernel (0x40080000), ramdisk (0x51b00000),
page size: 2048, cmdline (bootopt=64S3,32N2,64N2 buildvariant=user)
```

pmbootstrap generated offset from the boot.img:
```
deviceinfo_kernel_cmdline="bootopt=64S3,32N2,64N2 buildvariant=user"
deviceinfo_generate_bootimg="true"
deviceinfo_bootimg_qcdt="false"
deviceinfo_bootimg_mtk_mkimage="false"
deviceinfo_bootimg_dtb_second="false"
deviceinfo_flash_pagesize="2048"
deviceinfo_header_version="2"
deviceinfo_append_dtb="false"
deviceinfo_flash_offset_dtb="0x07808000"
deviceinfo_flash_offset_base="0x40078000"
deviceinfo_flash_offset_kernel="0x00008000"
deviceinfo_flash_offset_ramdisk="0x11a88000"
deviceinfo_flash_offset_second="0xbff88000"
deviceinfo_flash_offset_tags="0x07808000"
```

mkbootimg_tools report:
```
kernel         : kernel
ramdisk        : ramdisk
page size      : 2048
kernel size    : 13069731
ramdisk size   : 740132
dtb size       : 2
base           : 0x40078000
kernel offset  : 0x00008000
ramdisk offset : 0x11a88000
tags offset    : 0x07808000
dtb img        : dt.img
cmd line       : bootopt=64S3,32N2,64N2 buildvariant=user
ramdisk is gzip format.
```

Note that the DTB is not included in the boot.img, but in a separate file.

Sha256sum:
```
5c141824f8ef2e614449993d571fa9a66249f7a9b51a93795ad182c746acd4db  boot.bin
```

### Preloader / lk.bin

lk.bin is the preloader, which is the first thing that runs on the phone,
because the security on the Mediatek SoC is complete garbage, I was able to
dump it using mtkclient.

sha256sum:
```
a2fe9a4bd5f0644270187ba6b3daa8a0d2a7ab1612b49ab6dac989297d080d23  preloader.bin
```

### GPT Table

After dumping the preloader, I was able to dump the GPT table, which is
interesting because it contains the partition layout of the phone.

Dumped using mtkclient:
```
$ ./mtk printgpt
[...]
GPT Table:
-------------
boot_para:           Offset 0x0000000000008000, Length 0x0000000000100000, Flags 0x00000000, UUID f57ad330-39c2-4488-b09b-00cb43c9ccd4, Type EFI_BASIC_DATA
recovery:            Offset 0x0000000000108000, Length 0x0000000004000000, Flags 0x00000000, UUID fe686d97-3544-4a41-21be-167e25b61b6f, Type EFI_BASIC_DATA
para:                Offset 0x0000000004108000, Length 0x0000000000080000, Flags 0x00000000, UUID 1cb143a8-b1a8-4b57-51b2-945c5119e8fe, Type EFI_BASIC_DATA
expdb:               Offset 0x0000000004188000, Length 0x0000000001400000, Flags 0x00000000, UUID 3b9e343b-cdc8-4d7f-a69f-b6812e50ab62, Type EFI_BASIC_DATA
gsort:               Offset 0x0000000005588000, Length 0x0000000001000000, Flags 0x00000000, UUID 5f6a2c79-6617-4b85-02ac-c2975a14d2d7, Type EFI_BASIC_DATA
ffu:                 Offset 0x0000000006588000, Length 0x0000000000800000, Flags 0x00000000, UUID 4ae2050b-5db5-4ff7-d3aa-5730534be63d, Type EFI_BASIC_DATA
cust:                Offset 0x0000000006d88000, Length 0x0000000034000000, Flags 0x00000000, UUID 1f9b0939-e16b-4bc9-bca5-dc2ee969d801, Type EFI_BASIC_DATA
vbmeta_system:       Offset 0x000000003ad88000, Length 0x0000000000800000, Flags 0x00000000, UUID d722c721-0dee-4cb8-838a-2c63cd1393c7, Type EFI_BASIC_DATA
vbmeta_vendor:       Offset 0x000000003b588000, Length 0x0000000000800000, Flags 0x00000000, UUID e02179a8-ceb5-48a9-3188-4f1c9c5a8695, Type EFI_BASIC_DATA
frp:                 Offset 0x000000003bd88000, Length 0x0000000000100000, Flags 0x00000000, UUID 84b09a81-fad2-41ac-0e89-407c24975e74, Type EFI_BASIC_DATA
nvcfg:               Offset 0x000000003be88000, Length 0x0000000002000000, Flags 0x00000000, UUID e8f0a5ef-8d1b-42ea-2a9c-835cd77de363, Type EFI_BASIC_DATA
nvdata:              Offset 0x000000003de88000, Length 0x0000000004000000, Flags 0x00000000, UUID d5f0e175-a6e1-4db7-c094-f82ad032950b, Type EFI_BASIC_DATA
md_udc:              Offset 0x0000000041e88000, Length 0x000000000169a000, Flags 0x00000000, UUID 1d9056e1-e139-4fca-0b8c-b75fd74d81c6, Type EFI_BASIC_DATA
metadata:            Offset 0x0000000043522000, Length 0x0000000002000000, Flags 0x00000000, UUID 7792210b-b6a8-45d5-91ad-3361ed14c608, Type EFI_BASIC_DATA
protect1:            Offset 0x0000000045522000, Length 0x0000000000800000, Flags 0x00000000, UUID 138a6db9-1032-451d-e991-0fa38ff94fbb, Type EFI_BASIC_DATA
protect2:            Offset 0x0000000045d22000, Length 0x0000000000ade000, Flags 0x00000000, UUID 756d934c-50e3-4c91-46af-02d824169ca7, Type EFI_BASIC_DATA
seccfg:              Offset 0x0000000046800000, Length 0x0000000000800000, Flags 0x00000000, UUID a3f3c267-5521-42dd-24a7-3bdec20c7c6f, Type EFI_BASIC_DATA
persist:             Offset 0x0000000047000000, Length 0x0000000003000000, Flags 0x00000000, UUID 8c68cd2a-ccc9-4c5d-578b-34ae9b2dd481, Type EFI_BASIC_DATA
sec1:                Offset 0x000000004a000000, Length 0x0000000000200000, Flags 0x00000000, UUID 6a5cebf8-54a7-4b89-1d8d-c5eb140b095b, Type EFI_BASIC_DATA
proinfo:             Offset 0x000000004a200000, Length 0x0000000000300000, Flags 0x00000000, UUID a0d65bf8-e8de-4107-3494-1d318c843d37, Type EFI_BASIC_DATA
efuse:               Offset 0x000000004a500000, Length 0x0000000000080000, Flags 0x00000000, UUID 46f0c0bb-f227-4eb6-2fb8-66408e13e36d, Type EFI_BASIC_DATA
md1img:              Offset 0x000000004a580000, Length 0x0000000006400000, Flags 0x00000000, UUID fbc2c131-6392-4217-1eb5-548a6edb03d0, Type EFI_BASIC_DATA
spmfw:               Offset 0x0000000050980000, Length 0x0000000000100000, Flags 0x00000000, UUID e195a981-e285-4734-2580-ec323e9589d9, Type EFI_BASIC_DATA
scp1:                Offset 0x0000000050a80000, Length 0x0000000000100000, Flags 0x00000000, UUID e29052f8-5d3a-4e97-b5ad-5f312ce6610a, Type EFI_BASIC_DATA
scp2:                Offset 0x0000000050b80000, Length 0x0000000000100000, Flags 0x00000000, UUID 9c3cabd7-a35d-4b45-578c-b80775426b35, Type EFI_BASIC_DATA
sspm_1:              Offset 0x0000000050c80000, Length 0x0000000000100000, Flags 0x00000000, UUID e7099731-95a6-45a6-e5a1-1b6aba032cf1, Type EFI_BASIC_DATA
sspm_2:              Offset 0x0000000050d80000, Length 0x0000000000100000, Flags 0x00000000, UUID 8273e1ab-846f-4468-99b9-ee2ea8e50a16, Type EFI_BASIC_DATA
gz1:                 Offset 0x0000000050e80000, Length 0x0000000001000000, Flags 0x00000000, UUID d26472f1-9ebc-421d-14ba-311296457c90, Type EFI_BASIC_DATA
gz2:                 Offset 0x0000000051e80000, Length 0x0000000001000000, Flags 0x00000000, UUID b72ccbe9-2055-46f4-67a1-4a069c201738, Type EFI_BASIC_DATA
nvram:               Offset 0x0000000052e80000, Length 0x0000000004000000, Flags 0x00000000, UUID 9c1520f3-c2c5-4b89-4282-fe4c61208a9e, Type EFI_BASIC_DATA
lk:                  Offset 0x0000000056e80000, Length 0x0000000000200000, Flags 0x00000000, UUID 902d5f3f-434a-4de7-8889-321e88c9b8aa, Type EFI_BASIC_DATA
lk2:                 Offset 0x0000000057080000, Length 0x0000000000200000, Flags 0x00000000, UUID bece74c8-d8e2-4863-fe9b-5b0b66bb920f, Type EFI_BASIC_DATA
boot:                Offset 0x0000000057280000, Length 0x0000000004000000, Flags 0x00000000, UUID ff1342cf-b7be-44d5-5ea2-a435addd2702, Type EFI_BASIC_DATA
logo:                Offset 0x000000005b280000, Length 0x0000000000800000, Flags 0x00000000, UUID a4da8f1b-fe07-433b-cb95-84a5f23e477b, Type EFI_BASIC_DATA
dtbo:                Offset 0x000000005ba80000, Length 0x0000000000800000, Flags 0x00000000, UUID c2635e15-61aa-454e-409c-ebe1bdf19b9b, Type EFI_BASIC_DATA
tee1:                Offset 0x000000005c280000, Length 0x0000000000500000, Flags 0x00000000, UUID 4d2d1290-36a3-4f5d-b4af-319f8ab6dcd8, Type EFI_BASIC_DATA
tee2:                Offset 0x000000005c780000, Length 0x0000000000880000, Flags 0x00000000, UUID fdce12f0-a7eb-40f7-5083-960972e6cb57, Type EFI_BASIC_DATA
super:               Offset 0x000000005d000000, Length 0x0000000120000000, Flags 0x00000000, UUID 0fbbafa2-4aa9-4490-8389-5329328505fd, Type EFI_BASIC_DATA
vbmeta:              Offset 0x000000017d000000, Length 0x0000000000800000, Flags 0x00000000, UUID a76e4b2f-31cb-40ba-6a82-c0cb0b73c856, Type EFI_BASIC_DATA
cache:               Offset 0x000000017d800000, Length 0x000000001b000000, Flags 0x00000000, UUID f54ac030-7004-4d02-8194-bbf982036807, Type EFI_BASIC_DATA
userdata:            Offset 0x0000000198800000, Length 0x00000005ab8fbe00, Flags 0x00000000, UUID c4c310e2-4a7e-77d3-1848-61e2d8bb5e86, Type EFI_BASIC_DATA
otp:                 Offset 0x00000007440fbe00, Length 0x0000000002b00000, Flags 0x00000000, UUID 3734710f-0f13-1ab9-4c73-12a08ec50837, Type EFI_BASIC_DATA
flashinfo:           Offset 0x0000000746bfbe00, Length 0x0000000001000000, Flags 0x00000000, UUID 85a5b02f-3773-18b3-4910-718cde95107e, Type EFI_BASIC_DATA

Total disk size:0x0000000747c00000, sectors:0x0000000003a3e000
```
