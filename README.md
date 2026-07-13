# 🔮 Torre de Controle Logístico: Previsão de Atrasos com Machine Learning

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit_Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

## 📌 O Problema de Negócio
Em operações de Supply Chain e e-commerce de grande escala, a quebra de SLA (atraso na entrega) gera gargalos no SAC, perda de clientes e altos custos com logística reversa. 

Este projeto foi desenvolvido para atuar proativamente nesse cenário, ideal para o ritmo intenso de grandes centros de distribuição e varejistas. O objetivo é responder à pergunta: **"Como prever se uma mercadoria vai atrasar ANTES mesmo de ela ser despachada?"**

## 🏗️ Arquitetura da Solução
O projeto é um pipeline *End-to-End*, que vai desde a extração de dados brutos relacionais até a entrega de um painel executivo interativo.

1. **Extração e Modelagem (Data Prep):** Utilização da base real e pública da Olist (Kaggle). Cruzamento de múltiplas tabelas (Pedidos, Itens, Clientes, Produtos) via `Pandas` para criar uma Tabela Fato unificada.
2. **Feature Engineering:** Criação de variáveis fundamentais para a malha logística, como **Volume Cúbico da Carga**, **Rotas Interestaduais** e **Valor Financeiro em Risco**.
3. **Machine Learning:** Treinamento de um modelo `Random Forest Classifier` para calcular a probabilidade de atraso de cada pedido.
4. **Business Intelligence:** Desenvolvimento de um Dashboard no `Power BI` com estética *Dark/High-Tech* para monitoramento e tomada de decisão em tempo real.

---

## 📊 A Vitrine Executiva (Dashboard)
O painel foi desenhado para ser uma ferramenta de ação. Ele destaca o Faturamento em Risco e aponta no mapa as malhas logísticas estranguladas.

![Demonstração do Dashboard](link_para_o_seu_gif_ou_print_aqui.gif)

---

## 🧠 O Cérebro: O Modelo Preditivo
Para o algoritmo de Machine Learning, a prioridade da operação logística foi traduzida em matemática.

* **Algoritmo:** Random Forest Classifier.
* **Lidando com o Desbalanceamento:** Na vida real, a maioria das entregas chega no prazo. O parâmetro `class_weight='balanced'` foi utilizado para penalizar os erros da classe minoritária (atrasos), forçando o modelo a ser "paranoico" e não deixar os problemas passarem despercebidos.
* **Métrica de Foco:** Priorizou-se o **Recall (Sensibilidade)** da classe de atrasos. No contexto de negócios, é muito mais barato investigar um "falso positivo" (pacote que o modelo achou que ia atrasar, mas chegou no prazo) do que sofrer com um "falso negativo" (pacote que quebrou o SLA sem nenhum aviso prévio à transportadora).

## 📂 Estrutura do Repositório

```text
├── data/
│   ├── raw/                   # Dados brutos da Olist (ignorados no git)
│   └── processed/             # Base unificada e escorada com as previsões da IA
├── notebooks/
│   ├── 01_preparacao_dados.ipynb  # JOINs e Engenharia de Features
│   └── 02_treinamento_ml.ipynb    # Treinamento do Random Forest e exportação
├── dashboard/
│   └── torre_controle_logistica.pbix  # Arquivo do Power BI
└── README.md