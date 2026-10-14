# JioRouter AX6000 — Flashing OpenWrt via SSH
### Applies to: JIDU6101 and JIDU6201 / JIDU6401 / JIDU6601 / JIDU6701

---

## Step 1 — Backup

**Get U-Boot password** (MFG partition number can vary by device, so find it by name first):
```bash
cat /proc/mtd
```
Look for the line containing `"MFG"` and note its number (e.g. `mtd6`, `mtd7`), then:
```bash
strings /dev/mtd<X> | grep -i pass
```
Replace `<X>` with the number you found.

Alternative method:
```bash
/usr/bin/mfg_data get bootpass
```

**Backup partitions (from PC):**
```bash
ssh root@192.168.31.1 "cat /dev/mtd1" > mtd1_BL2.bin
ssh root@192.168.31.1 "cat /dev/mtd2" > mtd2_uboot_env.bin
ssh root@192.168.31.1 "cat /dev/mtd3" > mtd3_Factory.bin
ssh root@192.168.31.1 "cat /dev/mtd4" > mtd4_FIP.bin
ssh root@192.168.31.1 "cat /dev/mtd5" > mtd5_ubi.bin
ssh root@192.168.31.1 "cat /dev/mtd6" > mtd6_ubi2.bin
ssh root@192.168.31.1 "cat /dev/mtd7" > mtd7_MFG.bin
ssh root@192.168.31.1 "cat /dev/mtd8" > mtd8_Jio_Reserved.bin
```

---

## Step 2 — Flash OpenWrt

**From PC:**
```bash
scp -O openwrt-*-initramfs-factory.ubi root@192.168.31.1:/tmp/
```

**On router:**
```bash
ubidetach -m 6

ubiformat /dev/mtd6 -y -f /tmp/openwrt-*-initramfs-factory.ubi

fw_setenv bootcmd 'ubi detach; ubi part ubi2; ubi read 46000000 kernel; fdt addr $(fdtcontroladdr); fdt rm /signature; bootm 0x46000000'

fw_setenv dual_boot.current_slot 1
fw_setenv dual_boot.slot_0_invalid 1
fw_setenv dual_boot.slot_1_invalid 1
fw_setenv ipaddr

reboot
```

---

## Step 3 — Permanent Install (Sysupgrade)

**From PC:**
```bash
scp -O openwrt-*-squashfs-sysupgrade.bin root@192.168.1.1:/tmp/
```

**On router:**
```bash
sysupgrade /tmp/openwrt-*-squashfs-sysupgrade.bin
```

Router reboots — OpenWrt is now permanently installed.
