# MilkFlint for the Zyxel EX5601-T0 / T-56

[MilkFlint](https://github.com/OddBlueDog/openwrt) is firmware based on
OpenWrt 25.12, made for the GL.iNet GL-MT6000 (Flint 2), with its own web
interface. These are builds of it for the Zyxel EX5601-T0 (also sold as the
EX5601-T1 and as Telenor's T-56), which has the same MediaTek MT7986.

> [!CAUTION]
> **Flashing these images could brick your router.** They have never been
> run on an EX5601, so nobody knows yet whether they boot. If one doesn't,
> or boots without working network ports, the router stops answering, and
> only a serial cable and OpenWrt's recovery steps can bring it back, if
> anything can. You flash them at your own risk: there's no warranty and no
> promise that a bricked router can be recovered.

> [!WARNING]
> **Untested and experimental.** These images are built from the same tree
> as the GL-MT6000's, but they haven't been run on an EX5601 yet. They may
> not boot, and Wi-Fi or the ports may not work. MilkFlint itself is an
> alpha.
>
> **Only flash one if you have a way to recover the router** when it doesn't
> boot (a serial console and
> [OpenWrt's recovery steps](https://openwrt.org/toh/zyxel/t-56#debricking))
> and know how to use it. Try one router first, not all of them.

## Which image

OpenWrt has two flash layouts for the EX5601, and each has its own image.
On the router's OpenWrt, `cat /tmp/sysinfo/board_name` says which one it
has:

| `board_name` | Folder | Image |
|---|---|---|
| `zyxel,ex5601-t0-ubootmod` (OpenWrt's U-Boot) | `zyxel_ex5601-t0-ubootmod/` | `…-squashfs-sysupgrade.itb` |
| `zyxel,ex5601-t0-stock` (Zyxel's bootloader) | `zyxel_ex5601-t0-stock/` | `…-squashfs-sysupgrade.bin` |

Each version has a folder (the newest is `milkflint-0.34a/`) with one folder
per layout.
OpenWrt refuses an image made for the other layout.

## Installing

1. Install OpenWrt on the router first, following
   [OpenWrt's device page](https://openwrt.org/toh/zyxel/t-56#installation)
   (filed under the T-56, an ISP's EX5601-T1: the same router without the
   SFP+ port) and the
   [EX5601-T0 forum thread](https://forum.openwrt.org/t/adding-openwrt-support-for-zyxel-ex5601-t0/155914),
   and make sure you can recover it from there before going on.
2. Check the image against its `.sha256` file:
   `sha256sum -c milkflint-…-sysupgrade.bin.sha256`.
3. Flash the image for its layout **without keeping settings**: in LuCI,
   System → Backup / Flash Firmware → Flash image, untick "Keep settings";
   from a shell, `sysupgrade -n /tmp/milkflint-…`.
4. Plug a cable into a LAN port (`lan1` to `lan4`) and open
   <http://192.168.1.1>. There's no password yet: sign in with it empty and
   set one under System → Admin Password. Wi-Fi is off until you set it up
   on the Wi-Fi page, with your country.

This repo has only the sysupgrade images, no bootloader images, so nothing
here replaces the router's bootloader. OpenWrt's downloads also have
preloader and bl31-uboot images for the EX5601: never flash one of those
unless OpenWrt's page tells you to, as they replace the bootloader.

To go back, flash OpenWrt's sysupgrade image for your layout, again without
keeping settings.

## As an access point

Network → Operating Mode switches between router and access point (bridge
mode). With its WAN port cabled to your main router, the switch to access
point mode takes its address from the main router and then checks that it
can reach it; if it can't within two minutes, the router goes back to
router mode by itself. It's then at the address your main router gave it.
Leave it on during those two minutes: a switch cut short by a power cut or
a reboot isn't undone.

## Reports

Reports are welcome as an issue here, working or not: which layout
(`cat /tmp/sysinfo/board_name`), the boot log (`dmesg` and `logread` after
it starts), `ubus call system board`, whether both Wi-Fi bands come up and
devices can join each, and how a switch to access point mode and back
went.

## Versions

- **[0.34a](milkflint-0.34a/)**: the newest. 0.33a with the debug recorder
  fixed: with the Logs page's debug counters on, it stopped at the first
  kernel message and started again, over and over.
- **[0.33a](milkflint-0.33a/)**: the first EX5601 images, replaced by 0.34a.
  MilkFlint 0.32a (OpenWrt 25.12.6) plus the Operating Mode page (router or
  access point) and a software fast path for bridged connections, off by
  default.

## Source

Built from MilkFlint's OpenWrt branch,
[`milkflint-25.12`](https://github.com/OddBlueDog/openwrt/tree/milkflint-25.12),
which has OpenWrt's source and MilkFlint's changes; building it is in its
README.

- **0.34a**: commit
  [`0f0528ebfa`](https://github.com/OddBlueDog/openwrt/commit/0f0528ebfa987b0eb3dbeacf4bd87f02ef330629).
- **0.33a**: the same commit without the debug recorder's fix (in
  `package/milkflint/milkflint-ui/files/features/logs/bin/logs-keeper`) and
  with its own version number; the kernel, OpenWrt and everything else in
  it are the same.
