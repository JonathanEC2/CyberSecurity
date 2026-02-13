
# The Boot Up Process 

Cisco routers and switches have 4 built-in memory locations

- ROM - Read Only Memory
- Flash - newer devices use removable CompactFlash
- NVRAM - Non-Volatile RAM
- RAM - Random Access Memory

## ROM

When the device is powered on, it will first load from ROM. Two main functions are performed:
- Power On Self Test
- Load bootstrap

The bootstrap will look in flash for an IOS software image to load

Device has failed to boot if you see a prompt that say ROMMON. ROM Monitor can be used to recover a missing or corrupted software image. In this case you can boot from USB or an external TFTP server

## Flash Memory

Will load the first IOS image found in flash by default; you can override this with the `boot system` command

## NVRAM

- Next, system will load the startup-config configuration file from NVRAM. The saved startup-config becomes the current running-config in RAM
- Whenever you enter a command in IOS it takes effect immediately and goes into your running config. To make changes permanent across reboot:

`copy run start`

## RAM

- IOS system image and startup config are are loaded from flash and NVM ram into RAM during bootup
- RAM is used as the normal working memory of the device
- RAM is volatile

# Factory Reset and Password Recovery

## Factory Reset 

`write erase` will erase the startup-config. Reload to boot up with a blank configuration.

## Config Register

The configuration register can be used to change the way the router boots. Use the `config-register` command in global configuration mode or `confreg` at the rommon prompt.

0x2102 boot normally
0x2120 boot into rommon mode
0x2142 ignore contents of startup config

## Router Password Recovery Procedure

- Load into rommon
- Enter `confreg 0x2142`
- `restart`
- `enable`
- `copy start run`
- change enable secret using `enable secret {secret}`
- enter `config-register 0x2102`
- `copy run start`
- `reload`

Google instructions

# Backing up the System Image and Config

- You can copy IOS system images and configurations to Flash, FTP, TFTP or USB
- If you copy a config file into the running-config, it will be merged with the current configuration
- To replace a config, factory reset and then copy the new config into the startup config

```IOS
copy flash tftp
copy running-config tftp
copy start-up config usb
```

`wr erase` erases nvram files

# Upgrading the IOS System Image

- software.cisco.com
- After downloading the software, copy to the devices Flash using TFTP: `copy tftp flash`
- Delete the old system image or use the `boot system {source}:{filename} ` command