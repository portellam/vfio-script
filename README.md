# VFIO Script
### Pre-Development
Install and uninstall a VFIO setup on a Linux machine. Choose between a dynamic, GRUB, or static setup. 

## Table of Contents
- [1. Related Projects](#1-related-projects)
- [2. Documentation](#2-documentation)
- [3. Contact](#3-contact)
- [4. References](#4-references)
- [5. Planned Features](#5-planned-features)

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

### 3. Contact
Did you encounter a bug? Do you need help? Please visit the
**Issues page** ([Codeberg][31], [GitHub][32]).

[31]: https://codeberg.org/portellam/vfio-script/issues
[32]: https://github.com/portellam/vfio-script/issues

### 4. References
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