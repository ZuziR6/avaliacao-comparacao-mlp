**AINDA FALTA PREEENCHER OS DADOS**

# Dataset

Esta pasta é destinada aos dados utilizados nos experimentos de classificação binária com redes neurais multicamadas (MLP).

## Fonte dos dados

O dataset utilizado neste projeto foi obtido a partir de:

**Link:** (https://raw.githubusercontent.com/IBM/telco-customer-churn-on-icp4d/master/data/Telco-Customer-Churn.csv)

## Sobre o dataset

A base contém os registros utilizados para desenvolver o problema de classificação binária estudado no projeto.

**Quantidade de registros:** [COLOCAR QUANTIDADE]

**Quantidade de features:** [COLOCAR QUANTIDADE]

**Variável target:** [COLOCAR NOME DO TARGET]

**Classe positiva:** [COLOCAR CLASSE]

**Classe negativa:** [COLOCAR CLASSE]

## Organização dos dados

O arquivo utilizado pelo notebook deve ser disponibilizado localmente dentro desta pasta.

Exemplo:

```text
data/
├── README.md
└── dataset.csv
```

O arquivo `dataset.csv` não é versionado neste repositório quando sua distribuição não é permitida pela fonte original.

## Como obter os dados

1. Acesse a fonte oficial indicada acima.
2. Faça o download do dataset.
3. Coloque o arquivo na pasta `data/`.
4. Verifique se o nome e o formato do arquivo correspondem ao esperado pelo notebook.
5. Execute o notebook localizado em:

```text
notebooks/Experimentos_DL.ipynb
```

## Observação sobre versionamento

Os dados brutos não são necessariamente armazenados neste repositório para evitar a distribuição indevida de conteúdo pertencente à fonte original.

O notebook contém as etapas necessárias para carregamento e preparação dos dados utilizados nos experimentos.
