# Detectar anomalias de transações 

[![Static Badge](https://img.shields.io/badge/-Entrega%20Final-white)](https://github.com/jorgetxjr/detect_anomalia_transacoes_dio/blob/master/deteccao_fraudes.ipynb)
[![Static Badge](https://img.shields.io/badge/-Meu%20LinkedIn-blue)](https://www.linkedin.com/in/jorge-teixeira-jr/)

## Sobre o projeto
Executando o Aprendizado por Projetos (*Project Based Learning - PBL*) da [plataforma DIO](https://www.dio.me/), este projeto é para a análise de dados e segurança, usando o Python. Sendo o alvo deste projeto a identificação de fraudes bancárias.

## Tecnologias utilizadas
A base de dados é fornecida pelo Google com dados despersonalizados. O desenvolvimento foi feito no VSCode usando a extensão do Jupyter Notebook - podendo ser executado também em sua versão de browser.

## Instalação e dependências
Para a execução deste projeto além do Python e Jupyter Notebook, são necessárias as seguintes bibliotecas:
- pandas 
- numpy 
- matplotlib
- shap 
- scikit-learn
- imblearn
- xgboost

Para a instalação, use no terminal o comando *pip install*, seguido da biblioteca desejada. Exemplo:

```bash
pip install pandas
```

## Problemas Enfrentados
A principal característica desta base de dados é o seu **desbalanço**. Sendo 99% das operações válidas e menos de 1% como fraude. Os dados para inferência estatística e treinamento de modelos de aprendizado de máquina são envieasados, podendo levar ao *overfit* - quando o modelo desempenha bem no treinamento, mas nos testes e cenário real, não.
Tal problema é demonstrado pela tabela de resposta do modelo *Logistic Regression*:

2000 iterações - Logistic Regression
| Class / Metric | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| **0** | 1.00 | 1.00 | 1.00 | 85295 |
| **1** | 0.85 | 0.68 | 0.76 | 148 |
| **Accuracy** | | | 1.00 | 85443 |
| **Macro Avg** | 0.92 | 0.84 | 0.88 | 85443 |
| **Weighted Avg** | 1.00 | 1.00 | 1.00 | 85443 |

>0 = transação normal, 1 = fraude

> [!WARNING]
> **Sobre a execução do *Logistic Regression* com 2000 iterações:**
> Haverá um aviso e não um erro, informando que a quantidade de execuções terminou antes de um resultado adequado. Todavia, valores maiores de iteração foram testandos e não afetam significativamente o resultado do modelo. 
> **Pode ignorar o warning e prosseguir.**

Este modelo traz como resultado a curva ROC e a relação Precision-Recall.

![Curva ROC inicial](https://github.com/jorgetxjr/detect_anomalia_transacoes_dio/blob/master/assets/roc_base.png)
>Curva ROC

![Curva Precision-Recall inicial](https://github.com/jorgetxjr/detect_anomalia_transacoes_dio/blob/master/assets/precision-recall_base.png)

>Curva Precision-Recall

## Solução aplicada
A solução usada para contornar este problema foi o *underfit*. O dataset original é diminuido, fazendo com que a quantidade de dados de transações normais e de fraude sejam iguais. 
Com uma nova análise do modelo *Logistic Regression*, os resultados foram os seguintes:

2000 iterações - Logistic Regression
| Class / Metric | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| **0** | 0.93 | 0.96 | 0.95 | 148 |
| **1** | 0.96 | 0.93 | 0.95 | 148 |
| **Accuracy** | | | 0.95 | 296 |
| **Macro Avg** | 0.95 | 0.95 | 0.95 | 296 |
| **Weighted Avg** | 0.95 | 0.95 | 0.95 | 296 |

>0 = transação normal, 1 = fraude

Aplicando as mesmas características do modelo *Logistic Regression* no novo *dataset*, temos as seguintes curvas ROC e Precision-Recall:

![Curva ROC undersampling](https://github.com/jorgetxjr/detect_anomalia_transacoes_dio/blob/master/assets/roc_undersampling.png)
>Curva ROC

![Curva Precision-Recall undersampling](https://github.com/jorgetxjr/detect_anomalia_transacoes_dio/blob/master/assets/precision-recall_undersampling.png)

>Curva Precision-Recall

## Próximos passos
Outros modelos como *Overfit* e Árvore de decisão também foram explicados e podem ser aplicados em continuidade, afim de comparar os resultados e buscando a otimização da entrega.

## Contribuições e contato
Críticas, sugestões e melhorias são sempre bem vindas para o engrandecimento de meu conhecimento!

[![Static Badge](https://img.shields.io/badge/-Meu%20LinkedIn-blue)](https://www.linkedin.com/in/jorge-teixeira-jr/)