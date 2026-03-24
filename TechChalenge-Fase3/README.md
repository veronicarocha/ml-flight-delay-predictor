# Tech Challenge - Análise e Previsão de Atrasos de Voos

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

## Sobre o Projeto

Este projeto foi desenvolvido como parte do **Tech Challenge** fase 3 na FIAP, 
aplicando técnicas de **Machine Learning supervisionado e não supervisionado** 
para análise e previsão de atrasos de voos nos EUA em 2015.

**Dataset:** Base de dados pública de voos nos EUA (2015)  
**Autor:** Veronica Rocha  
**Data:** 24/Março/2026

---

## Objetivos do Tech Challenge

| Requisito | Status | Como foi atendido |
|-----------|--------|-------------------|
| **EDA com estatísticas descritivas** | ✅ | `describe()` e análise de distribuições |
| **Visualizações com insights** | ✅ |  gráficos: barras, linhas, mapas de calor |
| **Tratamento de valores ausentes** | ✅ | Remoção e imputação baseada em percentual |
| **Modelagem supervisionada** | ✅ | 3 algoritmos (RF, XGB, LGBM) comparados |
| **Comparação de algoritmos** | ✅ | Random Forest vs XGBoost vs LightGBM |
| **Modelagem não supervisionada** | ✅ | KMeans em voos e aeroportos + PCA |
| **Clusterização em gráficos** | ✅ | PCA visual, gráficos de cotovelo |
| **Apresentação crítica** | ✅ | Conclusões, limitações e próximos passos |

---

## Perguntas Respondidas pela Análise

| Pergunta | Resposta |
|----------|----------|
| **Quais aeroportos são mais críticos?** | Aeroportos de longa distância (Cluster 2) com 50.5% de atraso; aeroportos não mapeados com 100% de atraso (poucos voos) |
| **Que características aumentam a chance de atraso?** | Horário noturno (59.5%), longa distância (50.5%), finais de semana (48.6%) |
| **Atrasos são mais comuns em certos horários?** | Sim! Noturno (17:24) tem 59.5% vs matinal (10:00) com 41.6% - diferença de 18% |
| **É possível agrupar aeroportos?** | Sim! 3 perfis: curta distância matinal (35.9%), curta/média (45.5%), longa distância (50.5%) |
| **Até que ponto conseguimos prever atrasos?** | XGBoost com F1-score 0.6549 e AUC-ROC 0.7131  |

# Estrutura do Projeto

ML-FLIGHT-DELAY-PREDICTOR
TechChallenge-Fase3/<br>
├── airlines.csv # Dados das companhias aéreas<br>
├── airports.csv # Dados dos aeroportos<br>
├── flights.csv # Base de voos<br>
├── requirements.txt # Dependências do projeto<br>
├── tech_challenge_fiap_fase3_V7.ipynb # ML<br>
├── README.md # Este arquivo<br>


## Como Executar o Projeto Localmente

### 1️ Pré-requisitos

- Python 3.8 ou superior
- Git
- 8GB+ de RAM (recomendado)
- 5GB de espaço em disco

### 2️ Clonar o Repositório

```bash
git clone https://github.com/seu-usuario/tech-challenge-voos.git
cd tech-challenge-voos
```
### 3️ Criar e Ativar Ambiente Virtual

Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

Linux/Mac:

```bash
python3 -m venv venv
source venv/bin/activate
```

### 4️ Instalar Dependências

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

requirements.txt
```
pandas>=2.0.3
numpy>=1.24.3
matplotlib>=3.7.2
seaborn>=0.12.2
scikit-learn>=1.3.0
xgboost>=1.7.6
lightgbm>=4.6.0
category_encoders>=2.6.3
jupyter>=1.0.0
```

### 5️ Baixar os Dados

..no projeto

### 6️ Executar o Notebook
```bash
jupyter notebook notebooks/tech_challenge_voos.ipynb
```
Ou, se preferir executar como script Python:

```bash
python notebooks/tech_challenge_voos.py
```

### 7️ Instalar Plugin do Jupyter (Opcional)

Para melhor experiência no VS Code:

```bash
code --install-extension ms-toolsai.jupyter
```

Para extensões de visualização de dados:

```bash
code --install-extension ms-toolsai.datawrangler
```
# Principais Resultados

## Modelagem Supervisionada (Classificação)

| Modelo | Acurácia | Precisão | Recall | F1-score | AUC-ROC |
|--------|----------|----------|--------|----------|---------|
| Random Forest | 0.6307 | 0.6195 | 0.6777 | 0.6473 | 0.6826 |
| **XGBoost** | **0.6532** | **0.6516** | **0.6583** | **0.6549** | **0.7131** |
| LightGBM | 0.6476 | 0.6440 | 0.6601 | 0.6520 | 0.7048 |

**✅ Melhor modelo:** XGBoost  
- F1-score: **0.6549**  
- AUC-ROC: **0.7131**  
- Validação cruzada (5-fold): F1-score médio = **0.6621** (+/- 0.0035)

---

# Clusterização (Não Supervisionada)

### Clusters de Voos:

| Cluster | Perfil | Hora | Taxa Atraso |
|---------|--------|------|-------------|
| 0 | Noturno/Tarde | 17:24 | 59.5% (pior) |
| 1 | Matinal | 10:00 | 41.6% (melhor) |
| 2 | Fim de Semana | 13:36 | 48.6% (intermediário) |

### Clusters de Aeroportos:

| Cluster | Perfil | Distância | Hora | Taxa Atraso |
|---------|--------|-----------|------|-------------|
| 0 | Curta/Média | 424 mi | 13:12 | 45.5% |
| 1 | Curta - Manhã | 401 mi | 9:36 | 35.9% (melhor) |
| 2 | Longa Distância | 1.083 mi | 13:36 | 50.5% (pior) |


# Tecnologias Utilizadas
| Tecnologia | Versão | Uso |
|------------|--------|-----|
| Python | 3.11 | Linguagem principal |
| Pandas | 2.0.3 | Manipulação de dados |
| NumPy | 1.24.3 | Operações numéricas |
| Scikit-learn | 1.3.0 | Modelagem ML |
| XGBoost | 1.7.6 | Modelo supervisionado |
| LightGBM | 4.6.0 | Modelo supervisionado |
| Matplotlib | 3.7.2 | Visualizações |
| Seaborn | 0.12.2 | Visualizações estatísticas |
| Category Encoders | 2.6.3 | Target encoding |