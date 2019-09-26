# Logs
- Kernal log information that users can interactively retrieve.
```
dmesg
```
- Logs from the kernel and also daemons. Lists the logs in chronological format.
```
journalctl
```
  - r: Reverse order from newest to oldest.
  - f: Continuously print new logs to the screen as they are made.
  - u: Limit logs to those emitted by a specific system unit (ssh.service).

# Hardware
- Lists the PCI devices
```
lspci
```
- Lists the USB devices  
```
lsusb
```
- Lists the PCMCIA cards
```
lspcmcia
```
- Lists communication resources used by the devices
```
lsdev
```
- Combination of the above programs with some more detail.  
```
Lshw
```
