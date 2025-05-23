# Projeto de Estatística Aplicada

## 🧑‍💻 Autores  
- Ayrtton Lucas Silva (201921250007) - ayrtton.lucas@academico.ifpb.edu.br

## 🎯 Tema e Motivação  
Este projeto tem como tema a classificação de pacientes com AIDS, utilizando um conjunto de dados históricos que detalha estatísticas de saúde e informações categóricas sobre indivíduos diagnosticados. A motivação para esta escolha reside na importância crítica de compreender os fatores associados à infecção pelo vírus da AIDS, um desafio de saúde pública de relevância contínua, mesmo com os avanços da medicina.

Do ponto de vista estatístico e social, a análise deste dataset permite investigar padrões complexos e identificar variáveis preditivas que podem ser cruciais para o diagnóstico e a compreensão da progressão da doença. A capacidade de classificar com precisão o status de infecção a partir de dados clínicos e demográficos é de grande valor, podendo auxiliar em estudos epidemiológicos e na alocação de recursos de saúde.

## 📊 Conjunto de Dados Selecionado  
- Nome do conjunto de dados: AIDS Classification

- Fonte:  
  https://www.kaggle.com/datasets/aadarshvelu/aids-virus-infection-prediction?select=AIDS_Classification_15000.csv

- Descrição breve:  
  O conjunto de dados AIDS_Classification_15000.csv contém 15.000 entradas e 23 colunas, detalhando informações de pacientes diagnosticados com AIDS, originalmente publicado em 1996. Ele abrange uma variedade de atributos, incluindo dados demográficos (idade, peso, raça, gênero, atividade sexual), histórico médico (hemofilia, uso de drogas IV), histórico de tratamento (ZDV/não-ZDV), e resultados de exames laboratoriais (contagem de CD4/CD8). A variável alvo é infected, indicando se o paciente está infectado com AIDS (1=Sim, 0=Não).

- Justificativa para a escolha:  
  Este conjunto de dados foi escolhido por sua relevância no campo da saúde e por apresentar um problema clássico de classificação, que permite a aplicação de diversas técnicas estatísticas e de aprendizado de máquina. A riqueza de variáveis, tanto numéricas quanto categóricas, oferece um terreno fértil para análises exploratórias, identificação de correlações e construção de modelos preditivos. A análise pode ajudar a responder questões sobre quais fatores são mais influentes na determinação do status de infecção, contribuindo para uma melhor compreensão da doença e seus indicadores.

## ❓ Perguntas ou Hipóteses  
- Quais são as características demográficas (idade, peso, raça, gênero) dos pacientes no dataset e como elas se distribuem?

- Existe uma correlação entre o histórico de tratamento (trt, oprior, z30, preanti, str2, strat, treat, offtrt) e o status de infecção (infected)?

- Como os resultados dos exames laboratoriais (contagens de cd40, cd420, cd80, cd820) se relacionam com a infecção?

- É possível prever o status de infecção (infected) com alta acurácia utilizando as demais variáveis do dataset?

- Quais são as features mais importantes para a previsão do status de infecção, conforme identificado pelos modelos de Machine Learning?

- Os modelos de classificação conseguem lidar efetivamente com o desbalanceamento de classes na variável infected (aproximadamente 30.87% de casos infectados)?

## 🔍 Metodologia  
A metodologia empregada neste projeto segue as etapas padrão de um pipeline de Machine Learning para classificação, com foco na robustez e interpretabilidade dos resultados:

1. Carregamento e Pré-processamento de Dados:

  - O dataset AIDS_Classification_15000.csv é carregado utilizando a biblioteca Pandas.

  - As features são separadas da variável alvo (infected).

  - Identificação e tratamento de diferentes tipos de features:

  - Features Categóricas Nominais (trt, race, strat): Convertidas utilizando One-Hot Encoding (pd.get_dummies) para evitar a inferência de relações ordinais.

  - Features Numéricas Contínuas (time, age, wtkg, karnof, preanti, cd40, cd420, cd80, cd820): Normalizadas utilizando MinMaxScaler para escalar os valores entre 0 e 1.

  - Features Binárias (ex: hemo, homo, drugs): Mantidas em sua escala original (0 ou 1).

2. Seleção de Features:

  - A técnica de Recursive Feature Elimination (RFE) é aplicada, utilizando Regressão Logística como estimador, para selecionar as 8 features mais relevantes para a previsão do status de infecção.

3. Validação Cruzada:

  - O conjunto de dados é dividido em 10 folds utilizando StratifiedKFold. Esta técnica garante que a proporção das classes (infectado/não infectado) seja mantida em cada fold de treinamento e teste, o que é crucial dado o desbalanceamento da variável alvo.

4. Treinamento e Avaliação de Modelos:

  - Uma variedade de modelos de classificação é treinada e avaliada em cada um dos 10 folds:

    - Árvores de Decisão (Decision Tree Classifier)

    - Máquinas de Vetores de Suporte (SVC)

    - K-Nearest Neighbors (KNeighbors Classifier)

    - Bagging Classifier

    - Random Forest Classifier

    - Gradient Boosting Classifier

    - XGBoost Classifier

    - LightGBM Classifier

  - Para lidar com o desbalanceamento de classes, o parâmetro class_weight='balanced' é aplicado aos modelos que o suportam, e scale_pos_weight é ajustado para o XGBoost.

  - As métricas de desempenho coletadas para cada modelo e fold incluem: Acurácia, Precisão, Recall, Especificidade e Área Sob a Curva ROC (AUC).

5. Análise de Desempenho e Visualização:

  - As métricas de cada modelo são agregadas para calcular a média e o desvio padrão ao longo dos 10 folds, fornecendo uma avaliação robusta do desempenho geral.

  - Os modelos são ranqueados com base em sua Acurácia Média para identificar os 3 melhores.

  - Curvas ROC Combinadas: Para cada modelo, as probabilidades previstas e os rótulos verdadeiros de todos os folds são concatenados para gerar uma única curva ROC representativa e seu valor AUC correspondente. Essas curvas são plotadas em um único gráfico para comparação visual clara do poder discriminatório de cada modelo.

## 🛠️ Ferramentas Utilizadas  
O projeto é desenvolvido utilizando a linguagem de programação Python e as seguintes bibliotecas principais:

- pandas: Para manipulação e análise de dados (carregamento, pré-processamento, estruturação).

- numpy: Para operações numéricas eficientes, especialmente com arrays.

- scikit-learn: A biblioteca fundamental para Machine Learning, utilizada para pré-processamento (MinMaxScaler, RFE), divisão de dados (StratifiedKFold), e implementação de diversos algoritmos de classificação (LogisticRegression, DecisionTreeClassifier, SVC, KNeighborsClassifier, BaggingClassifier, RandomForestClassifier, GradientBoostingClassifier).

- xgboost: Para o algoritmo XGBoost Classifier.

- lightgbm: Para o algoritmo LightGBM Classifier.

- matplotlib: Para a criação de visualizações gráficas, como as Curvas ROC.

## 📈 Resultados  
*A preencher após as análises.*  
Resumo visual e interpretativo dos principais achados.

## 📌 Conclusões  
 Os modelos de boosting se mostraram os melhores para este dataset, sendo os mais promissores a se trabalhar com. É possível usar o GridSearchCV ou RandomizedSearchCV com parâmetros mais amplos ou refinados para melhorar o desempenho. Porém, devido ao tempo, o aumento pode ou não ser extremamente custoso, acabando por não valer a pena.

## ⚠️ Limitações e Trabalhos Futuros  
*A preencher no final do projeto.*  
Quais foram as limitações do estudo e o que poderia ser feito com mais tempo ou dados adicionais.

---

