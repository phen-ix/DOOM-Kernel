# DOOM Kernel — miatoll

Custom Linux kernel for the Xiaomi **miatoll** family (Qualcomm atoll / SM7125).

Base tree: Qualcomm CAF `msm-4.14` · stable: **OpenELA ELTS 4.14.357** · toolchain: **Clang 22**.

| Codename | Device |
|---|---|
| `joyeuse` | Redmi Note 9 Pro |
| `curtana` | Redmi Note 9S |
| `excalibur` | Redmi Note 9 Pro Max |
| `gram` | POCO M2 Pro |

---

## Highlights

**Power**
- `cpuidle`: TEO governor now actually enters C1/C2 instead of pinning every CPU in C0
  (a CPU with no PM-QoS object no longer reports a zero latency request; a zero request
  is treated as unconstrained, matching `menu`).
- `schedutil`: `min_rate_limit_ns` is initialised, so the rate limit is sane from boot.
- BBR3 alongside BBR.

**Kernel**
- KernelSU built in (4.14 syscall-table hooking + LSM hooks).
- WireGuard as a built-in module.
- NoMount v2.3.0 (`fs/nomount`).

**Display**
- KCal colour control on the SDE/DRM path — **chosen at flash time**, not compiled per build.

**Observability**
- `log_buf_len=4M` via `patch_cmdline`, so the early boot window survives in `dmesg`.
- Roughly a third of the boot-time `dmesg` noise removed; the calls stay behind dynamic debug.

---

## Install

1. Download the newest ZIP from **Releases** (`ci-latest` → `DOOM-Kernel-miatoll-<sha>.zip`).
2. Reboot to recovery (or flash with Kernel Flasher / KernelSU manager).
3. Flash the ZIP. The installer asks once:

   ```
   KCal: VOL UP = ON | VOL DOWN or no key = OFF (10s)
   ```

4. Keep the previous ZIP — rolling back is just flashing it again.

The installer asserts the device code name, so it refuses to flash on anything outside
`curtana`, `excalibur`, `gram`, `joyeuse`, `miatoll`.

## Build

CI (`.github/workflows/miatoll-kernel.yml`) runs on pushes to `arena/**` and `16`, on pull
requests, and on manual dispatch. Add `[skip ci]` to the commit message to push without
building. A successful run replaces the `ci-latest` release asset.

Locally:

```sh
scripts/build-miatoll.sh          # -> out/miatoll/anykernel/DOOM-Kernel-miatoll-<sha>.zip
```

The build takes `vendor/xiaomi/miatoll_defconfig`, enables `DRM_MSM_KCAL_CTRL`, then
packages the kernel + `cust-atoll-ab.dtb` and the four device overlays into an AnyKernel3 ZIP.

## Documentation

See [`docs/README.md`](docs/README.md) for the integration records and build evidence.

## Credits

- Base tree and miatoll device bring-up: **RoHaNRaJ**
- Stable patches: **OpenELA ELTS**
- AnyKernel3: **osm0sis**
- NoMount: **maxsteeel**
- KernelSU: **tiann**

## License

GPL-2.0 — see [`COPYING`](COPYING).
