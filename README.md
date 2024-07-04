# Reprogram TEE on Qualcomm devices
Guide to reprogram the TEE on Qualcomm devices to fix lost attestation keys.

## Why?

> [!NOTE]
> If you are here it is because your phone has lost the TEE attestation keys, possibly due to flashing the persist partition of your phone.
>
> If opening [Key Attestation Demo](https://github.com/vvb2060/KeyAttestation) does not give you any error, do **NOT** follow this guide.
>
> This guide will **NOT** provide instructions for passing Strong verdict.

## WARNINGS:

> [!WARNING]
> **- Your data may be lost, so backup your phone data first.**
>
> **- The original keys that your phone may include in the TEE will be lost.**
>
> **- I am not responsible for any other problems that may arise, these instructions are made on a POCO X3 Pro (vayu) with Paranoid Android uvite and work perfectly,they may not work as they should on other phones..**

## Info

> [!NOTE]
> **We won't flash engineering rom, instead will use a binary from engineering rom to write the keybox**

## You will need:

- A working brain.
- A working computer.
- An unlocked bootloader.
- BASIC KNOWLEDGE OF LINUX.
- A valid keybox.xml file, you can use this one in the repo.
- Downloaded engineering rom for your device.
- Rooted device.

## Instructions:

1. Extract /vendor/bin/KmInstallKeybox from engineering rom.
2. Phone must be connected to PC, then execute this commands IN ORDER:

```
adb shell mkdir -p /data/local/tmp
```
```
adb push KmInstallKeybox /data/local/tmp
```
```
adb shell chmod 777 /data/local/tmp/KmInstallKeybox
```
```
adb push keybox.xml /data/local/tmp
```
```
adb shell su -c /data/local/tmp/KmInstallKeybox /data/local/tmp/keybox.xml 0 true
```

If you are using different keybox, you must change few arguments:
> adb shell /data/local/tmp/KmInstallKeybox /patch/to/your/{KEYBOX FILE} {DEVICE ID} {ATTEST PROPS?}

Attest props must be true unless it gives some error.

> [!NOTE]
> It is not necessary to put keybox.xml exactly in /data/nativetest64/qti_keymaster_tests.
>
> If you get ```KeyMaster Attestation Key Provisioning success for KeyIDx``` and after that ```Segmentation fault``` while applying keybox, ignore it, key applied, so enjoy life.