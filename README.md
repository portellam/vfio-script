# VFIO Script
### Development | v0.0.1
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
  -h, --help     Print this help and exit.
  -v, --verbose  Show more output.

  VFIO setups:

  -D, --dynamic            Define a temporary VFIO setup as a QEMU command line.
                           Append to a Libvirt hook or a Guest machine
                           configuration file. VFIO setup may be
                           created/destroyed on a Guest startup/shutdown.

  -M|--multiple-grub NUMS  Define one or more VFIO setup(s) as command line
                           permutations; setup(s) are defined as individual
                           GRUB boot menu entries, where one permutation may be
                           chosen at Host machine startup.
                           Note: multiple GPUs on separate IOMMU groups will
                           create multiple permutations.

                           NUMS is a comma delimited list of positive numbers
                           representing selected kernel(s); multiply the
                           permutations by the number of available kernel(s) to
                           use (sorted newest to oldest).
                           Note: to use all available, input '0'.

  -S|--static OPT          Define a persistent VFIO setup.
                           OPT is an option.

  --static grub            Write to GRUB.
  --static conf            Write various configuration files.

  Additional arguments:

  --allow-unsafe       Override safety limits. Override a maximum amount of
                       permutations, and/or features which may repeat a given
                       command many times.
                       Note: safety limits are five (5) units each.
                       Note: no prompt at execution.


  --grub-cmdline TEXT  Define the GRUB command line.
                       Note: avoid escape characters (") and/or VFIO
                       commands so as to prevent conflicts.

                       TEXT is whitespace delimited text.

  Guest-machine-reserved devices to match:

  -g|--iommu-groups GROUPS  Specify which IOMMU groups may be reserved for any
                            Guest machine.

                            GROUPS is a comma delimited list of text.

  -d|--drivers DRIVERS      Specify which devices' drivers to override with the
                            "vfio-pci" driver.

                            DRIVERS is a comma delimited list of text.

  -v|--vfio-pci-ids HWIDS   Specify which devices' IDs to blacklist.

                            HWIDS is a comma delimited list of text.

  -p|--pci-stub-ids HWIDS   Specify which devices' IDs to blacklist and drivers
                            to override with the "pci-stub" driver.

                            HWIDS is a comma delimited list of text.

  Host-machine-reserved devices to match:

  --exclude-drivers DRIVERS       Specify which devices' drivers to not override
                                  with a VFIO driver, if not defined within
                                  "--drivers".

                                  DRIVERS is a comma delimited list of text.

  --exclude--iommu-groups GROUPS  Specify which IOMMU groups may be reserved for
                                  the Host machine, if not defined within
                                  "--groups".

                                  GROUPS is a comma delimited list of positive
                                  numbers.


  --exclude-hardware-ids HWIDS    Specify which devices' IDs to whitelist, if not
                                  defined within "--ids" or "--pci-stub-ids".

                                  HWIDS is a comma delimited list of text.
```

#### TODO:
- [ ] sanitize inputs.
- [ ] add logic to undo changes for other setups, if a given one is chosen.
  - in other words, prior to install of a given setup, uninstall the rest.

- [ ] `parse-iommu-devices`: add XML support!
  - in the mean time, warn the user if a VFIO setup is detected, and quit.
  - allow for override.

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
Did you encounter a bug? Do you need help? Please visit the [Issues][61] page.

[61]: https://github.com/portellam/vfio-script/issues

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