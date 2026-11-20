# Changelog — Pocket Master CFW 1.0.2 (KS Mod)

Todas as alterações relevantes aplicadas sobre a base **Pocket Master CFW 1.0.2 (1.3.3)** estão registradas abaixo.

---

## [1.0.2-KSMod]

### Adicionado (Firmware)
* **`Tone Hammer`** (`AMP`): Preamp/DI de baixo baseado no Aguilar® Tone Hammer®, com EQ de 3 bandas, varredura de `MidFreq`, volume estendido e chave `AGS`.
* **`Ages OD`** (`DRV`): Overdrive de baixo com 5 modos (`1–5`), blend paralelo `Dry`, `Bass` e `Treble`.
* **`OC-2 Oct`** (`FX1` e `FX2`): Oitavador analógico estilo Boss® OC-2® com `Oct1` (`-1 Oct`), `Dry` e `Oct2` (`-2 Oct`).
* **`J-60 Chorus`** (`FX1` e `FX2`): Chorus estéreo inspirado no Roland® Juno-60® com chaves `I` e `II`, `Mix`, `Tone` e `VOL`.
* **`MicroSynth`** (`FX2`): Sintetizador de baixo baseado no EHX® Bass Micro Synthesizer® com vozes `Sub`, `Dry`, `Octave`, `Square` e varredura de filtro (`Reso`, `Start`, `Stop`, `Rate`).
* **Tela de boot personalizada:** nova animação de inicialização `KS Mod`.

### Melhorias e Correções
* **Otimização de desempenho:** processamento dos 5 módulos ajustado para manter uso de DSP baixo e estável mesmo com toda a cadeia ligada.
* **Correção no `OC-2 Oct`:** corrigida a inicialização dos divisores de oitava para que `Oct1` e `Oct2` funcionem normalmente junto ao `Dry`.
* **Correção no `MicroSynth`:** corrigida a inicialização do disparo/varredura do filtro.

### Editor Windows (`SonicakeCFW-Setup-1.0.2-KSMod.exe`)
* Suporte completo aos 5 novos módulos (nomes, controles, descrições e envio de parâmetros via USB/SysEx).
* Badge de origem atualizado para `KSM`.
* Removidos os avisos `"This file is not a published release: flash it only if you know where it comes from."` e `" (not a published release)"` ao selecionar arquivos `.bin`.
