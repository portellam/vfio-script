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
Do you like editing configuration files? Repeatedly?

No? Then you're going **sane**.

### 2. Related Projects
To view other relevant projects, visit [Codeberg][21]
or [GitHub][22].

[21]: https://codeberg.org/portellam/vfio-collection
[22]: https://github.com/portellam/vfio-collection

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
- From anywhere, execute: `vfio-script`

```
  -h, --help                Print this help and exit.
  -v, --verbose             Show more output.

  -D, --dynamic             Define a temporary VFIO setup as a QEMU command
                            line. Append to a Libvirt hook or a Guest machine
                            configuration file. VFIO setup may be
                            created/destroyed on a Guest startup/shutdown.

  -G, --grub=NUMS           Define one or more VFIO setup(s) as command line(s);
                            setup(s) are defined as GRUB boot menu entries,
                            where one may be chosen at Host machine startup.
                            Note: multiple GPUs on separate IOMMU groups will
                            create multiple VFIO setups.
                            NUMS is a comma delimited list of positive non-zero
                            numbers, which represent the number of kernel(s) to
                            use per VFIO setup (sorted by newest to oldest).
                            Note: to use all available, leave blank.

  -S, --static              Define a persistent VFIO setup by writing to
                            various configuration files.

  --override                Override limits for features which may repeat a
                            given command many times (limit is five (5)
                            repetitions).
                            Note: "--grub=9" may use nine (9) or less kernels,
                            default is five (5) or less kernels.

  Note: the following options may be avoided to allow a given VFIO setup to
  determine which devices to use or not.

  -g, --groups=GROUPS       Specify which IOMMU groups may be reserved for any
                            Guest machine.
                            GROUPS is a comma delimited list of text.

  -d, --drivers=DRIVERS     Specify which devices' drivers to override with the
                            "vfio-pci" driver.
                            DRIVERS is a comma delimited list of text.

  -h, --ids=HWIDS           Specify which devices' IDs to blacklist.
                            HWIDS is a comma delimited list of text.

  --pci-stub-ids=HWIDS      Specify which devices' IDs to blacklist and drivers
                            to override with the "pci-stub" driver.
                            HWIDS is a comma delimited list of text.

  --exclude--groups=GROUPS    Specify which IOMMU groups drivers may be reserved
                              for the Host machine, if not defined within
                              "--groups".
                              GROUPS is a comma delimited list of positive
                              numbers.

  --exclude-drivers=DRIVERS   Specify which devices' drivers to not override
                              with a VFIO driver, if not defined within
                              "--drivers".
                              DRIVERS is a comma delimited list of text.

  --exclude-ids=HWIDS         Specify which devices' IDs to whitelist, if not
                              defined within "--ids" or "--pci-stub-ids".
                              HWIDS is a comma delimited list of text.
```

#### TODO:
- [ ] add exclusion arguments (drivers, hardware IDs, to ignore).
- [ ] add logic to define a safe maximum (and arguments to override) for the following:
  - number of linux kernels to use for GRUB menu entries (example: five kernels)
  - number of multiple VFIO setups for GRUB (ex: five IOMMU groups with GPUs),
  should execution of either `lspci` or `parse-iommu-devices` cause slow down.
- [ ] disclose and utilize `parse-iommu-devices` for all features.
- [ ] add logic to use `lspci` should `parse-iommu-devices` not be present.
- [ ] disclose that for a dynamic setup, the output is partial. It is up to the
user use this output to define guest machine QEMU command lines.
- [ ] avoid global parameters and pass standard input to functions as input
parameters.
- [ ] enable/disable features given arguments
  - defined preferred drivers/hardware IDs will disable GRUB setup.
- [ ] warn user if a setup leaves fewer than one GPU for the Host machine.



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