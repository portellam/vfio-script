# VFIO Script

### Development | v0.0.1

Easily automate the install or uninstall of a hardware pass-through (VFIO) setup
on a Linux machine. Select from either a dynamic, GRUB, or static setup.

#### View this repository on [Codeberg][01] or [GitHub][02].

[01]: https://codeberg.org/portellam/vfio-script
[02]: https://github.com/portellam/vfio-script
##

## Table of Contents

- [❓ 1. Why?](#-1-why)
- [🛠️ 2. Related Projects](#️-2-related-projects)
- [📝 3. Documentation](#-3-documentation)

- [✅ 4. Host Requirements](-#4-requirements)
  - [4.1. Software](#41-software)
  - [4.2. Hardware](#42-hardware)

- [💾 5. Download](#-4-download)

- [❓ 6. Usage](#6-usage)
  - [6.1. The Command Interface (CLI) or Terminal](#61-the-command-interface-cli-or-terminal)
  - [6.2. Verify Installer is Executable](#62-verify-script-is-executable)
  - [6.3. `installer.bash`](#63-installerbash)
  - [6.4. `vfio-script``](#64-vfioscript)
  - [6.5. VFIO Setups](#65-vfio-setups)

- [⚠️ 7. Disclaimer](#-7-disclaimer)
- [☎️ 8. Contact](#-8-contact)
- [🌐 9. References](#-9-references)

## Contents
### ❓ 1. Why?

Do you like *repeatedly* editing configuration files? No? Then you're going **sane**.

[*Hardware* or *PCI pass-through*](#3-documentation) is a feature in computing,
in which a Host machine can allocate and reserve PCI devices to guests or
Virtual Machines (VMs). This has advantages, most inherent is greater
compatibility over software-emulated devices; *devices do not have to be*
*developed twice.*

[*Virtual function input-output (VFIO)*](#3-documentation) is the framework in
which makes *Hardware pass-through* possible. It exposes direct, secure access to
devices, with the least overhead, and the highest possible performance
(close to or near bare-metal).

**Last and most important,** [*Quick Emulator (QEMU)*<sup>\[1\]</sup>](#1) and
[*Kernel-based Virtual Machine (KVM)*<sup>\[2\]</sup>](#2)
are the implementations which act as emulator and hypervisor, respectively.
*The two are commonly combined to make the colloquial VFIO setup, at least on*
*Linux.*

### 🛠️ 2. Related Projects

To view other relevant projects, visit [Codeberg][21]
or [GitHub][22].

[21]: https://codeberg.org/portellam/vfio-collection
[22]: https://github.com/portellam/vfio-collection

### 📝 3. Documentation

- What is IOMMU? [<sup>\[3\]</sup>](#3)
- What is VFIO? [<sup>\[4\]</sup>](#4)
- VFIO Discussion and Support [<sup>\[5\]</sup>](#5)
- Hardware/PCI Pass-through Guide [<sup>\[6\]</sup>](#6)
- Virtual Machine XML Format Guide [<sup>\[7\]</sup>](#7)

### ✅ 4. Requirements
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

### 💾 5. Download

- Download the Latest Release: [Codeberg][51], [GitHub][52]

- Download the `.zip` file:

  - From the webpage

    1. Viewing from the top of the repository's (current) webpage, click the
       drop-down icon:

       - `···` on Codeberg.
       - `<> Code ` on GitHub.

    2. Click `Download ZIP` and save.
    3. Open the `.zip` file, then extract its contents.

  - From the CLI:

    1. [Open the CLI](#61-the-command-interface-cli-or-terminal).
    2. Download the Latest:

    ```bash
    GH_USER=portellam; \
    GH_REPO=vfio-script; \
    GH_BRANCH=master; \
    wget \
      https://github.com/${GH_USER}/${GH_REPO}/archive/refs/heads/${GH_BRANCH}.zip \
      -O "${GH_REPO}-${GH_BRANCH}.zip" \
    && unzip ./"${GH_REPO}-${GH_BRANCH}.zip" \
    && rm ./"${GH_REPO}-${GH_BRANCH}.zip"
    ```

- Clone the repository:

  1. [Open the CLI](#61-the-command-interface-cli-or-terminal).

  2. Change your directory to your home folder or anywhere safe:
     - `cd ~`

  3. Clone the repository:
     - `git clone https://www.codeberg.org/portellam/vfio-script`
     - `git clone https://www.github.com/portellam/vfio-script`

[31]: https://codeberg.org/portellam/vfio-script/releases/latest
[32]: https://github.com/portellam/vfio-script/releases/latest

### ❓ 6. Usage

#### 6.1. The Command Interface (CLI) or Terminal

To open a CLI or Terminal:

- Open a console emulator (for Debian systems: Konsole).
- **Linux only:** Open an existing console: press `CTRL` + `ALT` + `F2`,
  `F3`, `F4`, `F5`, or `F6`.

  - **To return to the desktop,** press `CTRL` + `ALT` + `F7`.
  - `F1` is reserved for debug output of the Linux kernel.
  - `F7` is reserved for video output of the desktop environment.
  - `F8` and above are unused.

#### 6.2. Verify Installer is Executable

1. Go to the directory where the cloned/extracted repository folder is:
   `cd name_of_parent_folder/acpi-sleep/`

2. Make the installer script file executable: `chmod +x installer.bash`

   - Do **not** make any other script files executable. The installer will
    perform this action.
   - Do **not** make any non-script file executable. This is not necessary and
     potentially dangerous.

#### 6.3. `installer.bash`

Installer will copy the script file to `/usr/local/bin/`, and source files to
`/usr/local/bin/vfio-script.d/`.

```bash
sudo bash installer.sh
```

#### 6.4. `vfio-script`

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

                            0

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

#### 6.5. VFIO setups
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

### ⚠️ 7. Disclaimer
Did you encounter a bug? Do you need help? Please visit the [Issues][71] page.

[71]: https://github.com/portellam/vfio-script/issues

### ☎️ 8. Contact
Use at your own risk. Please review your system's specifications and resources.

### 🌐 9. References

#### 1.

&nbsp;&nbsp;**QEMU**. qemu.org. Accessed June 4, 2025

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://www.qemu.org/.</sup>

#### 2.

&nbsp;&nbsp;**Kernel-based Virtual Machine**. Wikipedia. Accessed June 4, 2025.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine.</sup>

#### 3.

&nbsp;&nbsp;**Input-output memory management unit**. Wikipedia. Accessed
June 4, 2025.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://en.wikipedia.org/wiki/Input%E2%80%93output_memory_management_unit.</sup>

#### 4.

&nbsp;&nbsp;**VFIO - ‘Virtual Function I/O’ - The Linux Kernel Documentation**.
The linux kernel. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://www.kernel.org/doc/html/latest/driver-api/vfio.html.</sup>

#### 5.

&nbsp;&nbsp;**VFIO Discussion and Support**. Reddit. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://old.reddit.com/r/VFIO/.</sup>

#### 6.
&nbsp;&nbsp;**PCI passthrough via OVMF**. ArchWiki. Accessed June 14, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF.</sup>

#### 7.

&nbsp;&nbsp;**XML Design Format**. GitHub - libvirt/libvirt. Accessed June 18, 2024.

&nbsp;&nbsp;&nbsp;&nbsp;<sup>https://github.com/libvirt/libvirt/blob/master/docs/formatdomain.rst.</sup>

##

#### Click [here](#vfio-script) to return to the top of this document.