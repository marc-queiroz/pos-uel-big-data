---
layout: post
title:  "Breve discussão sobre precisão e acurácia"
date:   2019-09-21 08:00:00 -0300
categories: pos uel correlação pearson kaggle jupyter notebook python3 2019
---
<!-- [Método Naive Bayes para classificação de spam usando a lista Tabu (Traduzido para o português)](https://www.kaggle.com/marcqueiroz/m-todo-naive-bayes-para-classifica-o-de-spam) -->

## Precisão e a eficiência do modelo

Ao analisar um teste de detecção de doença para bebês recém-nascido, conseguimos uma precisão de 98%. Mas o que isso realmente significa? O teste em questão foi realizado para bebês com nome Luke.

Como veremos a seguir, esse teste possui mesmo mais de 98% de precisão. Apesar disso, é um teste incrivelmente estúpido e uma boa ilustração do motivo pelo qual nós não usamos “precisão” para medir a eficiência de um modelo.

Imagine construir um modelo para fazer uma avaliação binária. Esse e-mail é spam? Deveríamos contratar este candidato? Este viajante é um terrorista em segredo?

Dado um conjunto de dados etiquetados e um modelo preditivo, cada ponto de dados se estabelece em quatro categorias:

* Positivo verdadeiro: “Esta mensagem é spam e previmos spam corretamente.”
* Positivo falso (Erro Tipo 1): “Esta mensagem não é spam, mas previmos que era.”
* Negativo falso (Erro Tipo 2): “Esta mensagem é spam, mas previmos que não era.”
* Negativo verdadeiro: “Esta mensagem não é spam e previmos que não era.”

Representamos essa contagem em uma matriz de confusão:

![Confusion Matrix](/pos-uel-big-data/assets/precisao_acuracia/figura01.png "Matriz de confusão")

Vamos ver como o teste de doença se encaixa nessa estrutura. Por agora, aproximadamente 5 bebês de 1000 se chamam Luke (http://bit.ly/1CchAqt). A incidência de normal da doença é de aproximadamente 1,4%, ou 14 de cada 1000 pessoas (http://1.usa.gov/1ycORjO).
Se acreditarmos que esses dois fatores são independentes e aplicar o teste “Luke para doença” em um milhão de pessoas, esperaríamos ver uma matriz de confusão com esta:

![Confusion Matrix](/pos-uel-big-data/assets/precisao_acuracia/figura02.png "Matriz Luke vs doença")


Podemos usar isso então para computar diversas estatísticas sobre o desempenho do modelo. Por exemplo, a acurácia é definida como a fração de premissas corretas:

```python
def accuracy(tp, fp, fn, tn):
  correct = tp + tn
  total = tp + fp + fn + tn
  return correct / total

print accuracy(70, 4930, 13930, 981070)      # 0.98114
```
Parece um número bem interessante. Mas, evidentemente, não é um bom teste, o que significa que não deveríamos colocar muita crença na acurácia bruta.
É comum considerar a combinação de precisão e sensibilidade. Exatidão significa o quão precisas nossas previsões positivas eram:
```python
def precision(tp, fp, fn, tn):
  return tp / (tp + fp)

print precision(70, 4930, 13930, 981070)      # 0.014
```
A sensibilidade mede qual fração dos positivos nossos modelos identificam:
```python
def recall(tp, fp, fn, tn):
  return tp / (tp + fn)

print recall(70, 4930, 13930, 981070)      # 0.005
```
Ambos são números terríveis, refletindo um modelo terrível.
Às vezes, precisão e sensibilidade são combinados ao F1 Score, definido assim:

```python
def f1_score(tp, fp, fn, tn):
  p = precision(tp, fp, fn, tn)
  r = recall(tp, fp, fn, tn)
  return 2 * p * r / (p + r)
```
Essa é a média harmônica (http://en.wikipedia.org/wiki/Harmonic_mean) da acurácia e sensibilidade e se acha necessariamente encontrada entre elas.
Geralmente, a escolha de um modelo implica em um compromisso entre acurácia e sensibilidade. Um modelo que prevê “sim” quando se está um pouco confiante provavelmente terá uma sensibilidade alta mas uma acurácia baixa; um modelo que prevê “sim” somente quando está extremamente confiante provavelmente terá uma sensibilidade baixa e uma acurácia alta.
Como alternativa, você pode pensar nisso como uma troca entre positivos e negativos falsos. Dizer “sim” com muita frequência trará muitos positivos falsos; dizer “não” com muita frequência trará muitos negativos falsos.
Imagine que existiram dez fatores de risco para a doença em questão, e que, quanto mais você os tenha, mais você estará propenso a desenvolvê-la. Nesse caso, você pode imaginar uma continuidade de testes: “prever determinada doença se houver ao menos um fator de risco”, “prever "evento" se houver ao menos dois fatores de risco” e assim por diante. Conforme o limite aumenta, você aumenta a exatidão do teste (desde que as pessoas com mais fatores de risco sejam mais propensas a desenvolver a doença) e diminui a confirmação do teste (uma vez que cada vez menos pacientes da doença chegarão ao limite).
