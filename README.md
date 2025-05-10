# VFIO Script
### Development | v0.0.1
Easily automate the install or uninstall of a hardware-passthrough (VFIO) setup
on a Linux machine. Select from either a dynamic, GRUB, or static setup.

#### View this repository on [Codeberg][01] or [GitHub][02].
[01]: https://codeberg.org/portellam/vfio-script
[02]: https://github.com/portellam/vfio-script
##

## Table of Contents
- [1. Why?](#1-why)
- [2. Related Projects](#2-related-projects)
- [3. Documentation](#3-documentation)
- [4. Requirements](#4-requirements)
  - [4.1. Software](#41-software)
  - [4.2. Hardware](#42-hardware)
- [5. Download](#4-download)
- [6. Usage](#6-usage)
  - [6.1. Install](#61-install)
  - [6.2. Executable](#62-executable)
  - [6.3. VFIO Setups](#63-vfio-setups)
- [7. Contact](#7-contact)
- [8. Contact](#8-disclaimer)
- [9. References](#9-references)

## Contents
### 1. Why?
Do you like *repeatedly* editing configuration files?

No? Then you're going **sane**.

### 2. Related Projects
To view other relevant projects, visit [Codeberg][21]
or [GitHub][22].

[21]: https://codeberg.org/portellam/vfio-collection
[22]: https://github.com/portellam/vfio-collection

### 3. Documentation
- What is VFIO?[<sup>[3]</sup>](#3)
- VFIO Discussion and Support[<sup>[4]</sup>](#4)
- Hardware-Passthrough Guide[<sup>[2]</sup>](#2)
- Virtual Machine XML Format Guide[<sup>[5]</sup>](#5)

### 4. Requirements
#### 4.1. Software
1. [`parse-iommu-devices`](#1) to reliably parse hardware devices.
2. **GRUB** to enable firmware options and (optionally) define a VFIO setup.
3. **Linux** as the host operating system and terminal interface/command line.

  | Linux Distributions  | Tested | Supported  |
  | :------------------- | :----: | :--------: |
  | Arch                 | No     | N/A        |
  | Debian               | Yes    | 12         |
  | Gentoo               | No     | N/A        |
  | Red Hat Enterprise   | No     | N/A        |
  | SUSE                 | No     | N/A        |

#### 4.2. Hardware
The following firmware options are supported and enabled (motherboard and CPU):
- **IOMMU**
    - For **AMD** machines:&nbsp;`AMD-Vi`
    - For **Intel** machines:&ensp;&nbsp;`VT-d`
    - **ARM** (`SMMU`) and other CPU architectures are not **explicitly**
    supported by `vfio-script`. *Use at your own risk.*

### 5. Download
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

### 6. Usage
#### 6.1. Install
Installer will copy the script file to `/usr/local/bin/`, and source files to
`/usr/local/bin/vfio-script.d/`.

```bash
sudo bash installer.sh
```

#### 6.2. Executable
- From anywhere, execute: `vfio-script`

```
  -h, --help     Print this help and exit.
  -v, --verbose  Show more output.
  -U, --uninstall          Uninstalls persistent VFIO setups.

  Multiple GRUB VFIO setup arguments:

  -M|--multiple-grub NUMS  Define one or more persistent VFIO setup(s) as GRUB
                           command line permutations; setup(s) are defined as
                           individual GRUB boot menu entries, where one
                           permutation may be chosen at Host machine startup.
                           Note: multiple GPUs on separate IOMMU groups will
                           create multiple permutations.

                           NUMS is a comma delimited list of positive numbers
                           representing selected kernel(s); multiply the
                           permutations by the number of available kernel(s) to
                           be used (sorted newest to oldest).
                           Note: to use all available, input '0'.

    ptions:

    --exclude-drivers DRIVERS       Specify which devices' drivers to not override
                                    with a VFIO driver, if not defined within
                                    "--drivers".

                                    DRIVERS is a comma delimited list of text.

    --exclude--iommu-groups GROUPS  Specify which IOMMU groups may be reserved for
                                    the Host machine, if not defined within
                                    "--iommu-groups".

                                    GROUPS is a comma delimited list of positive
                                    numbers.

  Other VFIO setup arguments:

  -D, --dynamic            Define a temporary VFIO setup as a QEMU command line.
                           Append to a Libvirt hook or a Guest machine
                           configuration file. This VFIO setup may be
                           created/destroyed on a Guest startup/shutdown.

  -S|--static OPT          Define a persistent VFIO setup.
                           OPT is an option.

  --static grub            Write to GRUB.
  --static conf            Write various configuration files.

  -g|--iommu-groups GROUPS  Specify which IOMMU groups may be reserved for any
                            Guest machine.

                            GROUPS is a comma delimited list of text.

  -d|--drivers DRIVERS      Specify which devices' drivers to override with the
                            "vfio-pci" driver.

                            DRIVERS is a comma delimited list of text.

  -h|--hardware-ids HWIDS   Specify which devices' IDs to blacklist.

                            HWIDS is a comma delimited list of text.


  Additional arguments:



  --exclude-drivers DRIVERS   Specify which devices' drivers to not override
                              with a VFIO driver, if not defined within
                              "--drivers".

                              DRIVERS is a comma delimited list of text.


  -u, --allow-unsafe          Override safety limits. Override a maximum amount of
                              permutations, and/or features which may repeat a given
                              command many times.
                              Note: safety limits are five (5) units each.
                              Note: no prompt at execution.

  -c, --grub-cmdline TEXT     Define the GRUB command line.
                              Note: avoid escape characters, such as double-quote (")
                              and/or VFIO commands so as to prevent conflicts.

                              TEXT is whitespace delimited text.



Examples:
      --multiple-grub 3   Define a multiple of GRUB boot menu entries (as
                          individual VFIO setups), multiplied by the three (3)
                          kernels.
```

#### 6.3. VFIO setups
- **Dynamic**
  - Define a temporary VFIO setup as a QEMU command line.
  - Append to a Libvirt hook or a Guest machine configuration file.
  - This VFIO setup may be created/destroyed on a Guest startup/shutdown.

- **Multiple GRUB**
  - Define one or more persistent VFIO setup(s) as GRUB command line
  permutations, where one permutation may be chosen at Host machine startup.
  - **Formulae:**
    - &ensp;**Given**&ensp; \( \text{groups}_{\text{guest video}} = \text{groups}_{\text{total video}} - \text{groups}_{\text{host video}} \)
      - &ensp;**If**&ensp; \( \text{groups}_{\text{guest video}} \geq 1 \)
        - &ensp;**Given**&ensp; \( \text{groups}_{\text{host video}} \geq 1 \)
        - &ensp;**Then**&ensp; \( \text{permutations}_{\text{total}} = \text{kernels} \times \text{groups}_{\text{guest video}} \)

      - &ensp;**If**&ensp; \( \text{groups}_{\text{guest video}} = 0 \)
        - **Given**&ensp; \( \text{groups}_{\text{total guest}} \geq 1 \)
        - &ensp;**Then**&ensp; \( \text{permutations}_{\text{total}} = \text{kernels} \)

  - Modifies the following files:
    - creates `/etc/grub.d/40_custom` to define the multiple boot menu entries.
    - **overwrites** `/etc/default/grub` to define the default boot menu entry.

- **Static**
  - Define a persistent VFIO setup.

  - Modifies either of the following files:
    - GRUB: `/etc/default/grub`.

    - system configuration files:
      - **overwrites** `/etc/initramfs-tools/modules`.
      - creates `/etc/modprobe.d/pci-blacklists.conf`.
      - creates `/etc/modprobe.d/vfio.conf`.
      - **overwrites** `/etc/modules`.

### 7. Contact
Did you encounter a bug? Do you need help? Please visit the [Issues][71] page.

[71]: https://github.com/portellam/vfio-script/issues

### 8. Disclaimer
Use at your own risk. Please review your system's specifications and resources.

### 9. References
#### 1.
&nbsp;&nbsp;**parse-iommu-devices**. Codeberg. Accessed May 7, 2025.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://codeberg.org/portellam/parse-iommu-devices.</sup>

&nbsp;&nbsp;**parse-iommu-devices**. GitHub. Accessed May 7, 2025.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://github.com/portellam/parse-iommu-devices.</sup>

#### 2.
&nbsp;&nbsp;**PCI passthrough via OVMF**. ArchWiki. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF.</sup>

#### 3.
&nbsp;&nbsp;**VFIO - ‘Virtual Function I/O’ - The Linux Kernel Documentation**.
The linux kernel. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://www.kernel.org/doc/html/latest/driver-api/vfio.html.</sup>

#### 4.
&nbsp;&nbsp;**VFIO Discussion and Support**. Reddit. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://www.reddit.com/r/VFIO/.</sup>

#### 5.
&nbsp;&nbsp;**XML Design Format** GitHub - libvirt/libvirt. Accessed June 18, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://github.com/libvirt/libvirt/blob/master/docs/formatdomain.rst.</sup>

#### Click [here](#vfio-script) to return to the top of this document.