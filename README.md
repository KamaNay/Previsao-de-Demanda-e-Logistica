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
3. **Machine Learning:** Treinamento de um modelo `Random Forest Classifier` com split sem 
   vazamento de dados (agrupado por pedido) e calibração de probabilidade (isotonic regression), 
   garantindo que o score gerado reflita a taxa real de atraso observada.
4. **Business Intelligence:** Desenvolvimento de um Dashboard no `Power BI` com estética *Dark/High-Tech* para monitoramento e tomada de decisão em tempo real.

---

## 📊 A Vitrine Executiva (Dashboard)
O painel foi desenhado para ser uma ferramenta de ação. Ele destaca o Faturamento em Risco e aponta no mapa as malhas logísticas estranguladas.

![Demonstração do Dashboard](./assets/dashboard_logistica.gif)

---

## 🧠 O Cérebro: O Modelo Preditivo
Para o algoritmo de Machine Learning, a prioridade da operação logística foi traduzida em matemática.

* **Algoritmo:** Random Forest Classifier, com probabilidades calibradas via Isotonic Regression.
* **Lidando com o Desbalanceamento:** Na vida real, a maioria das entregas chega no prazo. O 
  parâmetro `class_weight='balanced'` foi utilizado para penalizar os erros da classe minoritária 
  (atrasos), forçando o modelo a não deixar os problemas passarem despercebidos.
* **Threshold Ajustável:** Em vez de fixar a decisão em um ponto de corte único, o pipeline calcula 
  o threshold ótimo (maximizando F1) sobre as probabilidades calibradas, e expõe esse valor como 
  parâmetro de negócio — cortes mais baixos priorizam capturar mais atrasos (maior recall, mais 
  falsos alarmes); cortes mais altos priorizam confiabilidade do alerta (maior precisão, menos volume 
  sinalizado). A escolha fica a critério do time de operação, não do cientista de dados.

## 📝 Análise de Resultados e Visão de Negócios

1. **Os Ofensores do SLA (Causa Raiz):** O fator dominante é a 
   **sazonalidade** — o mês da compra concentra 35% da importância no modelo preditivo, 
   evidenciando picos de risco em períodos como Carnaval e Black Friday, quando o volume de 
   pedidos pressiona a capacidade operacional.

2. **Zonas Vermelhas da Malha:** A análise regional revelou que pedidos com destino a AL, MA, SE, 
   CE e PI têm taxa de atraso de até 3,2x a média nacional (6,6%). A rota SP → RJ merece atenção 
   especial: é a única rota de alto volume (9,4 mil pedidos, R$ 1,26 milhão) que também apresenta 
   risco elevado (13,5%), diferente de outras rotas de grande volume como SP → SP e SP → MG, 
   que ficam abaixo de 5%.

3. **A Estratégia do Modelo:** O `RandomForestClassifier` foi treinado com `class_weight='balanced'` 
   e teve suas probabilidades calibradas (isotonic regression) para refletir taxas reais de atraso — 
   o score médio do modelo bate com a taxa real observada (6,6%). O threshold de decisão é 
   ajustável de acordo com o apetite de risco da operação: cortes mais baixos (~12%) maximizam a 
   detecção de atrasos (recall ~41%); cortes mais altos priorizam precisão, reduzindo falsos alarmes.

4. **Impacto Financeiro Consolidado:** Com o threshold calibrado em uso, o dashboard aponta 
   R$ 1,5 a 2,4 milhões em faturamento operando em alto risco — entre 9,5% e 14,4% da receita total, 
   dependendo do corte de sensibilidade escolhido pelo time.

## 📂 Estrutura do Repositório

```text
├── assets/
│   └── dashboard_logistica.gif
├── data/
│   ├── processed/
│   │   ├── base_logistica_enriquecida.csv     # Base unificada (usada na EDA e no treino)
│   │   └── base_para_powerbi.csv              # Base final com risco calibrado
│   └── raw/                                   # Dados brutos da Olist (ignorados no git)
├── notebooks/
│   ├── 01_preparacao_dados.ipynb              # JOINs e Engenharia de Features
│   ├── 02_treinamento_ml.ipynb                # Treinamento, calibração e exportação
│   ├── 02_treinamento_ml_v2.ipynb             # Treinamento, calibração e exportação
│   ├── 02_treinamento_ml_v3.ipynb             # Treinamento, calibração e exportação
│   └── 03_analise_exploratoria.ipynb          # EDA e mapa de correlação
├── dashboard/
│   └── torre_controle_logistica.pbix
├── .gitignore                             # Ignora ambientes virtuais (.venv) e arquivos pesados
├── README.md                              # Documentação principal do projeto
└── requirements.txt                       # Dependências e bibliotecas Python utilizadas