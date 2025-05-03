# VFIO Script
### Development
Easily install, uninstall, or reinstall a VFIO setup on a Linux machine. Choose
between a dynamic, GRUB, or static setup.

#### View this repository on [Codeberg][01] or [GitHub][02].
[01]: https://codeberg.org/portellam/vfio-script
[02]: https://github.com/portellam/vfio-script
##

## Table of Contents
- [1. Why?](#1-why)
- [2. Related Projects](#2-related-projects)
- [3. Documentation](#3-documentation)
- [4. Download](#4-download)
- [5. Usage](#5-usage)
- [6. Contact](#6-contact)
- [7. References](#7-references)

## Contents
### 1. Why?
Do you like getting dirty in Linux? Writing and updating configuration files?
Repetitive steps are more enjoyable than the outcome?

No? Then you're going **sane**.

### 2. Related Projects
To view other relevant projects, visit [Codeberg][21]
or [GitHub][22].

[11]: https://codeberg.org/portellam/vfio-collection
[12]: https://github.com/portellam/vfio-collection

### 3. Documentation
- What is VFIO?[<sup>[2]</sup>](#2)
- VFIO Discussion and Support[<sup>[3]</sup>](#3)
- Hardware-Passthrough Guide[<sup>[1]</sup>](#1)
- Virtual Machine XML Format Guide[<sup>[4]</sup>](#4)

### 4. Download
- Download the Latest Release:&ensp;[Codeberg][41] or [GitHub][42].

- Download the `.zip` file:
    1. Viewing from the top of the repository's (current) webpage, click the
        drop-down icon:
        - `···` on Codeberg.
        - `<> Code ` on GitHub.
    2. Click `Download ZIP` and save.
    3. Open the `.zip` file, then extract its contents.

- Clone the repository:
    1. Open a Command Line Interface (CLI) or Terminal.
        - Open a console emulator (for Debian systems: Konsole).
        - **Linux only:** Open an existing console: press `CTRL` + `ALT` + `F2`,
        `F3`, `F4`, `F5`, or `F6`.
            - **To return to the desktop,** press `CTRL` + `ALT` + `F7`.
            - `F1` is reserved for debug output of the Linux kernel.
            - `F7` is reserved for video output of the desktop environment.
            - `F8` and above are unused.
    2. Change your directory to your home folder or anywhere safe:
        - `cd ~`
    3. Clone the repository:
        - `git clone https://www.codeberg.org/portellam/vfio-script`
        - `git clone https://www.github.com/portellam/vfio-script`

[41]: https://codeberg.org/portellam/vfio-script/releases/latest
[42]: https://github.com/portellam/vfio-script/releases/latest

### 5. Usage
#### 5.1. Install
Installer will copy the script file to `/usr/local/bin/`, and source files to
`/usr/local/bin/vfio-script.d/`.

```bash
sudo bash installer.sh
```

#### 5.2. Executable
- From anywhere, execute: `vfio-setup`

```
  -h, --help                Print this help and exit.
  -v, --verbose             Show more output.

  -d, --drivers=DRIVERS     Specify what device drivers to use the "vfio-pci"
                            driver.
                            Note: You may avoid this option to allow a specified
                            VFIO setup to determine what devices to blacklist or
                            not.
                            DRIVERS is a comma delimited list of text.

  -h, --hardware-ids=HWIDS  Specify what device IDs to blacklist.
                            Note: You may avoid this option to allow a specified
                            VFIO setup to determine what devices to blacklist or
                            not.
                            HWIDS is a comma delimited list of text.

  --pci-stub=HWIDS          Specify what device IDs to blacklist and device
                            drivers to use the "pci-stub" driver.
                            HWIDS is a comma delimited list of text.

  -D, --dynamic             Define a temporary VFIO setup as a QEMU command
                            line or Libvirt hook. May be created/destroyed on a
                            specific Guest machine startup/shutdown.

  -G, --grub=NUMS           Define one or more VFIO setup(s) as command line(s);
                            setup(s) are defined as GRUB boot menu entries,
                            where one may be chosen at Host startup.
                            Note: multiple GPUs on separate IOMMU groups will
                            create multiple VFIO setups.
                            NUMS is a comma delimited list of positive non-zero
                            numbers, which represent the number of kernel(s) to
                            use per VFIO setup (latest to oldest).
                            Note: To use all, leave blank.

  -S, --static              Define a persistent VFIO setup via writing to
                            various configuration files.
```

### 6. Contact
Did you encounter a bug? Do you need help? Please visit the
**Issues page** ([Codeberg][41], [GitHub][42]).

[41]: https://codeberg.org/portellam/vfio-script/issues
[42]: https://github.com/portellam/vfio-script/issues

### 7. References
#### 1.
&nbsp;&nbsp;**PCI passthrough via OVMF**. ArchWiki. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF.</sup>

#### 2.
&nbsp;&nbsp;**VFIO - ‘Virtual Function I/O’ - The Linux Kernel Documentation**.
The linux kernel. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://www.kernel.org/doc/html/latest/driver-api/vfio.html.</sup>

#### 3.
&nbsp;&nbsp;**VFIO Discussion and Support**. Reddit. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://www.reddit.com/r/VFIO/.</sup>

#### 4.
&nbsp;&nbsp;**XML Design Format** GitHub - libvirt/libvirt. Accessed June 18, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://github.com/libvirt/libvirt/blob/master/docs/formatdomain.rst.</sup>

#### Click [here](#vfio-script) to return to the top of this document.