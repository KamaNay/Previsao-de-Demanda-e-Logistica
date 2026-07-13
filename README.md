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

![Demonstração do Dashboard](./assets/dashboard_logistica.gif)

---

## 🧠 O Cérebro: O Modelo Preditivo
Para o algoritmo de Machine Learning, a prioridade da operação logística foi traduzida em matemática.

* **Algoritmo:** Random Forest Classifier.
* **Lidando com o Desbalanceamento:** Na vida real, a maioria das entregas chega no prazo. O parâmetro `class_weight='balanced'` foi utilizado para penalizar os erros da classe minoritária (atrasos), forçando o modelo a ser "paranoico" e não deixar os problemas passarem despercebidos.
* **Métrica de Foco:** Priorizou-se o **Recall (Sensibilidade)** da classe de atrasos. No contexto de negócios, é muito mais barato investigar um "falso positivo" (pacote que o modelo achou que ia atrasar, mas chegou no prazo) do que sofrer com um "falso negativo" (pacote que quebrou o SLA sem nenhum aviso prévio à transportadora).

## 📝 Análise de Resultados e Visão de Negócios

A Torre de Controle não é apenas um painel visual; ela é o resultado final de um pipeline analítico rigoroso, validado estatisticamente e focado no Supply Chain corporativo.

A Análise Exploratória de Dados (EDA) e o treinamento do modelo preditivo revelaram insights fundamentais sobre a operação da Olist:

1. **Os Ofensores do SLA (Causa Raiz):** Através de um Mapa de Calor de correlação estatística, identificamos que a variável física [Peso da Carga ou Volume Cúbico] possui a maior correlação linear com a quebra de SLA. Isso prova matematicamente que o gargalo operacional ocorre no transporte de mercadorias [ex: de linha branca/pesadas], exigindo transportadoras com maior capilaridade e robustez para esses modais.

2. **Zonas Vermelhas da Malha:** A análise regional revelou que as rotas com destino aos estados de [ex: AL, RR, AM] possuem taxas de atraso até [ex: 3x] superiores à média nacional. O Power BI automatiza o monitoramento dessas rotas interestaduais interestaduais (SP -> Nordeste).

3. **A Estratégia do Modelo (Recall de 53%):** Optamos por treinar o modelo `Random Forest Classifier` focando agressivamente na penalização dos erros da classe de atrasos. Isso resultou em um Recall de 53%, interceptando proativamente mais da metade dos problemas reais. No contexto logístico corporativo, priorizamos o alarme falso ( investigation ) em vez do falso negativo ( SAC comprometido e custos com reembolsos ).

4. **Impacto Financeiro Consolidado:** O Power BI consolida o pipeline de Machine Learning ao cruzar a probabilidade predita com a coluna de Valor Total do Pedido, apontando diretamente para os R$ 634 Mil de faturamento operando em Alto Risco (probabilidade >= 70%).

Essa abordagem orientada por dados permite que o gestor de Supply Chain atue preventivamente, mudando transportadoras, acionando o SAC antes do cliente reclamar ou renegociando SLAs nas rotas críticas, transformando uma Torre de Observação em uma ferramenta de ação direta.

## 📂 Estrutura do Repositório

```text
├── assets/
│   └── dashboard_logistica.gif            # GIF de demonstração do painel
├── data/
│   ├── processed/                         # Base unificada e com previsões da IA
│   └── raw/                               # Dados brutos da Olist (ignorados no git)
├── notebooks/
│   ├── 01_preparacao_dados.ipynb  # JOINs e Engenharia de Features
│   └── 02_treinamento_ml.ipynb    # Treinamento do Random Forest e exportação
├── dashboard/
│   └── torre_controle_logistica.pbix  # Arquivo do Power BI
└── README.md