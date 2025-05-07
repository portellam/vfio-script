# TODO:
- [ ] simplify input params
  - get IOMMU groups to include.
  - get IOMMU groups to exclude.
  - get non VGA groups' IDs, hardware IDs, and driver names.




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