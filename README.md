# Sistema de Detecção de Armas Brancas em Tempo Real (YOLOv11)

[![Powered by YOLOv11](https://img.shields.io/badge/Model-YOLOv11s-blue)](https://github.com/ultralytics/ultralytics)
[![Python](https://img.shields.io/badge/Python-3.10%2B-yellow)](https://www.python.org/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](LINK_DO_SEU_NOTEBOOK_AQUI)

**Status:** Versão 1.0 (Estável)

## Visão Geral
Este projeto apresenta um sistema de Visão Computacional desenvolvido para a detecção de armas brancas (facas) em vídeo. Utilizando a arquitetura **YOLOv11s (Small)**, o sistema processa frames capturados via webcam diretamente no navegador (Google Colab), aplicando um pipeline de pós-processamento para padronização de alertas.

O foco do projeto foi criar uma solução **Cloud-Native** que permite inferência acelerada por GPU (Tesla T4) sem necessidade de instalação local complexa, utilizando uma ponte JavaScript-Python para captura de vídeo.

### Destaques Técnicos
* **Unificação de Taxonomia:** Implementação de lógica de pós-processamento que intercepta as detecções do modelo e unifica múltiplas classes de treinamento (ex: `knife`, `kitchen-knife`) em uma única classe alerta: **"Faca"**.
* **Filtragem de Ruído:** Definição de limiar de confiança (`conf > 0.40`) ajustado empiricamente para eliminar falsos positivos comuns em ambientes domésticos.
* **Inferência Híbrida:** Pipeline customizado que integra o kernel Python do Colab com a API de mídia do navegador, permitindo processamento de vídeo em tempo real na nuvem.

---

## Demonstração
*(Insira aqui o GIF ou vídeo `demo_preview.gif`)*

---

## Especificações Técnicas
* **Modelo:** YOLOv11s (Fine-Tuning com pesos `best.pt`).
* **Hardware:** NVIDIA Tesla T4 (16GB VRAM).
* **Stack:**
    * `ultralytics`: Motor de inferência YOLO.
    * `opencv-python`: Manipulação de arrays de imagem.
    * `IPython.display` & `JavaScript`: Interface de captura de vídeo web.

---

## Instruções de Execução (Google Colab)

Este projeto foi desenhado para ser executado inteiramente na nuvem.

1. **Acesso:** Clique no botão **"Open in Colab"** no topo deste documento.
2. **Setup:**
    * Certifique-se de que o arquivo de pesos `best.pt` foi carregado na raiz do ambiente ou na pasta correta.
    * No menu do Colab, verifique se o **Ambiente de Execução** está configurado para **GPU**.
3. **Execução:**
    * Rode as células de instalação de dependências.
    * Execute a célula **"Webcam Stream"**.
    * O navegador solicitará permissão para usar sua câmera.

---

## Estrutura do Repositório
```text
├── models/
│   └── best.pt               # Pesos do modelo treinado
├── notebooks/
│   └── treino_yolo.ipynb     # Notebook contendo o código de treino e a inferência web
├── assets/                   # Imagens de validação e matriz de confusão
└── README.md                 # Documentação do projeto