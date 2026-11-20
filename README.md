# Pocket Master CFW 1.0.2 — KS Mod (Bass & Synth Edition)

Modificação experimental de custom firmware (CFW) e aplicativos companheiros para a pedaleira **Sonicake Pocket Master**, focada em **contrabaixo e timbres synth**, baseada na **CFW 1.0.2 (base 1.3.3)**.

> [!CAUTION]
> **AVISO LEGAL — USE POR SUA CONTA E RISCO**
>
> Este projeto é uma modificação experimental sem vínculo oficial com a **Sonicake**.
> * **Instale e teste inteiramente por sua própria conta e risco.**
> * Antes de gravar qualquer arquivo `.bin` na pedaleira, faça **backup completo** de seus presets, Impulse Responses (IRs) e capturas/clones.
> * **Não nos responsabilizamos** por eventuais danos ao hardware, perda de dados, mau funcionamento ou inutilização (*brick*) do equipamento decorrentes do uso deste firmware, dos instaladores ou das instruções aqui descritas.
> * Marcas citadas (*Aguilar®, Tone Hammer®, Walrus Audio®, Ages®, Boss®, OC-2®, Roland®, Juno-60®, Electro-Harmonix®, Bass Micro Synthesizer®, Sonicake®*) pertencem aos seus respectivos proprietários e são usadas apenas como referência sonora de inspiração dos algoritmos.

---

## Estrutura do Repositório

```text
├── firmware/
│   └── PocketMaster_CFW1.0.2_KS_Mod.bin     # Firmware compilado (2.125.752 B, CRCs validados)
├── apps/
│   ├── SonicakeCFW-Setup-1.0.2-KSMod.exe    # Editor Windows patched (sem alerta "not a published release")
│   └── SonicMaster_1.0.10_KSMod.apk         # Editor Android (Flutter 1.0.10+1 com suporte completo KS Mod)
├── presets/
│   ├── Sub-Bass.png                         # Preset MicroSynth: Sub-Bass
│   ├── Synthbass.png                        # Preset MicroSynth: Synthbass
│   └── Wave.png                             # Preset MicroSynth: Wave
├── CHANGELOG.md
├── LICENSE
└── README.md
```

---

## Pedais e Amplificador Adicionados

Além dos módulos originais da CFW 1.0.2, foram desenvolvidos e integrados **5 módulos DSP dedicados** rodando diretamente em **ITCM RAM (`0x1000xxxx` — zero *wait-states*)** para manter o consumo de CPU do DSP baixo e equivalente ao dos pedais nativos:

| Módulo | Slot(s) | Inspiração Sonora | Controles |
| :--- | :--- | :--- | :--- |
| **Tone Hammer** | `AMP` (`#8`) | Aguilar® Tone Hammer® Preamp/DI | `Gain`, `Bass`, `Middle`, `MidFreq`, `Treble`, `VOL`, `AGS` (`Off/On`) |
| **Ages OD** | `DRV` (`#7`) | Walrus Audio® Ages® Overdrive | `Volume`, `Dry`, `Gain`, `Bass`, `Treble`, `Mode` (`1–5`) |
| **OC-2 Oct** | `FX1` (`#6`) e `FX2` (`#11`) | Boss® OC-2 Octaver® analógico | `Oct1` (-1 Oct), `Dry`, `Oct2` (-2 Oct) |
| **J-60 Chorus** | `FX1` (`#6`) e `FX2` (`#11`) | Roland® Juno-60 / June-60 BBD | `I`, `II`, `Mix`, `Tone`, `VOL` |
| **MicroSynth** | `FX2` (`#11`) | EHX® Bass Micro Synthesizer® | `Sub`, `Dry`, `Octave`, `Square`, `Reso`, `Start`, `Stop`, `Rate` |

### Destaques Técnicos da Modificação
* **Execução em ITCM RAM (`0x1000xxxx`):** todos os 5 loops de processamento de áudio a 48 kHz foram portados da Flash SPI para memória ITCM de baixa latência (`FX1` `0x10001000`, `DRV` `0x10002800`, `AMP` `0x10003800`, `FX2` `0x10009000`), com cálculo de coeficientes apenas quando um knob é alterado.
* **Código PIC em `FX1`/`FX2`:** `OC-2 Oct` e `J-60 Chorus` são independentes de posição (*position-independent code*) para funcionar igualmente antes (`FX1`) ou depois (`FX2`) do bloco de drive/amp.
* **Tela de Boot:** animação de inicialização personalizada (`148×48`).
* **Apps atualizados:** tanto o **Sonicake CFW (Windows)** quanto o **SonicMaster (Android)** reconhecem todos os novos `effect_id` e parâmetros, exibindo o selo **KSM / KS Mod** (e no Windows, sem o aviso `"not a published release"` ao carregar o `.bin` customizado).

---

## Presets de Exemplo — MicroSynth

Abaixo estão 3 timbres prontos testados no módulo **MicroSynth** (`FX2`):

### 1. Sub-Bass
Sub-grave puro com varredura descendente longa (~7 kHz → ~55 Hz):
* `Sub: 100` | `Dry: 0` | `Octave: 0` | `Square: 0` | `Reso: 0` | `Start: 100` | `Stop: 0` | `Rate: 0`

![Preset Sub-Bass](presets/Sub-Bass.png)

### 2. Synthbass
Sub-grave encorpado com filtro aberto contínuo (7 kHz):
* `Sub: 100` | `Dry: 0` | `Octave: 0` | `Square: 0` | `Reso: 0` | `Start: 100` | `Stop: 100` | `Rate: 0`

![Preset Synthbass](presets/Synthbass.png)

### 3. Wave
Ataque rápido ascendente (~500 Hz → 7 kHz) misturando sub-oitava, sinal limpo, oitava acima e onda quadrada:
* `Sub: 100` | `Dry: 100` | `Octave: 75` | `Square: 40` | `Reso: 0` | `Start: 50` | `Stop: 100` | `Rate: 100`

![Preset Wave](presets/Wave.png)

---

## Como Instalar (Por Sua Conta e Risco)

### 1. Pré-requisitos e Backup
1. Conecte o Pocket Master ao PC via **USB** e **faça backup** de todos os seus presets, IRs e capturas.
2. Certifique-se de que a bateria da pedaleira esteja carregada ou o cabo USB conectado de forma firme em uma porta traseira da placa-mãe (evite hubs instáveis).

### 2. Instalar o Editor Windows (`SonicakeCFW`)
1. Execute [`apps/SonicakeCFW-Setup-1.0.2-KSMod.exe`](apps/SonicakeCFW-Setup-1.0.2-KSMod.exe) para instalar/atualizar a versão compatível com os 5 módulos do KS Mod e sem o alerta de arquivo não publicado.

### 3. Gravar o Firmware (`.bin`)
* **Arquivo:** [`firmware/PocketMaster_CFW1.0.2_KS_Mod.bin`](firmware/PocketMaster_CFW1.0.2_KS_Mod.bin)
* **Tamanho:** `2.125.752` bytes
* **SHA-256:** `2661264CA336ED537DB9F5501EDD99A882BDBC2B23966FD4252C1ECA7186567D`

1. Abra o **Sonicake CFW** instalado (ou o utilitário de atualização compatível), conecte a pedaleira e entre na tela de atualização de firmware.
2. Selecione `firmware/PocketMaster_CFW1.0.2_KS_Mod.bin` e confirme a gravação.
3. **Não desconecte o cabo nem desligue o pedal** até a barra concluir e o equipamento reiniciar completamente.

> [!NOTE]
> Se vier do firmware oficial (*stock*) pela primeira vez para a base CFW 1.0.2, seus slots de IR e Clones podem ser reordenados/limpos conforme o comportamento padrão da CFW — por isso o backup prévio é indispensável.

### 4. App Android (`SonicMaster KS Mod`)
1. Transfira e instale [`apps/SonicMaster_1.0.10_KSMod.apk`](apps/SonicMaster_1.0.10_KSMod.apk) no seu dispositivo Android (habilitando instalação de fontes desconhecidas).
2. Conecte via USB-OTG ou Bluetooth para editar todos os parâmetros nativos e os 5 efeitos do KS Mod pelo celular.

---

## Créditos e Base do Projeto

Este mod foi construído sobre a **Pocket Master Custom Firmware (CFW 1.0.2)** e o ecossistema **Sonicake CFW**, projetos desenvolvidos pelo autor original da CFW:

* Site oficial da CFW base: https://pocketmaster-cfw.guitar-training-generator.com/

Todos os créditos pelo desenvolvimento inicial da arquitetura CFW 1.0.2, desbloqueio de slots e ferramentas base pertencem ao criador original.

---

## Licença

Distribuído sob os termos da licença em [`LICENSE`](LICENSE) (**sem garantias** de qualquer tipo).
