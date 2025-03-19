# Sneaky Patch
## Description
A high-value system has been compromised. Security analysts have detected suspicious activity within the kernel, but the attacker’s presence remains hidden. Traditional detection tools have failed, and the intruder has established deep persistence. Investigate a live system suspected of running a kernel-level backdoor.

It's provided a Machine to investigate
## Solution
From the description, we thought in starting searching in the kernel logs. Executing the command:
```bash
sudo dmesg
```
It was possible to watch some interesting things from the output:
```bash
[   26.371308] systemd-journald[132]: File /var/log/journal/dc7c8ac5c09a4bbfaf3d09d399f10d96/user-1000.journal corrupted or uncleanly shut down, renaming and replacing.
[   32.701060] spatch: loading out-of-tree module taints kernel.
[   32.701072] spatch: module verification failed: signature and/or required key missing - tainting kernel
[   32.702610] [CIPHER BACKDOOR] Module loaded. Write data to /proc/cipher_bd
[   32.704977] [CIPHER BACKDOOR] Executing command: id
[   32.711742] [CIPHER BACKDOOR] Command Output: uid=0(root) gid=0(root) groups=0(root)

[   41.059522] traps: mate-power-mana[1887] trap int3 ip:71d3aec050df sp:7fff1aa8dd40 error:0 in libglib-2.0.so.0.8000.0[71d3aebc1000+a0000]
```
We can observe:
- Module 'spatch' loaded, it's out-of-tree & tainted, this proves that this module is not suppose to be in kernel.
- The backdoor exists ([CIPHER BACKDOOR]) and accepts commands though the /proc/cipher_bd archive.
Let's find where this 'spatch' is:
```bash
find / -type f -name 'spatch.ko' 2>/dev/null
```
Output:
```bash
/lib/modules/6.8.0-1016-aws/kernel/drivers/misc/spatch.ko
```
After getting the path we search inside the module:
```bash
strings /lib/modules/6.8.0-1016-aws/kernel/drivers/misc/spatch.ko | less
```
Output:
```bash
6[CIPHER BACKDOOR] Module loaded. Write data to /proc/%s
6[CIPHER BACKDOOR] Module unloaded.
3[CIPHER BACKDOOR] Failed to read output file
6[CIPHER BACKDOOR] Command Output: %s
3[CIPHER BACKDOOR] No output captured.
6[CIPHER BACKDOOR] Executing command: %s
3[CIPHER BACKDOOR] Failed to setup usermode helper.
6[CIPHER BACKDOOR] Format: echo "COMMAND" > /proc/cipher_bd
6[CIPHER BACKDOOR] Try: echo "%s" > /proc/cipher_bd
6[CIPHER BACKDOOR] Here's the secret: 54484d7b73757033725f736e33346b795f643030727d0a
PATH=/sbin:/bin:/usr/sbin:/usr/bin
description=Cipher is always root
```
Interesting:

**6[CIPHER BACKDOOR] Here's the secret: 54484d7b73757033725f736e33346b795f643030727d0a**

Using CyberChef[https://cyberchef.org/] to convert the hash from hexa to text:

**THM{sup3r_sn34ky_d00r}**
