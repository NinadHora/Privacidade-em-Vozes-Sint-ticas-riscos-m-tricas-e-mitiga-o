
# Privacidade em Biometria de Voz & Vozes Sintéticas — Tutorial (Python Brasil 2025)

[![Abrir no Colab](https://img.shields.io/badge/Colab-abrir_notebook-yellow.svg)]([LINK_COLAB_AQUI])
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![CI](https://img.shields.io/github/actions/workflow/status/[SEU_USUARIO]/[NOME_REPO]/ci.yml?label=CI)](./.github/workflows/ci.yml)

Repositório do tutorial **mão-na-massa (3h)** sobre **privacidade de dados** em biometria de voz e vozes sintéticas.  
Foco prático: **detectar áudio fake/real**, medir **riscos de privacidade** (membership inference e reidentificação) e aplicar **mitigações**.

---

## Sumário
- [🎯 Objetivos de aprendizagem](#-objetivos-de-aprendizagem)
- [🧰 Pré-requisitos](#-pré-requisitos)
- [🚀 Como executar](#-como-executar)
- [🔬 Pipeline e notebooks](#-pipeline-e-notebooks)
- [📈 Métricas e privacidade](#-métricas-e-privacidade)
- [🧪 Critérios de publicação (go/no-go)](#-critérios-de-publicação-go-no-go)
- [🗂️ Estrutura do repositório](#️-estrutura-do-repositório)
- [📚 Dados e licenças](#-dados-e-licenças)
- [🛡️ Ética, LGPD e governança](#️-ética-lgpd-e-governança)
- [🛠️ Solução de problemas](#️-solução-de-problemas)
- [📝 Citação](#-citação)
- [📄 Licença](#-licença)

---

## 🎯 Objetivos de aprendizagem
- Carregar e inspecionar o dataset **[`Shahzaib-Arshad/audio-fake-real-dataset`](https://huggingface.co/datasets/Shahzaib-Arshad/audio-fake-real-dataset)**.
- Treinar baselines:
  - **MFCC + Regressão Logística** (rápido/CPU).
  - **Embeddings wav2vec2 + MLP** (robusto; pré-treino).
- Avaliar **AUC**, **F1**, **EER** (biometria), **calibração** (**ECE/NLL**).
- Medir riscos:
  - **Membership Inference (MIA)** simplificado (confiança/perda).
  - **Reidentificação** com **ECAPA** (similaridade/Top-k).
- Aplicar **mitigações**: calibragem (temperature scaling), regularização/augmentations, minimização/retensão e política de exportação de scores/embeddings.

---

## 🧰 Pré-requisitos
- Python **3.10+**.
- CPU suficiente para MFCC + LR; **GPU opcional** (Colab) acelera wav2vec2/ECAPA.
- `pip` ou `conda`.

---

## 🚀 Como executar

### Google Colab (recomendado)
1. Clique no badge **Abrir no Colab** acima e execute as células na ordem.
2. No bloco **Configuração**, ajuste:
   - `FAST_MODE=True` para ensaio rápido/CPU.
   - Aumente `LIMIT_W2V` se tiver **GPU**.

### Local (CPU)
```bash
python -m venv .venv && source .venv/bin/activate     # (Windows) .venv\Scripts\activate
pip install -r requirements.txt
make smoke            # checa imports/versões
make data-subset      # baixa subset local (WAV + meta.csv)
make notebooks        # abre Jupyter
