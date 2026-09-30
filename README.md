# Kernel ReSukiSU + SUSFS — Moto G54 5G (cancunf)

Kernel compilado com **KernelSU (ReSukiSU)** + **SUSFS v2.3.0** (inline hooks) para o
Moto G54 5G (`cancunf`, MT6855), Android 13.

| Info | Valor |
|---|---|
| Kernel | `5.10.269-android12` |
| Root | ReSukiSU (KernelSU fork) |
| SUSFS | v2.3.0 (inline hooks, sem kprobe) |
| Build source | [`felipevlk/GKI_KernelSU_SUSFS`](https://github.com/felipevlk/GKI_KernelSU_SUSFS) (build a partir do fork) — `root_flavor=ReSukiSU`, `use_susfs=true` |

## Arquivos (assets da release) — na ordem de uso

| # | Arquivo | O que é |
|---|---|---|
| 1 | `1-boot-resukisu-cancunf.img` | Boot image com ReSukiSU (flash no celular) |
| 2 | `2-anykernel3-resuki.zip` | AnyKernel3 (alternativa de flash via recovery/gerenciador) |
| 3 | `3-gerenciador-resukisu.apk` | Gerenciador ReSukiSU (app do root) |

## Passo a passo

### Passo 1 — Baixar os 3 arquivos
Baixe os 3 assets acima para o PC.

### Passo 2 — Flashar o kernel (boot image)
O bootloader da Motorola bloqueia `fastboot flash boot` ("Preflight validation failed").
Use o **fastbootd**:

```bash
adb reboot fastboot
# se voltar pro bootloader, rode: fastboot reboot fastboot
fastboot flash boot 1-boot-resukisu-cancunf.img
fastboot reboot
```

### Passo 3 — Instalar o gerenciador
Com o celular ligado, instale o `3-gerenciador-resukisu.apk` e abra o app para
conceder/gerenciar o root.

> O `2-anykernel3-resuki.zip` é uma **alternativa** ao passo 2: em vez de flashear a
> imagem direto, dá pra aplicar pelo gerenciador/recovery (AnyKernel3).

## Gerenciador (upstream)

Alternativamente, baixe o manager no repo
[`ReSukiSU/ReSukiSU`](https://github.com/ReSukiSU/ReSukiSU).

---

> Build produzido a partir do fork [`felipevlk/GKI_KernelSU_SUSFS`](https://github.com/felipevlk/GKI_KernelSU_SUSFS).
> Este repositório contém apenas os **binários compilados**.
