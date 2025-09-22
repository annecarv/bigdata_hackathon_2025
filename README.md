# Hackathon Big Data 2025 – Forecast de Vendas  

Este projeto tem como objetivo prever a quantidade semanal de vendas por ponto de venda (PDV) e produto (SKU).  
A previsão abrange as cinco primeiras semanas de janeiro/2023, utilizando dados históricos de 2022.  

A solução combina:  
- Machine Learning → para análise exploratória e modelos baseline  
- Modelos de Séries Temporais (SARIMAX) → para previsões específicas de cada PDV x SKU  

---

## Como Executar  

### 1. Instalação das Dependências  
Clone o repositório e instale os pacotes:  

```bash
git clone https://github.com/seu-usuario/hackathon-bigdata-2025.git
cd hackathon-bigdata-2025
pip install -r requirements.txt
```
---

## Estrutura do Projeto  

### 1. Carregamento e Integração dos Dados  
- Histórico de vendas  
- Cadastro de produtos  
- Cadastro de pontos de venda (PDVs)  
- Integração em um dataset único para análises e modelagem  

### 2. Pré-processamento  
- Conversão de datas  
- Criação de variáveis temporais (ano, mês, semana, dia da semana)  
- Cálculo de diferenças de datas  
- Amostragem para otimização em datasets grandes  

### 3. Análise Exploratória (EDA)  
- Quantidade de valores únicos por coluna  
- Correlação entre variáveis numéricas (`quantity`, `gross_value`, `net_value`, etc.)  
- Visualização gráfica de padrões de vendas  

### 4. Engenharia de Features  
- Normalização de variáveis numéricas  
- One-hot encoding (categorias de baixa cardinalidade)  
- Codificação por frequência (categorias de alta cardinalidade)  

### 5. Modelagem com Machine Learning  
Algoritmos testados:  
- Decision Tree Regressor  
- Random Forest Regressor  
- MLP Regressor (Neural Network)  

Métricas utilizadas:  
- R²  
- RMSE  

### 6. Séries Temporais (SARIMAX)  
- Agregação semanal por PDV x SKU  
- Séries curtas → média histórica como fallback  
- Séries robustas → previsão via SARIMAX com sazonalidade anual  

### 7. Paralelização e Otimização  
- Execução em paralelo para milhares de séries temporais  
- Redução significativa do tempo de processamento  

### 8. Geração do Arquivo de Submissão  
- Colunas: `semana`, `pdv`, `produto`, `quantidade_prevista`  
- Ajuste de valores negativos → zero  
- Arquivo final pronto para submissão  

---

## Resultados Esperados  
- Previsões semanais de vendas por PDV e SKU  
- Identificação das variáveis mais relevantes  
- Suporte ao planejamento de estoque e vendas  

---

## Estrutura do Dataset  

Target:  
- `quantity` → Quantidade vendida  

Variáveis Numéricas:  
- `gross_value`, `net_value`, `gross_profit`, `discount`, `taxes`, `semana`  

Variáveis Categóricas:  
- `internal_store_id`, `internal_product_id`, `distributor_id`, `produto`, `categoria`,  
  `descricao`, `tipos`, `label`, `subcategoria`, `marca`, `fabricante`,  
  `pdv`, `premise`, `categoria_pdv`, `zipcode`  

Total: 6.560.698 registros | 24 variáveis  

---

## Análise Exploratória – Correlação com `quantity`  

| Variável       | Correlação |
|----------------|------------|
| `gross_value`  | 0.818      |
| `net_value`    | 0.819      |
| `discount`     | 0.532      |
| `gross_profit` | 0.221      |
| `taxes`        | 0.048      |

Observação: `gross_value` e `net_value` são as variáveis mais relevantes.  

---

## Tecnologias Utilizadas  

- Python 3.10+  
- Bibliotecas:  
  - pandas → manipulação de dados  
  - numpy → operações numéricas  
  - matplotlib, seaborn → visualização  
  - scikit-learn → Machine Learning  
  - statsmodels → SARIMAX  
  - joblib → paralelização  
  - pyarrow, fastparquet → suporte a Parquet  

---

## Referências  


NIELSEN, Aileen. *Análise prática de séries temporais: predição com estatística e aprendizado de máquina*.  
Tradução de Guilherme Henrique Marques Ribeiro. 1. ed. São Paulo: Novatec Editora, 2021.  


