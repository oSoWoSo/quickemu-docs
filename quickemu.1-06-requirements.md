
## Requirements

* [QEMU](https://www.qemu.org/) (*6.0.0 or newer*) **with GTK, SDL, SPICE & VirtFS support**
* [bash](https://www.gnu.org/software/bash/) (*4.0 or newer*)
* [Coreutils](https://www.gnu.org/software/coreutils/)
* [EDK II](https://github.com/tianocore/edk2)
* [grep](https://www.gnu.org/software/grep/)
* [jq](https://stedolan.github.io/jq/)
* [LSB](https://wiki.linuxfoundation.org/lsb/start)
* [procps](https://gitlab.com/procps-ng/procps)
* [python3](https://www.python.org/)
* [macrecovery](https://github.com/acidanthera/OpenCorePkg/tree/master/Utilities/macrecovery)
* [mkisofs](http://cdrtools.sourceforge.net/private/cdrecord.html)
* [usbutils](https://github.com/gregkh/usbutils)
* [util-linux](https://github.com/karelzak/util-linux)
* [sed](https://www.gnu.org/software/sed/)
* [socat](http://www.dest-unreach.org/socat/)
* [spicy](https://gitlab.freedesktop.org/spice/spice-gtk)
* [swtpm](https://github.com/stefanberger/swtpm)
* [Wget](https://www.gnu.org/software/wget/)
* [xdg-user-dirs](https://www.freedesktop.org/wiki/Software/xdg-user-dirs/)
* [xrandr](https://gitlab.freedesktop.org/xorg/app/xrandr)
* [zsync](http://zsync.moria.org.uk/)
* [unzip](http://www.info-zip.org/UnZip.html)

### Installing Requirements

For Ubuntu, Arch and nixos systems the [ppa](https://launchpad.net/~flexiondotorg/+archive/ubuntu/quickemu), [AUR](https://aur.archlinux.org/packages/quickemu) or [nix](https://github.com/NixOS/nixpkgs/tree/master/pkgs/development/quickemu) packaging will take care of the dependencies. For other host distributions or operating systems it will be
necessary to install the above requirements or their equivalents.

These examples may save a little typing

Debian (and direct derivatives such as MX Linux):

```
sudo apt install qemu bash coreutils ovmf grep jq lsb-base procps python3 genisoimage usbutils util-linux sed spice-client-gtk libtss2-tcti-swtpm0 wget xdg-user-dirs zsync unzip
```

Fedora:

```
sudo dnf install qemu bash coreutils edk2-tools grep jq lsb procps python3 genisoimage usbutils util-linux sed spice-gtk-tools swtpm wget xdg-user-dirs xrandr unzip
```

MacOS:

This is a work in progress (see [issue 248](https://github.com/quickemu-project/quickemu/issues/248) for other steps and changes that may enable running on MacOS)
```
brew install qemu bash coreutils grep jq python@3.10 cdrtools gnu-sed spice-gtk wget zsync
```
