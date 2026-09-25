# Otimização e Comparativo de Arquiteturas em Deep Learning

## Sobre o projeto

Este repositório apresenta uma investigação experimental sobre o impacto de diferentes arquiteturas de **Redes Neurais Multicamadas (Multi-Layer Perceptron — MLP)** em um problema de classificação binária.

O objetivo principal foi avaliar como alterações na **capacidade da rede**, **profundidade** e **funções de ativação** influenciam o desempenho e a capacidade de generalização dos modelos.

Foram realizados **7 experimentos controlados (E1 a E7)**, mantendo as condições de treinamento constantes sempre que possível. A análise considerou múltiplas métricas, permitindo observar não apenas a acurácia, mas também o equilíbrio entre **Precisão, Recall e F1-Score**.

O projeto foi desenvolvido como parte da disciplina de **Deep Learning / Inteligência Artificial** da graduação em Ciência da Computação.

---

## Objetivos

O projeto teve como objetivos:

* Explorar e preparar uma base de dados para classificação binária;
* Construir diferentes arquiteturas de redes neurais densas;
* Avaliar o impacto do número de neurônios nas camadas ocultas;
* Avaliar o impacto do aumento da profundidade da rede;
* Comparar diferentes funções de ativação;
* Identificar sinais de **overfitting** e **underfitting**;
* Comparar o desempenho dos modelos utilizando múltiplas métricas;
* Selecionar uma arquitetura com melhor capacidade de generalização com base no conjunto de validação;
* Avaliar o modelo selecionado posteriormente no conjunto de teste.

---

## Metodologia

O desenvolvimento seguiu um fluxo completo de Machine Learning:

1. Entendimento do problema;
2. Análise exploratória dos dados (EDA);
3. Identificação de valores ausentes, inconsistências e duplicatas;
4. Investigação de possíveis fontes de data leakage;
5. Tratamento e preparação dos dados;
6. Divisão estratificada em treino, validação e teste;
7. Aplicação do pré-processamento;
8. Construção das diferentes arquiteturas de MLP;
9. Treinamento dos modelos;
10. Avaliação utilizando múltiplas métricas;
11. Comparação controlada dos experimentos;
12. Seleção da arquitetura com base nos resultados de validação;
13. Avaliação final no conjunto de teste.

Um cuidado importante da metodologia foi evitar que o conjunto de teste influenciasse as decisões de modelagem. Dessa forma, a escolha da arquitetura foi realizada utilizando exclusivamente os resultados obtidos no conjunto de validação.

---

## Experimentos

Foram realizados sete experimentos, organizados para analisar separadamente os efeitos da **largura**, **profundidade** e **função de ativação**.

### Comparação de capacidade e profundidade

Os experimentos E1 a E5 utilizaram a função de ativação ReLU:

| Experimento | Arquitetura    | Ativação | Objetivo                        |
| ----------- | -------------- | -------- | ------------------------------- |
| E1          | `[16]`         | ReLU     | Arquitetura de referência       |
| E2          | `[32]`         | ReLU     | Aumento da capacidade           |
| E3          | `[64]`         | ReLU     | Aumento adicional da capacidade |
| E4          | `[32, 16]`     | ReLU     | Aumento da profundidade         |
| E5          | `[64, 32, 16]` | ReLU     | Arquitetura mais profunda       |

### Comparação das funções de ativação

Os experimentos E2, E6 e E7 mantiveram a arquitetura `[32]`, permitindo comparar diferentes funções de ativação:

| Experimento | Arquitetura | Ativação |
| ----------- | ----------- | -------- |
| E2          | `[32]`      | ReLU     |
| E6          | `[32]`      | Tanh     |
| E7          | `[32]`      | Sigmoid  |

Essa organização permite observar o efeito da função de ativação mantendo a topologia da rede constante.

---

## Resultados

Os modelos foram avaliados principalmente a partir do desempenho no conjunto de validação.

| Experimento | Arquitetura    | Ativação | Loss Val. | Acc. Treino | Acc. Val. | Precisão | Recall | F1-Score |
| ----------- | -------------- | -------- | --------: | ----------: | --------: | -------: | -----: | -------: |
| E1          | `[16]`         | ReLU     |    0.4196 |      0.7930 |    0.8166 |   0.6351 | 0.5072 |   0.5640 |
| E2          | `[32]`         | ReLU     |    0.4287 |      0.7977 |    0.8270 |   0.6570 | 0.4892 |   0.5608 |
| E3          | `[64]`         | ReLU     |    0.4388 |      0.7882 |    0.8278 |   0.6455 | 0.4388 |   0.5225 |
| E4          | `[32, 16]`     | ReLU     |    0.4482 |      0.7759 |    0.8333 |   0.5963 | 0.4676 |   0.5242 |
| E5          | `[64, 32, 16]` | ReLU     |    0.5832 |      0.7578 |    0.8708 |   0.5511 | 0.4460 |   0.4930 |
| E6          | `[32]`         | Tanh     |    0.4208 |      0.7939 |    0.8217 |   0.6432 | 0.4928 |   0.5580 |
| E7          | `[32]`         | Sigmoid  |    0.4149 |      0.7968 |    0.8083 |   0.6429 | 0.5180 |   0.5737 |

> As métricas apresentadas correspondem aos resultados obtidos durante os experimentos registrados no notebook.

### Principais observações

**E7 — `[32]` com Sigmoid**

Apresentou o maior F1-Score de validação entre os experimentos, com **0.5737**, além da menor validation loss, de **0.4149**.

**E1 — `[16]` com ReLU**

Apresentou F1-Score de **0.5640**, mostrando que uma arquitetura mais simples pode apresentar desempenho competitivo sem aumentar significativamente a complexidade do modelo.

**E2 — `[32]` com ReLU**

Obteve a maior Precisão entre os experimentos, com **0.6570**, mas apresentou Recall inferior ao E7.

**E5 — `[64, 32, 16]` com ReLU**

Apresentou o maior gap entre desempenho de treino e validação em termos de acurácia, além do menor F1-Score entre os experimentos. O comportamento observado indica maior dificuldade de generalização nessa configuração.

---

## Análise dos experimentos

### Capacidade da rede

O aumento do número de neurônios não produziu uma melhora consistente nas métricas.

A arquitetura E1, com apenas 16 neurônios, apresentou F1-Score de 0.5640, enquanto E2, com 32 neurônios, apresentou 0.5608. O aumento para 64 neurônios em E3 reduziu o F1-Score para 0.5225.

Isso demonstra que aumentar a capacidade da rede não necessariamente resulta em melhor generalização para o problema analisado.

### Profundidade

O aumento do número de camadas também não apresentou ganho consistente.

Enquanto E2 utilizou uma única camada com 32 neurônios, E4 utilizou duas camadas `[32, 16]` e E5 utilizou três camadas `[64, 32, 16]`.

O F1-Score passou de:

* E2: **0.5608**
* E4: **0.5242**
* E5: **0.4930**

A arquitetura mais profunda apresentou o menor desempenho de F1-Score entre os experimentos.

### Funções de ativação

Mantendo a arquitetura `[32]`, foram comparadas três funções de ativação:

* ReLU: F1 = **0.5608**
* Tanh: F1 = **0.5580**
* Sigmoid: F1 = **0.5737**

Nesse conjunto de experimentos, a configuração com Sigmoid apresentou o maior F1-Score e a menor loss de validação.

Esse resultado destaca a importância de testar empiricamente diferentes configurações em vez de assumir previamente que uma determinada função de ativação produzirá necessariamente o melhor resultado.

---

## Overfitting e generalização

A comparação entre as métricas de treinamento e validação permitiu identificar comportamentos diferentes entre as arquiteturas.

A E5 apresentou uma acurácia de treino de **0.8708**, enquanto sua acurácia de validação foi de **0.7578**, indicando uma diferença significativa entre o desempenho observado nos dados utilizados para treinamento e nos dados de validação.

Além disso, seu F1-Score de validação foi de **0.4930**, inferior ao das demais arquiteturas.

Esse comportamento é compatível com sinais de **overfitting**, indicando que o aumento da capacidade e profundidade da rede não trouxe benefício de generalização nesse experimento.

---

## Modelo selecionado

Com base exclusivamente nos resultados obtidos no conjunto de validação, a arquitetura **E7 — `[32]` com função de ativação Sigmoid** apresentou o maior F1-Score entre os modelos avaliados:

**F1-Score: 0.5737**

Além disso, apresentou a menor loss de validação:

**Validation Loss: 0.4149**

A seleção considerou conjuntamente Precision, Recall, F1-Score e Loss, evitando utilizar apenas a acurácia como critério de decisão.

A avaliação final no conjunto de teste foi realizada somente após a definição da arquitetura.

---

## Tecnologias e ferramentas

### Linguagem

* Python 3.x

### Machine Learning e Deep Learning

* TensorFlow
* Keras
* Scikit-Learn

### Manipulação de dados

* Pandas
* NumPy

### Visualização

* Matplotlib
* Seaborn

### Ambiente

* Jupyter Notebook
* Google Colab

---

## Estrutura do repositório

```text
.
├── data/
│   └── README.md
│
├── notebooks/
│   └── Experimentos_DL.ipynb
│
├── docs/
│   └── Relatorio_Tecnico.pdf
│
├── images/
│   ├── distribuicao_classes.png
│   ├── comparacao_modelos.png
│   ├── matriz_confusao.png
│   └── curvas_treinamento.png
│
├── README.md
│
└── requirements.txt
```

---

## Como executar

### 1. Clone o repositório

```bash
git clone https://github.com/SEU-USUARIO/otimizacao-deep-learning.git
```

### 2. Acesse o diretório

```bash
cd otimizacao-deep-learning
```

### 3. Crie um ambiente virtual

No Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

No Linux/macOS:

```bash
python3 -m venv venv
source venv/bin/activate
```

### 4. Instale as dependências

```bash
pip install -r requirements.txt
```

### 5. Execute o notebook

```bash
jupyter notebook notebooks/Experimentos_DL.ipynb
```

Também é possível executar o projeto diretamente pelo Google Colab.

---

## Relatório técnico

O relatório técnico apresenta a documentação completa do projeto, incluindo:

* definição do problema;
* descrição da base;
* análise exploratória;
* tratamento dos dados;
* metodologia experimental;
* arquiteturas avaliadas;
* métricas de avaliação;
* comparação dos modelos;
* análise de overfitting e generalização;
* seleção da arquitetura;
* avaliação final no conjunto de teste;
* conclusões e limitações.

O documento está disponível em:

```text
docs/Relatorio_Tecnico.pdf
```

---

## Reprodutibilidade

O projeto foi estruturado buscando garantir a reprodução dos experimentos, utilizando uma semente aleatória fixa e mantendo os mesmos conjuntos de treino e validação durante a comparação das arquiteturas.

As transformações de pré-processamento foram ajustadas de acordo com a metodologia definida no projeto, evitando que informações do conjunto de validação e teste fossem utilizadas indevidamente durante o treinamento.

---

## Limitações

Os resultados apresentados são específicos para a base de dados e configuração experimental utilizadas neste projeto.

O desempenho observado não deve ser interpretado como evidência de que uma determinada arquitetura ou função de ativação será superior em outros problemas de classificação.

Além disso, o conjunto de arquiteturas avaliadas representa apenas uma parcela do espaço possível de configurações de redes neurais.

Como possíveis extensões, poderiam ser investigados:

* Dropout;
* L1/L2 Regularization;
* Batch Normalization;
* Early Stopping;
* ajuste sistemático da taxa de aprendizado;
* otimização de hiperparâmetros;
* outras arquiteturas;
* validação cruzada.

---

## Autores

**• Gabriel Guimarães de Oliveira — RM: 567835**

**• Pedro Paulo Ferreira Agnelo D'angelo — RM: 567564** 

**• Christian Raymundo Diaz - RM: 568324**

Ciência da Computação — FIAP

Projeto desenvolvido para a disciplina de Deep Learning / Inteligência Artificial.

---

## Licença

Este projeto foi desenvolvido para fins acadêmicos e de portfólio.

Caso utilize uma base de dados de terceiros, consulte e respeite os termos de uso e a licença estabelecidos pela fonte original.
