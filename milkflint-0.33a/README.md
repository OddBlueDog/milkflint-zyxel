# MilkFlint 0.33a for the Zyxel EX5601-T0 / T-56

Replaced by [0.34a](../milkflint-0.34a/), which fixes the debug recorder
(the Logs page's debug counters): flash that one instead.

> [!WARNING]
> Untested and experimental: read the [main README](../README.md) first, and
> only flash one of these if you have a way to recover the router.

MilkFlint 0.32a (OpenWrt 25.12.6) plus the Operating Mode page (router or
access point) and a software fast path for bridged connections, off by
default.

| Layout (`cat /tmp/sysinfo/board_name`) | Image | SHA-256 |
|---|---|---|
| `zyxel,ex5601-t0-stock` | [`zyxel_ex5601-t0-stock/…-squashfs-sysupgrade.bin`](zyxel_ex5601-t0-stock/milkflint-0.33a-r33311-981c978eff-mediatek-filogic-zyxel_ex5601-t0-stock-squashfs-sysupgrade.bin) | `8c79051198f1abb80b1b7a38cea5435d69dee7118a2efad1e49605ccd32a3010` |
| `zyxel,ex5601-t0-ubootmod` | [`zyxel_ex5601-t0-ubootmod/…-squashfs-sysupgrade.itb`](zyxel_ex5601-t0-ubootmod/milkflint-0.33a-r33311-981c978eff-mediatek-filogic-zyxel_ex5601-t0-ubootmod-squashfs-sysupgrade.itb) | `4e28793a154554ee3f4e42a0ca4588d1b88e03320b26a4197dbc1f896f098c64` |

Flash it from OpenWrt without keeping settings (`sysupgrade -n`), as the
main README says.
