
## macOS Guest

`quickget` automatically downloads a macOS recovery image and creates a virtual
machine configuration.

```bash
quickget macos catalina
quickemu --vm macos-catalina.conf
```

macOS `high-sierra`, `mojave`, `catalina`, `big-sur` and `monterey` are supported.

* Use cursor keys and enter key to select the **macOS Base System**
* From **macOS Utilities**
  * Click **Disk Utility** and **Continue**
    * On macOS Catalina, Big Sur & Monterey
      * Select `Apple Inc. VirtIO Block Media` from the list and click **Erase**.
    * On macOS Mojave and High Sierra
      * Select `QEMU HARDDISK Media` (~103.08GB) from the list and click **Erase**.
  *   Enter a `Name:` for the disk
      * If your installing macOS Mojave or later (Catalina, Big Sur,
        and Monterey), choose any of the APFS options as the filesystem.
        MacOS Extended may not work.
  *   Click **Erase**.
  * Click **Done**.
  * Close Disk Utility
* From **macOS Utilities**
  * Click **Reinstall macOS** and **Continue**
* Complete the installation as you normally would.
  * On the first reboot use cursor keys and enter key to select **macOS Installer**
  * On the subsequent reboots use cursor keys and enter key to select the disk you named

The default macOS configuration looks like this:

```bash
guest_os="macos"
img="macos-catalina/RecoveryImage.img"
disk_img="macos-catalina/disk.qcow2"
macos_release="catalina"
```

* `guest_os="macos"` instructs Quickemu to optimise for macOS.
* `macos_release="catalina"` instructs Quickemu to optimise for a particular macOS release.
  * For example VirtIO Network and Memory Ballooning are available in Big Sur and newer, but not previous releases.
  * And VirtIO Block Media (disks) are supported/stable in Catalina and newer.

### macOS compatibility

There are some considerations when running macOS via Quickemu.

* Supported macOS releases:
  * High Sierra
  * Mojave
  * Catalina **(Recommended)**
  * Big Sur
  * Monterey
* `quickemu` will automatically download the required [OpenCore](https://github.com/acidanthera/OpenCorePkg)
  bootloader and OVMF firmware from [OSX-KVM](https://github.com/kholia/OSX-KVM).
* Optimised by default, but no GPU acceleration is available.
  * Host CPU vendor is detected and guest CPU is optimised accordingly.
  * [VirtIO Block Media](https://www.kraxel.org/blog/2019/06/macos-qemu-guest/) is used for the system disk where supported.
  * [VirtIO `usb-tablet`](http://philjordan.eu/osx-virt/) is used for the mouse.
  * VirtIO Network (`virtio-net`) is supported and enabled on macOS Big Sur and newer but previous releases use `vmxnet3`.
  * VirtIO Memory Ballooning is supported and enabled on macOS Big Sur and newer but disabled for other support macOS releases.
* USB host and SPICE pass-through is:
  * UHCI (USB 2.0) on macOS Catalina and earlier.
  * XHCI (USB 3.0) on macOS Big Sur and newer.
* Display resolution can only be changed via macOS System Preferences.
*   **Full Duplex audio requires [VoodooHDA OC](https://github.com/chris1111/VoodooHDA-OC) or pass-through a USB audio-device to the macOS guest VM**.
   * NOTE! [Gatekeeper](https://disable-gatekeeper.github.io/) and [System Integrity Protection (SIP)](https://developer.apple.com/documentation/security/disabling_and_enabling_system_integrity_protection) need to be disabled to install VoodooHDA OC
* File sharing between guest and host is available via [virtio-9p](https://wiki.qemu.org/Documentation/9psetup) and [SPICE webdavd](https://gitlab.gnome.org/GNOME/phodav/-/merge_requests/24).
* Copy/paste via SPICE agent is **not available on macOS**.

### macOS App Store

If you see *"Your device or computer could not be verified"* when you try to
login to the App Store, make sure that your wired ethernet device is `en0`. Use
`ifconfig` in a terminal to verify this.

If the wired ethernet device is not `en0`, then then go to *System Preferences* -> *Network*,
delete all the network devices and apply the changes. Next, open a terminal and
run the following:

```bash
sudo rm /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist
```

Now reboot, and the App Store should work.