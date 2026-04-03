# DeepFake Detection attraverso l'utilizzo del modello CLIP

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-ee4c2c.svg)](https://pytorch.org/)
[![CLIP](https://img.shields.io/badge/Model-CLIP-lightgrey.svg)](https://github.com/openai/CLIP)

[cite_start]Repository ufficiale del progetto per l'esame di **Fondamenti di Visione Artificiale e Biometria** presso l'Università degli Studi di Salerno (a.a. 2024/2025)[cite: 4, 9, 10].

## Descrizione del Progetto
[cite_start]L'obiettivo della ricerca è lo sviluppo di un sistema di classificazione binaria per distinguere immagini reali da immagini sintetiche (Deepfake)[cite: 13, 40]. [cite_start]Il cuore del sistema è il modello **CLIP (Contrastive Language-Image Pretraining)**, utilizzato come estrattore di feature visive e testuali[cite: 21, 96].

## Metodologia e Scelte Progettuali
[cite_start]Il sistema sfrutta un'architettura basata su **Triplet Loss** per mappare le immagini in uno spazio latente dove[cite: 112]:
* [cite_start]**Anchor**: Immagini reali[cite: 111].
* [cite_start]**Positive**: Immagini simili alle reali[cite: 111, 112].
* [cite_start]**Negative**: Immagini fake[cite: 111, 112].

[cite_start]Il modello mira a minimizzare la distanza tra anchor e positive, massimizzando contemporaneamente quella tra anchor e negative[cite: 112].

### Configurazione
* [cite_start]**Modello Visione**: Transformer $Vit-B/32$ (per sola immagine) e $Vit-B/16$ (per approccio multimodale)[cite: 96, 463].
* [cite_start]**Pre-processing**: Ridimensionamento a $200\times200$ pixel, denormalizzazione e normalizzazione specifica CLIP[cite: 38, 106].
* [cite_start]**Embedding**: Riduzione della dimensionalità da 512 a 128[cite: 104].
* [cite_start]**Classificatore**: Support Vector Machine (SVM) con suddivisione 70% Training, 10% Validation, 20% Test[cite: 189, 378].

---

## 📊 Dataset
[cite_start]Il dataset analizzato comprende un totale di 2.496.738 immagini generate tramite 25 diversi algoritmi (GAN, Diffusion Models, etc.)[cite: 27, 28]. [cite_start]Per l'addestramento sono stati utilizzati subset bilanciati[cite: 76]:
* [cite_start]**Cycle-GAN**: 7.605 reali / 7.605 fake[cite: 93].
* [cite_start]**Pro-GAN**: 20.000 reali / 20.000 fake[cite: 93].

![Bilanciamento Dataset](./grafico_bilanciamento.png)

---

## 📈 Risultati
L'efficacia è stata testata su tre diverse configurazioni.

### 1. Estrazione Sola Immagine
| Dataset | Accuracy (Test) | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- | :--- |
| **Cycle-GAN** | [cite_start]94.0% [cite: 220] | [cite_start]94.0% [cite: 220] | [cite_start]94.0% [cite: 220] | [cite_start]94.0% [cite: 220] |
| **Pro-GAN** | [cite_start]91.85% [cite: 327] | [cite_start]91.85% [cite: 327] | [cite_start]91.85% [cite: 327] | [cite_start]91.85% [cite: 327] |

### 2. Immagine + Testo (Somma degli Embedding)
[cite_start]Risultati ottenuti fondendo le feature visive con la categoria testuale[cite: 467, 471].
* [cite_start]**Dataset Combinato Accuracy**: 91.25%[cite: 717].

### 3. Immagine + Testo (Prodotto degli Embedding)
[cite_start]Risultati ottenuti tramite prodotto elemento per elemento per cogliere l'interazione diretta[cite: 468, 719].
* [cite_start]**Dataset Combinato Accuracy**: 90.57%[cite: 953].

---

## 🚀 Conclusioni
[cite_start]Entrambi gli approcci hanno dimostrato ottime capacità di generalizzazione[cite: 956]. [cite_start]L'analisi tramite **PCA** conferma che gli embedding estratti da CLIP, uniti alla regolarizzazione della Triplet Loss, creano cluster ben definiti per la separazione tra reale e sintetico[cite: 441, 659].

## 👥 Autori
* [cite_start]**Chiara Puglia** Master's Degree Student in Computer Science, curriculum Data Science and Machine Learning [cite: 7]
* [cite_start]**Luca Giuliano** Master's Degree Student in Computer Science, curriculum Data Science and Machine Learning [cite: 8]

---

## 📚 Riferimenti
* [cite_start][1] Dataset DeepFake [cite: 960]
* [cite_start][2] De Rosa et al., "Exploring the Adversarial Robustness of CLIP for AI-generated Image Detection" (WIFS 2024) [cite: 962]
* [cite_start][3] Ojha et al., (CVPR 2023) [cite: 21]
