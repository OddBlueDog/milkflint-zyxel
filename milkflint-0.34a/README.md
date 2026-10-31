# MilkFlint 0.34a for the Zyxel EX5601-T0 / T-56

> [!WARNING]
> Untested and experimental: read the [main README](../README.md) first, and
> only flash one of these if you have a way to recover the router.

0.33a with the debug recorder fixed: with the Logs page's debug counters
on, it stopped at the first kernel message and started again, over and
over. Like 0.33a: MilkFlint 0.32a (OpenWrt 25.12.6) plus the Operating Mode
page (router or access point) and a software fast path for bridged
connections, off by default.

| Layout (`cat /tmp/sysinfo/board_name`) | Image | SHA-256 |
|---|---|---|
| `zyxel,ex5601-t0-stock` | [`zyxel_ex5601-t0-stock/…-squashfs-sysupgrade.bin`](zyxel_ex5601-t0-stock/milkflint-0.34a-r33311-981c978eff-mediatek-filogic-zyxel_ex5601-t0-stock-squashfs-sysupgrade.bin) | `ece2e9f25b09618654ee6e4a13c7e9b203d7e1b8549d38c81d4650e0e6a2d6cb` |
| `zyxel,ex5601-t0-ubootmod` | [`zyxel_ex5601-t0-ubootmod/…-squashfs-sysupgrade.itb`](zyxel_ex5601-t0-ubootmod/milkflint-0.34a-r33311-981c978eff-mediatek-filogic-zyxel_ex5601-t0-ubootmod-squashfs-sysupgrade.itb) | `c43655a3b1610f9be29578081e23e30de08b24e7d5a4d662a44cac3e4406b248` |

Flash it from OpenWrt without keeping settings (`sysupgrade -n`), as the
main README says.
