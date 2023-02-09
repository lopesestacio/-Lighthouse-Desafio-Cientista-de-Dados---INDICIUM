# [Lighthouse] Desafio Cientista de Dados - Manutenção preventiva - INDICIUM

Este projeto foi realizado como desafio para avaliação no processo seletivo do programa Lighthouse da Indicium.

## Objetivos :pushpin: :grey_exclamation:
O projeto possui como objetivo a criação de um modelo de classificação capaz de identificar quais máquinas apresentam potencial de falha tendo como base dados extraídos através de sensores durante o processo de manufatura.

## :book: Dados 

Os dados utilizados no projeto foram disponibilizados pela INDICIUM.

Foram disponilizados os seguintes arquivos.

- `[Lighthouse] Desafio Cientista de Dados - Manutenção preventiva.docx`---> Contendo as instruções para o desafio.
- `desafio_manutencao_preditiva_treino.csv`---> Arquivo csv contendo o dataset para treino com as features e os rotulos.
- `desafio_manutencao_preditiva_teste.csv`---> Arquivo csv contendo o dataset de teste para realizar o predição com o modelo já treinado.

Os seguintes arquivos foram adicionados para compor o projeto.

- `regression_logistic.ipynb` ---> Jupyter notebook contendo as informações do modelo escolhido de regressão logistica (EDA, Estatisticas descritivas, treinamento, predição)
- `decision_tree.ipynb` ---> Jupyter notebook contendo as informações do modelo alternativo de arvore de decisão (EDA, Estatisticas descritivas, treinamento, predição)
- `predicted.csv`---> Arquivo csv contendo o resultado final do modelo em uma planilha com apenas duas colunas (rowNumber, predictedValues). 
- `requirements.txt` ---> Contendo as dependencias do projeto.

### Documentação dos dados  :eyes: :clipboard:

| udi | product_id | type | air_temperature_k | process_temperature_k | rotational_speed_rpm | torque_nm | tool_wear_min | failure_type |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | M14860 | M | 298.1 | 308.6 | 1551 | 42.8 | 0 | No Failure |
| 1 | 2 | L47181 | L | 298.2 | 308.7 | 1408 | 46.3 | 3 | No Failure |
| 2 | 5 | L47184 | L | 298.2 | 308.7 | 1408 | 40.0 | 9 | No Failure |
| 3 | 6 | M14865 | M | 298.1 | 308.6 | 1425 | 41.9 | 11 | No Failure |
| 4 | 7 | L47186 | L | 298.1 | 308.6 | 1558 | 42.4 | 14 | No Failure |




- `UID`: Identificador único que varia de 1 a 10000
- `product_id`: Consistindo em uma letra L, M ou H para baixo (50% de todos os produtos), médio (30%) e alto (20%) como variantes de qualidade do produto e um número de série específico da variante
- `type`: apenas o tipo de produto L, M ou H da coluna 2
- `air_temperature_k`: Gerada usando um processo de passeio aleatório posteriormente normalizado para um desvio padrão de 2 K em torno de 300 K
- `process_temperature_k`: Gerada usando um processo de passeio aleatório normalizado para um desvio padrão de 1 K, adicionado à temperatura do ar mais 10 K.
- `rotational_speed_rpm`: Calculada a partir de uma potência de 2860 W, sobreposta com um ruído normalmente distribuído
- `torque_nm`: Os valores de torque são normalmente distribuídos em torno de 40 Nm com SD = 10 Nm e sem valores negativos.
- `tool_wear_min`: As variantes de qualidade H/M/L adicionam 5/3/2 minutos de desgaste da ferramenta à ferramenta utilizada no processo.
- `failure_type` : Contendo o tipo de falha da maquina. 

# Manipulação dos dados  :pencil:

## Seleção de features.

Retiramos a coluna `UID` por se tratar de uma variavel categorica nominal, que serve apenas como identificador.

Retiramos a coluna `product_id` por se tratar de uma variavel categorica nominal, que serve para identificar cada maquina
com sua variante de qualidade do produto (L, M, ou H) com uma sequencia especifica.

Retiramos a coluna `type` por se tratar de uma variavel categorica nominal, que indentifica a variante de qualidade do produto. Pensamos que esse coluna por haver correlação com a coluna `tool_wear_min` poderia ser utilizado no modelo escolhido, porém houve queda percentual da accuracia, e esse feature se mostrou irrelevante.

Utilizamos as seguintes features.

- `air_temperature_k`
- `process_temperature_k`
- `rotational_speed_rpm`
- `torque_nm`
- `tool_wear_min`

## Dados ausentes.

O dataset não possuia dados ausentes para serem tratados.

# Estatisticas descritivas.

As estatísitcas nos informam como esta a distribuição dos nossos dados, podem indicar a presença de outliers, e verificar a assimetria dos dados.

| Feature | Count | Mean | Std | Min | 25% | 50% | 75% | Max |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| air_temperature_k | 6667.000000 | 299.992515 | 1.994710 | 295.300000 | 298.300000 | 300.000000 | 301.500000 | 304.500000 |
| process_temperature_k | 6667.000000 | 309.992620 | 1.488101 | 305.700000 | 308.800000 | 310.000000 | 311.100000 | 313.800000 |
| rotational_speed_rpm | 6667.000000 | 1537.419529 | 177.182908 | 1168.000000 | 1422.500000 | 1503.000000 | 1612.000000 | 2886.000000 |
| torque_nm | 6667.000000 | 40.058512 | 9.950804 | 3.800000 | 33.200000 | 40.200000 | 46.800000 | 76.600000 |
| tool_wear_min | 6667.000000 | 108.098095 | 63.359915 | 0.000000 | 54.000000 | 108.000000 | 162.000000 | 251.000000 |

##




