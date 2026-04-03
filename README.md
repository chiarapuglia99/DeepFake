# 🛡️ DeepFake Detection attraverso l'utilizzo del modello CLIP

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-ee4c2c.svg)](https://pytorch.org/)
[![CLIP](https://img.shields.io/badge/Model-CLIP-lightgrey.svg)](https://github.com/openai/CLIP)

## 📝 Descrizione del Progetto
L'obiettivo della ricerca è lo sviluppo di un sistema di classificazione binaria per distinguere immagini reali da immagini sintetiche (Deepfake)[cite: 13, 40]. Il cuore del sistema è il modello **CLIP (Contrastive Language-Image Pretraining)**, utilizzato come estrattore di feature visive e testuali.

## 🔬 Metodologia e Scelte Progettuali
Il sistema sfrutta un'architettura basata su **Triplet Loss** per mappare le immagini in uno spazio latente dove:
* **Anchor**: Immagini reali.
* **Positive**: Immagini simili alle reali.
* **Negative**: Immagini fake.

[cite_start]Il modello mira a minimizzare la distanza tra anchor e positive, massimizzando contemporaneamente quella tra anchor e negative.

### ⚙️ Configurazione
* **Modello Visione**: Transformer $Vit-B/32$ (per sola immagine) e $Vit-B/16$ (per approccio multimodale).
* **Pre-processing**: Ridimensionamento a $200\times200$ pixel, denormalizzazione e normalizzazione specifica CLIP.
* **Embedding**: Riduzione della dimensionalità da 512 a 128.
* **Classificatore**: Support Vector Machine (SVM) con suddivisione 70% Training, 10% Validation, 20% Test.

---

## 📊 Dataset
Il dataset analizzato comprende un totale di 2.496.738 immagini generate tramite 25 diversi algoritmi (GAN, Diffusion Models, etc.). Per l'addestramento sono stati utilizzati subset bilanciati:
* **Cycle-GAN**: 7.605 reali / 7.605 fake.
* **Pro-GAN**: 20.000 reali / 20.000 fake.

![Bilanciamento Dataset](./grafico_bilanciamento.png)

---

## 📈 Risultati
L'efficacia è stata testata su tre diverse configurazioni.

### 1. Estrazione Sola Immagine
| Dataset | Accuracy (Test) | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- | :--- |
| **Cycle-GAN** | 94.0%  | 94.0% | 94.0% | 94.0% |
| **Pro-GAN** | 91.85% | 91.85% | 91.85% | 91.85% |

### 2. Immagine + Testo (Somma degli Embedding)
Risultati ottenuti fondendo le feature visive con la categoria testuale.
* **Dataset Combinato Accuracy**: 91.25%.

### 3. Immagine + Testo (Prodotto degli Embedding)
Risultati ottenuti tramite prodotto elemento per elemento per cogliere l'interazione diretta.
* **Dataset Combinato Accuracy**: 90.57%.

---

## 🚀 Conclusioni
Entrambi gli approcci hanno dimostrato ottime capacità di generalizzazione. L'analisi tramite **PCA** conferma che gli embedding estratti da CLIP, uniti alla regolarizzazione della Triplet Loss, creano cluster ben definiti per la separazione tra reale e sintetico.

## 👥 Autori
* **Chiara Puglia**: Master's Degree Student in Computer Science, curriculum Data Science and Machine Learning at University of Salerno.
* **Luca Giuliano**: Master's Degree Student in Computer Science, curriculum Data Science and Machine Learning at University of Salerno.

---

## 📚 Riferimenti
* [1] Dataset DeepFake.
* [2] De Rosa et al., "Exploring the Adversarial Robustness of CLIP for AI-generated Image Detection" (WIFS 2024).
* [3] Ojha et al., (CVPR 2023).
