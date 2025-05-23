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
  ![Acuracia](https://github.com/user-attachments/assets/04f0d08e-b384-4382-8924-fc3d814582b6)
  ![Precisao](https://github.com/user-attachments/assets/18d80afb-60ce-4738-b7e1-7b6e32c4c60b)
  ![Recall](https://github.com/user-attachments/assets/e0f0022a-fa0a-4995-bf7b-f19cd7eaad21)
  ![Especificidade](https://github.com/user-attachments/assets/42f12be6-2a70-4edd-89e2-dfd81f819907)
  ![ROC](https://github.com/user-attachments/assets/9e99cda0-2ab2-40e8-acc7-8e4fd3e5ab53)

## 📌 Conclusões  
  Este projeto de estatística aplicada teve como objetivo principal desenvolver modelos de Machine Learning capazes de prever o status de infecção por AIDS a partir de dados de pacientes. Através de um pipeline metodológico robusto, que incluiu a análise exploratória de dados, tratamento de features categóricas e numéricas, seleção de features via RFE e uma validação cruzada estratificada em 10 folds, conseguimos avaliar o desempenho de diversos algoritmos de classificação.

  Os resultados demonstraram que modelos baseados em ensembles e boosting, como o GradientBoostingClassifier (AUC = 0.70), LightGBMClassifier (AUC = 0.68), RandomForestClassifier (AUC = 0.66) e XGBoostClassifier (AUC = 0.65), foram os que apresentaram o melhor poder discriminatório. Eles superaram significativamente os classificadores mais simples e o desempenho de um classificador aleatório (AUC = 0.50), indicando uma capacidade razoável de distinguir entre pacientes infectados e não infectados. Por outro lado, modelos como a Árvore de Decisão padrão (AUC = 0.55) e o SVC com kernel linear (AUC = 0.50) mostraram desempenho limitado, sugerindo que a complexidade da relação entre as features e o status de infecção não é linear ou não é bem capturada por abordagens mais simplistas.

  O sucesso na identificação de modelos com bom poder preditivo, mesmo em um cenário de classes desbalanceadas, valida a importância da abordagem de pré-processamento adotada e da utilização de técnicas como class_weight e scale_pos_weight. Este estudo demonstra a viabilidade de utilizar dados clínicos e demográficos para auxiliar na classificação de pacientes com AIDS, o que pode ter implicações valiosas em pesquisas futuras e na tomada de decisões em saúde pública.

## ⚠️ Limitações e Trabalhos Futuros  
  Embora o projeto tenha alcançado modelos com bom poder preditivo para a classificação de AIDS, algumas limitações e direções para trabalhos futuros podem ser exploradas:

- Ajuste Fino de Hiperparâmetros: Ir além da busca básica, utilizando técnicas como Grid Search ou Randomized Search com espaços de parâmetros mais refinados, ou otimização bayesiana, para extrair o desempenho máximo dos modelos mais promissores (Gradient Boosting, LightGBM, Random Forest, XGBoost).
- Exploração de Técnicas Avançadas de Balanceamento de Classes: Além de class_weight, investigar a aplicação de métodos de reamostragem como SMOTE (Synthetic Minority Over-sampling Technique) ou ADASYN no conjunto de treinamento de cada fold. Isso pode ajudar a melhorar ainda mais o Recall para a classe minoritária, sem comprometer significativamente a Precisão ou Especificidade.
- Análise de Erros Aprofundada e Otimização de Limiares: Realizar uma análise mais detalhada dos Falsos Positivos e Falsos Negativos na matriz de confusão para os melhores modelos. Isso pode levar à otimização do limiar de classificação (decision threshold) para atender a necessidades específicas do domínio médico, onde o custo de um Falso Negativo (não identificar um paciente infectado) pode ser muito maior do que o de um Falso Positivo.
- Engenharia de Features: Explorar a criação de novas features a partir das existentes (ex: proporções de CD4/CD8, variações ao longo do tempo se mais dados longitudinais estivessem disponíveis). Isso pode capturar relações não lineares e complexas que os modelos atuais podem não estar aproveitando ao máximo.
