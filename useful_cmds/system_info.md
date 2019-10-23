# System\_Info

## Logs

* Kernal log information that users can interactively retrieve.

  ```text
  dmesg
  ```

* Logs from the kernel and also daemons. Lists the logs in chronological format.

  ```text
  journalctl
  ```

  * r: Reverse order from newest to oldest.
  * f: Continuously print new logs to the screen as they are made.
  * u: Limit logs to those emitted by a specific system unit \(ssh.service\).

## Hardware

* Lists the PCI devices

  ```text
  lspci
  ```

  - Lists the USB devices  

  ```text
  lsusb
  ```

* Lists the PCMCIA cards

  ```text
  lspcmcia
  ```

* Lists communication resources used by the devices

  ```text
  lsdev
  ```

* Combination of the above programs with some more detail.  

  ```text
  Lshw
  ```

