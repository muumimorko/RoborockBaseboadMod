# Roborock S5 Wall Distance Mod

Binary modification for Roborock S5 that allows it to follow walls with shallow baseboards without bumping into them constantly.

## Description

Older vacuum firmwares loaded navigation configuration variables from `/opt/rockrobo/cleaner/lib/`[Nav.cfg](Nav.cfg). Newer ones have them hardcoded in `librrnavdrv.so`.

Modied following values, for circa 12 mm thick baseboards:
| Address | Type  | Stock | Mod   | Suspected name in Nav.conf |
| ------- | ----- | ----- | ----- | -------------- |
308E08 | (u)int32 | 175   | 189   | Robot.radius
308E0C | float32  | 178,5 | 192,5 | Robot.radiusWithGlue
309068 | (u)int32 | 13    | 30    | WallFollower.DIS_EXPECTED_WALL
309124 | (u)int32 | 12	  | 30    | WallFollowerST.DIS_EXPECTED_WALL

### Premodified files
* `librrnavdrv_2020_modded.so` for firmware version `v11_002020.fullos.6fbc6417-7a69-495a-879c-41fec575d6be.pkg`.
* **UNTESTED** `librrnavdrv_2034_modded.so` for firmware version `v11_002034.fullos.55915876-2190-407a-9fcb-f1e760d9b623`.

## Installation
* Root vacuum (dustcloud/dustbuilder)
* Remember backups
* Replace `/opt/rockrobo/cleaner/lib/librrnavdr.so` with `librrnavdrv_FWVERSION_modded.so` or modify your own.

### Example:
```
ssh root@IPADDRESS "cp /opt/rockrobo/cleaner/lib/librrnavdr.so /opt/rockrobo/cleaner/lib/librrnavdr.so.bak"
mkdir tmp
cp librrnavdrv_FWVERSION_modded.so tmp/librrnavdrv.so
scp tmp/librrnavdrv.so root@IPADDRESS:/opt/rockrobo/cleaner/lib/
rm -r tmp
```