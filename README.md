# Modelagem Preditiva de Sucesso de Filmes
Este projeto tem como objetivo construir um modelo de Machine Learning capaz de **prever o lucro financeiro de filmes** com base em seus metadados.  
A variável-alvo utilizada é o **profit** (lucro), definido como:

\[
profit = revenue - budget
\]

A previsão desse valor pode apoiar **estúdios, produtoras e investidores** em decisões estratégicas sobre planejamento e avaliação financeira de produções cinematográficas.

---

## Integrantes do Projeto
- **Integrante 1:** Henrique Andrade
- **Integrante 2:** João Pedro Espanhol

---

## Estrutura do Projeto



Projeto-ML/
<br>
│
<br>
├── ProjetoAM_Parte2.ipynb   # Notebook completo com análise e modelagem
<br>
├── movies_metadata.csv      # Dataset utilizado
<br>
└── README.md                # Este documento



---

## Tecnologias Utilizadas

### **Linguagem**
- Python 3.10+

### **Bibliotecas Principais**
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scikit-learn`
- `xgboost`
- `ast`
- `warnings`

### **Modelos de Machine Learning**
- Dummy Regressor (baseline)
- Regressão Linear
- Random Forest Regressor
- XGBoost Regressor

---

## 1. Preparação e Limpeza dos Dados

O dataset utilizado é o **MovieLens + TMDB Metadata**, com cerca de **45 mil filmes**.  
As etapas principais de preparação incluem:

- Conversão de colunas numéricas (budget, revenue, runtime, etc.)
- Filtragem de filmes com valores válidos de orçamento e receita
- Criação da variável-alvo **profit**
- Conversão de colunas JSON (genres, companies, production_countries)
- Criação de listas estruturadas com `ast.literal_eval`
- Seleção de features categóricas:
  - **Top 20 gêneros**
  - **Top 10 países**
  - **Top 50 produtoras**
- Codificação com `MultiLabelBinarizer`
- Criação da feature **weighted_rating** baseada em IMDB/WR formula

---

## 2. Modelagem

Três modelos foram treinados e comparados:

### **2.1 Modelos Avaliados**
| Modelo | Descrição |
|-------|-----------|
| Dummy Regressor | Modelo de referência (baseline) |
| Regressão Linear | Modelo linear simples |
| Random Forest | Ensemble baseado em árvores |
| XGBoost | Gradient Boosting (melhor desempenho) |

### **2.2 Pipeline**
Um `Pipeline` inclui:
- Normalização de variáveis numéricas com `StandardScaler`
- Features categóricas mantidas como binárias (one-hot)
- Treinamento automático do modelo escolhido

---

## 3. Resultados Principais

### **Desempenho dos Modelos (Teste)**

| Modelo | R² | RMSE |
|-------|-----------|----------------|
| Dummy Regressor | -0.0002 | 140,081,573 |
| Regressão Linear | 0.4767 | 101,323,184 |
| Random Forest | 0.6174 | 86,636,604 |
| **XGBoost (melhor)** | **0.6268** | **85,573,444** |

➡ **O XGBoost teve o melhor desempenho geral**, explicando ~62% da variabilidade do lucro.

---

## 4. Otimização do Modelo

O **Random Forest** foi otimizado usando Grid Search + Cross-Validation (5-fold).

### **Parâmetros Otimizados**
```json
{
  "max_depth": 20,
  "n_estimators": 100
}
````

### **Desempenho após otimização**

* **R²:** 0.6114
* **RMSE:** 87,314,244
* **MAE:** 47,760,407

---

## 5. Principais Insights

### **Features mais importantes**

1. **budget** (orçamento)
2. **popularity**
3. **weighted_rating**
4. Certos gêneros e países aparecem como moderadamente relevantes
5. Empresas de produção têm efeito menor, mas consistente

### **Conclusões**

* Investimentos maiores tendem a gerar lucros maiores.
* Filmes mais populares pré-lançamento têm melhor desempenho.
* A nota ponderada melhora a capacidade preditiva.
* Modelos baseados em árvores são os mais eficazes nesta tarefa.

### **Limitações**

* Difícil prever lucro sem considerar:

  * Marketing
  * Competição de lançamentos
  * Fatores culturais
  * Hype de franquias
  * Avaliações da crítica especializada
* RMSE e MAE ainda são altos devido à grande variação natural dos lucros.

---

## **Como Executar o Projeto**

### **Pré-requisitos**

Antes de tudo, instale as dependências:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost
```

### **Execução**

1. Baixe o repositório

```bash
git clone https://github.com/Angelo-Andrade/Projeto-de-Introdu-o-a-Aprendizado-de-M-quina/
```

Depois descompacte a pasta do dataset e a mantenha no mesmo diretório que o notebook.

2. Abra o notebook:

```bash
jupyter notebook ProjetoAM_Parte2.ipynb
```

3. Execute todas as células na ordem, pulando a etapa de download de dados (segundo código no tópico 1.7).

### **Dataset**

O arquivo `movies_metadata.csv` deve estar na mesma pasta do notebook.
Caso não esteja, ajuste o caminho na célula de leitura.

---

## Status do Projeto

Concluído

### Possíveis melhoras futuras:

* Adição de NLP com palavras-chave
* Inclusão de dados externos (marketing, calendário de lançamentos)
* Redes neurais para modelos mais complexos

---
