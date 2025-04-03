# VFIO Script
### Pre-Development
Install and uninstall a VFIO setup on a Linux machine. Choose between a dynamic, GRUB, or static setup. 

#### View this repository on [Codeberg][01] or [GitHub][02].
[01]: https://codeberg.org/portellam/vfio-script
[02]: https://github.com/portellam/vfio-script
##

## Table of Contents
- [1. Related Projects](#1-related-projects)
- [2. Documentation](#2-documentation)
- [3. Download](#3-download)
- [4. Contact](#4-contact)
- [5. References](#5-references)
- [6. Planned Features](#6-planned-features)

## Contents
### 1. Related Projects
To view other relevant projects, visit [Codeberg][11]
or [GitHub][12].

[11]: https://codeberg.org/portellam/vfio-collection
[12]: https://github.com/portellam/vfio-collection

### 2. Documentation
- What is VFIO?[<sup>[2]</sup>](#2)
- VFIO Discussion and Support[<sup>[3]</sup>](#3)
- Hardware-Passthrough Guide[<sup>[1]</sup>](#1)
- Virtual Machine XML Format Guide[<sup>[4]</sup>](#4)

### 3. Download
- Download the Latest Release:&ensp;[Codeberg][31] or [GitHub][32].

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

[31]: https://codeberg.org/portellam/vfio-script/releases/latest
[32]: https://github.com/portellam/vfio-script/releases/latest

### 4. Contact
Did you encounter a bug? Do you need help? Please visit the
**Issues page** ([Codeberg][41], [GitHub][42]).

[41]: https://codeberg.org/portellam/vfio-script/issues
[42]: https://github.com/portellam/vfio-script/issues

### 5. References
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

### 5. Planned Features
- Isolate and migrate VFIO setup from [Deploy VFIO](https://github.com/portellam/deploy-VFIO) and place here.
- Implement a dynamic/hooks based VFIO setup.
##

#### Click [here](#vfio-script) to return to the top of this document.