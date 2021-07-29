<h1>Android</h1>

[TOC]


# Debug

## adb

### Issue: no permission

When i try:

```bash
adb devices
```

i get the result:

```bash
List of devices attached 
????????????    no permissions
```

Then I tried to restart the Adb server

```bash
sudo adb kill-server
```

and then

```bash
sudo adb start-server
```

then connected the device, turn Debugging on and type

```bash
adb devices
```

Still any issue? then follow [this](https://askubuntu.com/questions/908306/adb-no-permissions-on-ubuntu-17-04)


## Root

### Magisk

Source:
    - https://www.didgeridoohan.com/magisk

- if failing to flash .zip (due to signature verification) --> uncheck sign verification before flash
