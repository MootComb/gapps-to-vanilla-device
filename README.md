<h1 align="center">gapps-to-vanilla device</h1>

A recovery script that removes all Google apps (GAPPS) from a device firmware and replaces them with AOSP versions. The result is a "vanilla" system without Google services, but with AOSP equivalents.

It works by comparing the GAPPS image and the VANILLA image of the same GSI build: everything that exists only in GAPPS is deleted, everything that exists only in VANILLA is restored, and differing files are replaced.

---

## Requirements

- Access to fastboot or recovery: TWRP, PBRP, or OrangeFox.
- A device firmware for which a **GAPPS** and **VANILLA** pair of the same version exists (used to generate the ZIP).

---

## Installation Methods

### Method 1 — Ready-made ZIP from Releases

1. Find your firmware version in [Releases](../../releases). If the version matches, download the corresponding ZIP.
2. In recovery, go to **Mount** and check the `system`, `system_ext`, and `product` partitions.
3. In recovery, go to **Settings → General** and **uncheck** **"Unmount system before installing a ZIP"**.
4. Flash the ZIP via **ADB Sideload** or directly from recovery.
5. Wipe **data**, **cache**, **dalvik-cache**, and format data (clean install). If you don't want to touch the **data** partition, you will need to run the additional [`clear.sh`](clear.sh) script in adb shell.

### Method 2 — Generate the ZIP yourself via GitHub Actions

1. Fork the repository. Go to **Actions** and click **"I understand my workflows, go ahead and enable them"**.
2. Go to **Actions → Release → Run workflow**. In the window that opens:
   - in the **URL of the GApps firmware** field, paste the URL of the repository containing your phone's firmware
   - in the **URL of the Vanilla firmware** field, paste the URL of the repository containing the firmware for another phone, a **VANILLA** version that matches the same version number.
3. Click **Run workflow**, wait for it to finish, then go to **Releases** and download the ZIP.
4. Then follow Method 1, steps 2–5:
   - in recovery **Mount** → check `system`, `system_ext`, `product`;
   - **Settings → General** → uncheck **"Unmount system before installing a ZIP"**;
   - flash the ZIP via **ADB Sideload** or from recovery;
   - wipe **data**, **cache**, **dalvik-cache**, and format data (clean install). If you don't want to touch the **data** partition, you will need to run the additional [`clear.sh`](clear.sh) script in adb shell.

Instead of steps 2-5 from step 1, you can flash 3 images via fastboot flash

---

## After Installation: Replacing GMS

To make apps that depend on Google services work, install MicroG:

- [GmsCore](https://github.com/microg/GmsCore/releases) — packages `gms` and `vending`;
- [GsfProxy](https://github.com/MootComb/GsfProxy/releases) — package `gsf`.

---

## Limitations

- Requires a **GAPPS** and **VANILLA** pair of the same device version to generate the ZIP.
- Another format with support only for ext4 and f2fs: [`gapps-to-vanilla-gsi`](https://github.com/MootComb/gapps-to-vanilla-gsi)

---

## License

GPL-3.0. See [LICENSE](LICENSE).
