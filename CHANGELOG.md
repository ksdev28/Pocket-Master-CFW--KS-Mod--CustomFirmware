# Changelog — Pocket Master CFW 1.0.2 (KS Mod)

Todas as alterações relevantes aplicadas sobre a base **Pocket Master CFW 1.0.2 (1.3.3)** estão registradas abaixo.

---

## [1.0.2-KSMod] — ITCM Performance Fix, OC-2/MicroSynth Init Fix & App Updates

### Adicionado (Firmware `sec2` + `sec5`)
* **`Tone Hammer`** (`AMP` slot 8, `eid=0x0078`, `mid=0x07`, UI ID `339`): Preamp/DI baseado no Aguilar® Tone Hammer® com EQ de 3 bandas, `MidFreq` varredurável (`180 Hz–1 kHz`), +6 dB de headroom em `VOL` e chave `AGS` com crossover dinâmico.
* **`Ages OD`** (`DRV` slot 7, `eid=0x0042`, `mid=0x03`, UI ID `209`): Overdrive de 5 modos (`Lo-Si`, `Lo-LED`, `Hi-Si`, `Hi-LED`, `Hard`) com blend paralelo `Dry`, realimentação `Bass` e shelf `Treble`.
* **`OC-2 Oct`** (`FX1` slot 6 e `FX2` slot 11, `eid=0x002A`, `mid=0x01`, UI ID `130`): Oitavador analógico monofônico estilo Boss® OC-2® com `Oct1` (`-1 Oct`), `Dry` e `Oct2` (`-2 Oct`).
* **`J-60 Chorus`** (`FX1` slot 6 e `FX2` slot 11, `eid=0x002C`, `mid=0x04`, UI ID `129`): Chorus BBD estéreo inspirado no Roland® Juno-60® com chaves `I` e `II`, LPF BBD (`Tone`), HPF 120 Hz no caminho *wet*, `Mix` e `VOL`.
* **`MicroSynth`** (`FX2` slot 11, `eid=0x002D`, `mid=0x01`, UI ID `128`): Sintetizador de baixo baseado no EHX® Bass Micro Synthesizer® com vozes `Sub`, `Dry`, `Octave`, `Square` e filtro ressonante 3 polos (`Reso`, `Start`, `Stop`, `Rate`).
* **Boot GIF customizado (`sec4`):** tela inicial `148×48` atualizada dentro do bloco seguro (`16.183 B`).

### Otimizado
* **Porte completo de DSP para ITCM RAM (`0x1000xxxx`):**
  * Eliminada a execução XIP em Flash SPI durante o loop de áudio a 48 kHz (que causava pico de CPU% ao ativar os novos pedais).
  * Carregador `init_slot_idx()` com barreiras `dsb sy; isb sy` copiando `.itcm_j60`, `.itcm_oc2`, `.itcm_ms`, `.itcm_ages` e `.itcm_bh` para os bancos ITCM de `FX1` (`0x10001000`), `DRV` (`0x10002800`), `AMP` (`0x10003800`) e `FX2` (`0x10009000`).
  * `OC-2 Oct` e `J-60 Chorus` compilados 100% PIC (sem ponteiros absolutos) para compartilhamento de código entre `FX1` e `FX2`.
  * Divisões pesadas `vdiv.f32` por amostra substituídas por aproximação Newton-Raphson (`rcp1`) nos clippers/mixers; cálculo de coeficientes biquad movido para *cold path* em Flash executado apenas na alteração de parâmetros.
  * Todos os módulos empacotados nos 3 buracos seguros `0xFF` da `sec2` (`Hole 0`: `2032/2044 B`, `Hole 1`: `3492/3516 B`, `Hole 2`: `1688 B` código + cabeçalhos/tabelas até `0x3f098/0x3f0bc`).

### Corrigido
* **`OC-2 Oct` saindo apenas som limpo (`Dry`):** corrigidos os índices de inicialização de `div2` (`word[52]` / `+0xd0`) e `div4` (`word[53]` / `+0xd4`) em `Oc2ItcmState` no carregador ITCM (antes estavam sendo gravados fora da struct, mantendo os divisores zerados).
* **`MicroSynth` trigger/sweep na inicialização:** corrigidos os índices `trig_armed` (`word[21]` / `+0x54`) e `sweep_phase` (`word[23]` / `+0x5c`) em `MicroSynthState`, evitando gravação acidental em `trig_hold` (`+0x58`).

### Aplicativos Companheiros (Windows & Android)
* **`SonicakeCFW` Windows (`SonicakeCFW-Setup-1.0.2-KSMod.exe`):**
  * Adicionadas definições, assinaturas SysEx, metadados `AMP LOOK` e comandos de parâmetros (`6.548` comandos validados com CRC-8) para os 5 efeitos.
  * Selo de origem atualizado para `KSM`.
  * Removidas as mensagens `"This file is not a published release: flash it only if you know where it comes from."` e `" (not a published release)"` no seletor de `.bin`.
* **`SonicMaster` Android (`SonicMaster_1.0.10_KSMod.apk`):**
  * Compilação nativa Flutter `v1.0.10+1` com suporte completo aos 5 novos efeitos/parâmetros, exibição de informações e selo **KS Mod**.
