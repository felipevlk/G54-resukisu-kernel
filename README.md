# Kernel ReSukiSU + SUSFS — Moto G54 5G (cancunf)

Kernel compilado com **KernelSU (ReSukiSU)** + **SUSFS v2.3.0** (inline hooks) para o
Moto G54 5G (`cancunf`, MT6855), Android 13.

| Info | Valor |
|---|---|
| Kernel | `5.10.269-android12` |
| Root | ReSukiSU (KernelSU fork) |
| SUSFS | v2.3.0 (inline hooks, sem kprobe) |
| Build source | [`felipevlk/GKI_KernelSU_SUSFS`](https://github.com/felipevlk/GKI_KernelSU_SUSFS) — `root_flavor=ReSukiSU`, `use_susfs=true` |

## Compatibilidade

| Item | Valor |
|---|---|
| Aparelho | Moto G54 5G (`cancunf`) |
| SoC | MediaTek MT6855 (Dimensity 7020/930) |
| Android | 13 (SDK 33) |
| Branch do kernel (GKI) | **5.10 `android12`** |
| Kernel stock (base de origem) | `5.10.168` |
| Kernel deste build | `5.10.269-android12` |
| Page size | 4K |

> Este boot é feito para o **Moto G54 5G** com kernel **GKI 5.10 `android12`** e **4K page**.
> Não usar em outros aparelhos / branches — risco de bootloop.

## Arquivos (assets da release)

- `1-boot-resukisu-cancunf.img` — boot image pronta (flash via fastbootd).
- `2-anykernel3-resuki.zip` — AnyKernel3 flashável (via gerenciador/recovery).
- `3-gerenciador-resukisu.apk` — gerenciador ReSukiSU.

## Flash

O bootloader da Motorola bloqueia `fastboot flash boot` ("Preflight validation failed").
Flashear via **fastbootd**:

```bash
adb reboot fastboot
# se voltar pro bootloader, rode: fastboot reboot fastboot
fastboot flash boot 1-boot-resukisu-cancunf.img
fastboot reboot
```

Depois instale o gerenciador:

```bash
adb install 3-gerenciador-resukisu.apk
```

## Patches aplicados (esconder root)

Além do ReSukiSU + SUSFS, foram aplicados:

| Patch | Versão | Função |
|---|---|---|
| SUSFS | v2.3.0 (inline hooks) | oculta arquivos/mounts/ksu do userspace |
| brene | — | config do SUSFS (props, uname spoof, hide) |
| TrickyStore | 1.4.1 (`5ec1cff`) | atestação de certificado |
| PlayIntegrityFix | v19.9104 | props de integridade |
| ZygiskNext / ZygiskSU | 1.5.0 | suporte Zygisk |
| NoMount (metamódulo) | v2.0.0 | gerenciamento de mounts |
| ZN-AuditPatch | v1.2.0 (`aviraxp`) | corrige o audit SELinux |
| ksud (uapi fix) | 3.4.0-18 | corrige os scripts de boot dos módulos |

### Configs aplicadas no aparelho

- `/data/adb/tricky_store/target.txt` — GMS + vending + gsf + gms.unstable + bancopan + detectores
- `/data/adb/tricky_store/security_patch.txt` — `system=202401 / boot=2024-01-01 / vendor=2024-01-01`
- `/data/adb/brene/config.sh` — `config_spoof_system_properties=1`, `config_spoof_uname=1`, `config_selinux_hide=1`, `config_su_compat=1`
- uname SUSFS: `susfs set_uname "5.10.269-android12" "#1 SMP PREEMPT"`

## Resultado

- Play Integrity: **BASIC 🟢 + DEVICE 🟢**
- Duck Detector: 1 Danger (TEE/KeyMint — hardware)
- Chunqiu Native Check: 0 (só "USB debugging", temporário)

---

> Build produzido a partir do fork [`felipevlk/GKI_KernelSU_SUSFS`](https://github.com/felipevlk/GKI_KernelSU_SUSFS).
> Este repositório contém apenas os **binários compilados**.
