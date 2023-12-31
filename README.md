# Monitor de Exercícios

#### Introdução
A escassez de enfoque nos programas de treino de força na literatura conexa e a ausência de apoio dos rastreadores de atividade atuais para exercícios com pesos livres representam desafios enfrentados por muitos entusiastas e profissionais de fitness. Com o crescente interesse em tecnologias e aplicativos de monitoramento de atividades, emerge um vasto potencial para o desenvolvimento de soluções que mitiguem essa lacuna. Além disso, a identificação de atividade pode ser aplicada para abordar desafios sociais substanciais, abrangendo reabilitação, sustentabilidade, cuidados geriátricos e saúde. Este projeto propõe explorar as potencialidades de aplicativos adaptados ao contexto no domínio do treino de força, empregando dados obtidos a partir de sensores de pulso (smartwatches) para analisar exercícios com pesos livres. O intento é forjar modelos que, à semelhança de treinadores pessoais, acompanhem os exercícios, contabilizem repetições, identifiquem movimentos e desvelando formas inapropriadas de execução, almejando auxiliar os usuários a concretizarem seus objetivos de maneira mais eficaz e segura.

#### Exercicios
![exercise examples](img/exercicios_basicos.png)



#### Objetivos
* Classificar os exercícios básicos com barra
* Contar o número de repetições
* Detectar forma inadequada do movimento

#### Instalação
Criar, instalar e ativar o ambiente  Anaconda: `conda env create -f environment.yml`.

---
### **Etapa 01 - Preparação dos Dados**
Ler todos os arquivos CSV brutos separados, processa-los e mesclá-los em um único conjunto de dados.
1. Conjunto de dados em → data/raw
2. Extrair recursos do nome do arquivo
3. Ler todos os arquivos
4. Trabalhar com datetimes
5. Criar uma função personalizada
6. Mesclar conjuntos de dados
7. Resample dos dados (conversão de frequência)
8. Exportar conjunto de dados processados

Códigos originais: [`make_dataset.py`](src/data/make_dataset.py)

Passo a passo explicado: [`01_make_dataset.ipynb`](notebooks/01_make_dataset.ipynb)

---
### **Etapa 02 - Exploratory Data Analysis (EDA)**
Criar scripts para processar, visualizar e modelar os dados de acelerômetro e giroscópio. 

1. Plotar as séries temporais de todos os exercícios
2. Plotar todos os eixos (x, y e z)
3. Comparar participantes
4. Criar um loop para plotar todas as combinações por sensor
5. Combinar os gráficos em uma única figura
6. Looping para todas as combinações e exportar para ambos os sensores

Códigos originais: [`visualize.py`](src/visualization/visualize.py)

Passo a passo explicado: [`02_visualize.ipynb`](notebooks/02_visualize.ipynb)

---
### **Etapa 03 - Lidando com Outliers**
Verificar se existem quaisquer valores atípicos (outliers) nos dados dados que desejamos remover.

1. Diagramas de caixa e amplitude interquartil (IQR)
2. Plotagem de valores atípicos ao longo do tempo
3. Função para marcar valores atípicos aplicando diversos métodps (IQR, Chauvenet e Fator de Valor Atípico Local)
4. Verificando outliers agrupados por rótulo
5. Substituindo outliers


Códigos originais: [`remove_outliers.py`](src/features/remove_outliers.py)

Passo a passo explicado: [`03_remove_outliers.ipynb`](notebooks/03_remove_outliers.ipynb)

---
### **Etapa 04 - Feature Engineering**
Filtrar ruidos e identificar partes dos dados que explicam a maior parte da variância utilizando PCA. Em seguida, adicionar recursos numéricos, temporais, de frequência e de agrupamento
para gerar novas features.


1. Lidando com valores ausentes
2. Filtro passa-baixa (Butterworth)
3. Aplicando PCA
4. Raiz quadrada da soma dos quadrados (vetor r)
5. Abstração temporal
6. Abstração da frequência
7. Lidando com "overlapping data" (overfitting)


Códigos originais: [`build_features.py`](src/features/build_features.py)

Passo a passo explicado: [`04_build_features.ipynb`](notebooks/04_build_features.ipynb)

---
### **Etapa 05 - Treinando o Modelo**
Realizar experimentos para a seleção das features, escolha do modelo e ajuste dos hiperparâmetros em busca da combinação que resulta na maior precisão para a classificação dos exercícios.


1. Criação do conjunto de treinamento e de teste
2. Divisão das features em subconjuntos
3. "Forward feature selection" utilizando árvore de decisão simples
4. Aplicação de vários modelos e "Grid search" para a definição dos hiperparâmetros
5. Comparação dos resultados
6. Seleção do melhor modelo e avaliação dos resultados
7. Teste de um modelo mais simples


Códigos originais: [`train_model.py`](src/models/train_model.py)

Passo a passo explicado: [`05_train_model.ipynb`](notebooks/05_train_model.ipynb)

---
### **Etapa 06 - Contando Repetições**
Criar um script em Python que pode contar repetições e mensurar a eficiência do código.

1. Visualizar os dados para identificar padrões
2. Configurar o Filtro Passa-Baixa (Butterworth)
3. Criar uma função para contar repetições
4. Criar um dataframe de referência (benchmark)
5. Avaliar os resultados (MAE)


Códigos originais: [`count_repetitions.py`](src/features/count_repetitions.py)

Passo a passo explicado: [`06_count_repetitions.ipynb`](notebooks/06_count_repetitions.ipynb)










