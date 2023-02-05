# pikvm-usb-atx-ctrl

Enables PiKVM to control ATX operations of multiple computers via USB.

![screenshot](/images/kvm-atx-menu.png)


## HOWTO

What you need:
* Your favorite PiKVM setup
* RP2040-Zero (RP2040-Pico should work, too)
* DLN-2 device drivers as part of your distribution or from here: https://github.com/zappanaut/dln2-dkms
* The [USB-ATX-CTRL PCB](https://github.com/zappanaut/usb-atx-ctrl) or a breadboard


### Setting up the DLN-2 device driver

The PiKVM image is lacking the DLN2 device drivers. To install these you can follow the instructions from the [dln2-dkms](https://github.com/zappanaut/dln2-dkms) repository.

It is important that the [udev rule files](https://github.com/zappanaut/dln2-dkms/tree/main/udev) are also installed and the directory `/dev/gpio-by-serial` exists. This also applies to distributions that already come with the DLN2 drivers!
Each board has a (hopefully) unique serial number, that is used by a udev rule to create a symlink to the actual device in `/dev/gpio-by-serial/`. This way the boards can be referenced independently from the kernel's enumeration.


### Flashing the RP2040

The firmware sources can be found in the [pico-usb-io-board](https://github.com/zappanaut/pico-usb-io-board) repository. Make sure you are using the [usb-atx-ctrl branch](https://github.com/zappanaut/pico-usb-io-board/tree/usb-atx-ctrl)!
Or simply use the firmware image `firmware/dln2.uf2` from this repository.


### Building the USB-ATX-CTRL Board

There is yet another [repository with KiCAD and Gerber files](https://github.com/zappanaut/usb-atx-ctrl) for a PCB, that can be attached to a slot bracket.

It is also possible to build this on a breadboard. You may want to have a look at the [PiKVM documentation](https://github.com/pikvm/pikvm)  and in particular the "ATX control board". The schematics are very similar.


### Setting up PiKVM

There are no special requirements regarding the PiKVM installation itself. This setup is using only mechanisms that are already in place.

Use the `kvmd/override.yml` and `kvmd/web.css` as a starting point and copy them to the `/etc/kvmd/` directory after editing.
In particular replace `[RP2040-serial]` in `override.yml` with the serial numbers of your boards.


## Future development

The board's I/O capabilities can be used for many kinds of telemetry like e.g. monitoring the temperature and voltages...


## Disclaimer

Even though this setup is working for me, your mileage may vary...


