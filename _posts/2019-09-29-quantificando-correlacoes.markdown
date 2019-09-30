---
layout: post
title:  "Coeficiente de correlação de Pearson"
date:   2019-09-21 08:00:00 -0300
categories: pos uel correlação pearson kaggle jupyter notebook python3 2019
---
## Coeficiente de correlação de Pearson 

[Kaggle - Coeficiente de correlação de Pearson](https://www.kaggle.com/marcqueiroz/coeficiente-de-correla-o-de-pearson)

## Quantificando Correlação

Muitos métodos estatísticos e de aprendizado de máquina pressupõem que seus recursos sejam independentes. Para testar se eles são independentes, você precisa avaliar a correlação deles - até que ponto
variáveis demonstram interdependência. 

A correlação é quantificada pelo valor de uma variável chamada **r**, que varia entre –1
e 1. Quanto mais próximo o valor de **r** for 1 ou –1, maior a correlação entre duas
variáveis. Se duas variáveis tiverem um valor **r** próximo a 0, isso poderá indicar que elas são
variáveis independentes.

## Calculando a correlação com o r de Pearson

Se você deseja descobrir relacionamentos dependentes entre variáveis contínuas em um conjunto de dados,
use estatísticas para estimar sua correlação. A forma mais simples de análise de correlação é a 
correlação Pearson, que assume que:
* Seus dados são normalmente distribuídos.
* Você tem variáveis numéricas contínuas.
* Suas variáveis estão linearmente relacionadas.
