# Kernel ReSukiSU + SUSFS — Moto G54 5G (cancunf)

Kernel compilado com **KernelSU (ReSukiSU)** + **SUSFS v2.3.0** (inline hooks) para o
Moto G54 5G (`cancunf`, MT6855), Android 13.

| Info | Valor |
|---|---|
| Kernel | `5.10.269-android12` |
| Root | ReSukiSU (KernelSU fork) |
| SUSFS | v2.3.0 (inline hooks, sem kprobe) |
| Build source | [`felipevlk/GKI_KernelSU_SUSFS`](https://github.com/felipevlk/GKI_KernelSU_SUSFS) (build a partir do fork) — `root_flavor=ReSukiSU`, `use_susfs=true` |

## Arquivos (assets da release)

- `new-boot-resukisu.img` — boot image pronto (flash via fastbootd).
- `resuki-ak3.zip` — AnyKernel3 flashável (via gerenciador/recovery).
- `ReSukiSU_v4.2.0-rc3_35187-universal-release.apk` — gerenciador ReSukiSU (instalar após o flash).
- `boot-fallback-KernelSU-Next.img` — boot de fallback (root anterior, KernelSU-Next). Use só em emergência.

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

Instale o `ReSukiSU_v4.2.0-rc3_35187-universal-release.apk` (asset desta release) após
flashear o kernel. Alternativamente, baixe no repo upstream
[`ReSukiSU/ReSukiSU`](https://github.com/ReSukiSU/ReSukiSU).

## Fallback

Se o ReSukiSU falhar, flashe `boot-fallback-KernelSU-Next.img` (root anterior) para
restaurar o acesso root. Nesse modo voltam os hooks kprobe (detectáveis).

---

> Build produzido a partir do fork [`felipevlk/GKI_KernelSU_SUSFS`](https://github.com/felipevlk/GKI_KernelSU_SUSFS).
> Este repositório contém apenas os **binários compilados**.
