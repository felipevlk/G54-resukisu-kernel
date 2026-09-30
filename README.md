# Kernel ReSukiSU + SUSFS — Moto G54 5G (cancunf)

Kernel compilado com **KernelSU (ReSukiSU)** + **SUSFS v2.3.0** (inline hooks) para o
Moto G54 5G (`cancunf`, MT6855), Android 13.

| Info | Valor |
|---|---|
| Kernel | `5.10.269-android12` |
| Root | ReSukiSU (KernelSU fork) |
| SUSFS | v2.3.0 (inline hooks, sem kprobe) |
| Build source | `felipevlk/GKI_KernelSU_SUSFS` (root_flavor=ReSukiSU, use_susfs=true) |

## Arquivos

- `new-boot-resukisu.img` — boot image pronto (flash via fastbootd).
- `resuki-ak3.zip` — AnyKernel3 flashável (via gerenciador/recovery).

## Flash

O bootloader da Motorola bloqueia `fastboot flash boot` ("Preflight validation failed").
Flashear via **fastbootd**:

```bash
adb reboot fastboot
# se voltar pro bootloader, rode: fastboot reboot fastboot
fastboot flash boot new-boot-resukisu.img
fastboot reboot
```

## Gerenciador

APK do gerenciador ReSukiSU v4.2.0 (não incluído aqui — baixe no repo upstream
`ReSukiSU/ReSukiSU`).

---

> Este repositório contém apenas o **binário compilado**. O código-fonte é privado.
