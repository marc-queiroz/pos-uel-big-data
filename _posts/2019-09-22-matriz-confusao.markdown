---
layout: post
title:  "Matriz Confusão em Python"
date:   2019-09-29 08:00:00 -0300
categories: pos uel matriz confusão python 
---

## Matriz Confusão com Python

Post de [Emanuel Souza](http://github.com/emanuelsouza)

Matriz de confusão é uma uma ferramenta muito usada para avaliações de
<a href="https://towardsdatascience.com/machine-learning-classifiers-a5cc4e1b0623" class="bu df ni nj nk nl">modelos de classificação</a>
em
<a href="https://medium.com/data-science-brigade/a-diferen%C3%A7a-entre-intelig%C3%AAncia-artificial-machine-learning-e-deep-learning-930b5cc2aa42" class="bu df ni nj nk nl">Aprendizado de Máquina</a>
(mais comumente chamado de Machine Learning).

Para termos dados de exemplo, imagine que eu tivesse um modelo
que, dada as características fisiológicas de uma paciente, dissesse que
a mesma está grávida ou não. Porém, para o nosso contexto, eu só trarei
uma lista com os dados reais, e uma lista de dados preditos pelo modelo,
ambos dados *fake*.

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura01.png" class="hy n o hx y mm mn qh qi" width="513" height="80" alt="" /><figcaption>Listas com valores “fake”</figcaption>
</figure>

Como saber se meu modelo previu bem? Como saber se ele prevê bem a
classe que queremos (Grávida)? Essas e outras questões podemos entender
com as matrizes de confusão.

------------------------------------------------------------------------

O que são matrizes de confusão?
===============================

É um tabela que mostra as frequências de classificação para cada classe
do modelo. Pegando o exemplo acima, ela vai nos mostrar as frequências:

-   <span id="e7bb">**Verdadeiro positivo (*true positive* — TP)**:
    ocorre quando no conjunto real, a classe que estamos buscando foi
    prevista corretamente. Por exemplo, quando a mulher está grávida e o
    modelo previu corretamente que ela está grávida.</span>
-   <span id="3af2">**Falso positivo (*false positive* — FP)**: ocorre
    quando no conjunto real, a classe que estamos buscando prever foi
    prevista incorretamente. Exemplo: a mulher não está grávida, mas o
    modelo disse que ela está.</span>
-   <span id="2398">**Falso verdadeiro (*true negative* — TN)**: ocorre
    quando no conjunto real, a classe que não estamos buscando prever
    foi prevista corretamente. Exemplo: a mulher não estava grávida, e o
    modelo previu corretamente que ela não está.</span>
-   <span id="2719">**Falso negativo (*false negative* — FN)**: ocorre
    quando no conjunto real, a classe que não estamos buscando prever
    foi prevista incorretamente. Por exemplo, quando a mulher está
    grávida e o modelo previu incorretamente que ela não está
    grávida.</span>

Ao final teremos para o conjunto acima

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura02.png" class="hy n o hx y mm mn qh qi" width="404" height="90" alt="" /><figcaption>Matriz de Confusão usando os dados que temos</figcaption>
</figure>

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura03.png" class="hy n o hx y mm mn qh qi" width="327" height="85" alt="" /><figcaption>Matriz de Confusão mostrando as categorias</figcaption>
</figure>

Assim, nosso modelo:

-   <span id="7a6b">Previu grávida 3 vezes corretamente</span>
-   <span id="6c49">Previu não grávidas 4 vezes corretamente</span>
-   <span id="9e55">Previu grávida 1 vez incorretamente</span>
-   <span id="4f2a">Previu não grávida 2 vezes incorretamente</span>

A seguir, analisaremos algumas informações úteis que podemos tirar dessa
tabela

Alguns conceitos importantes decorrentes da matriz
==================================================

Acurácia
--------

<a href="https://developers.google.com/machine-learning/crash-course/classification/accuracy" class="bu df ni nj nk nl">Diz quanto o meu modelo acertou das previsões possíveis</a>.
No contexto acima, nosso modelo teve uma acurácia de 70%, pois acertou 7
das 10 previsões. E a razão entre o somatório das previsões corretas
(verdadeiros positivos com verdadeiros negativos) sobre o somatório das
previsões.

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura04.png" class="hy n o hx y mm mn qh qi" width="589" height="87" alt="" />
</figure>

Mas isso é tudo?

Recall
------

No material do
<a href="https://developers.google.com/machine-learning/crash-course/classification/precision-and-recall" class="bu df ni nj nk nl">Google Developers para Machine Learning</a>,
podemos ver que *recall* responde a seguinte pergunta: qual proporção de
positivos foi identificados corretamente? Em outras palavras, quão bom
meu modelo é para prever positivos, sendo positivo entendido como a
classe que se quer prever, no nosso contexto, se a mulher está grávida.
É definido como a razão entre verdadeiros positivos sobre a soma de
verdadeiros positivos com negativos falsos.

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura05.png" class="hy n o hx y mm mn qh qi" width="198" height="83" alt="" />
</figure>

Precisão
--------

Ainda usando o material do Google Developers, eles definem precisão como
a resposta para a seguinte pergunta: Qual a proporção de identificações
positivas foi realmente correta? Em outras palavras,
o qual bem meu modelo trabalhou.

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura06.png" class="hy n o hx y mm mn qh qi" width="238" height="79" alt="" />
</figure>

f-score
-------

Já o *f-score* nos mostra o balanço entre a precisão e o *recall* de
nosso modelo. Sua fórmula é:

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura07.png" class="hy n o hx y mm mn qh qi" width="260" height="81" alt="" />
</figure>

Uma observação **muito** importante. Os cálculos acima visam entender o
seu modelo sobre os dados positivos. Ou seja, quero prever se a paciente
está grávida, portanto vou olhar métricas para avaliar essa classe.
Quando estamos falando de classificação multiclass (mais de duas classes
possíveis de resposta), podemos trabalhar sobre a classe que queremos
prever, mas também podemos olhar para cada classe em separado. Para
tanto, pode ser útil, na hora de fazer a matriz de confusão, considerar
a classe que queremos prever como a classe positiva, e todo o restante
como negativo, assim, “inferimos” uma classificação binária só para
entender o quão bem o nosso modelo está em prever a classe que queremos.

O pacote
<a href="https://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics" class="bu df ni nj nk nl">metrics</a>
do sklearn, possui uma função muito interessante:
<a href="https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html#sklearn.metrics.classification_report" class="bu df ni nj nk nl">classification_report</a>,
que entrega todas as métricas acima prontas em formato tabular, vale a
pena a conferida. Tais métricas são consideradas para cada classe do
nosso modelo. Um exemplo no print abaixo:

<figure>
<img src="/pos-uel-big-data/assets/matriz_confusao/figura08.png" class="hy n o hx y mm mn qh qi" width="480" height="155" alt="" />
</figure>

Exemplo em Python
=================

Lembrando que o sklearn já possui a implementação da
<a href="https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html" class="bu df ni nj nk nl">confusion_matrix</a>.
Fuçando o código fonte, verás que na versão atual (0.20.3), eles usam
por debaixo do capô, a função
<a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.coo_matrix.html#scipy.sparse.coo_matrix" class="bu df ni nj nk nl">coo_matrix</a>,
do módulo sparse do pacote scipy.

Calculando para matrizes 2 x 2 (classificação binária)
------------------------------------------------------

```python
import numpy as np

# 1 para grávida, 0 para não grávida
valores_reais    = [1, 0, 1, 0, 0, 0, 1, 0, 1, 0]
valores_preditos = [1, 0, 0, 1, 0, 0, 1, 1, 1, 0]

def get_confusion_matrix(reais, preditos, labels):
    """
    Uma função que retorna a matriz de confusão para uma classificação binária
    
    Args:
        reais (list): lista de valores reais
        preditos (list): lista de valores preditos pelo modelos
        labels (list): lista de labels a serem avaliados.
            É importante que ela esteja presente, pois usaremos ela para entender
            quem é a classe positiva e quem é a classe negativa
    
    Returns:
        Um numpy.array, no formato:
            numpy.array([
                [ tp, fp ],
                [ fn, tn ]
            ])
    """
    # não implementado
    if len(labels) > 2:
        return None

    if len(reais) != len(preditos):
        return None
    
    # considerando a primeira classe como a positiva, e a segunda a negativa
    true_class = labels[0]
    negative_class = labels[1]

    # valores preditos corretamente
    tp = 0
    tn = 0
    
    # valores preditos incorretamente
    fp = 0
    fn = 0
    
    for (indice, v_real) in enumerate(reais):
        v_predito = preditos[indice]

        # se trata de um valor real da classe positiva
        if v_real == true_class:
            tp += 1 if v_predito == v_real else 0
            fp += 1 if v_predito != v_real else 0
        else:
            tn += 1 if v_predito == v_real else 0
            fn += 1 if v_predito != v_real else 0
    
    return np.array([
        # valores da classe positiva
        [ tp, fp ],
        # valores da classe negativa
        [ fn, tn ]
    ])

get_confusion_matrix(reais=valores_reais, preditos=valores_preditos, labels=[1,0])
# array([[3, 1], [2, 4]])
```

Post de [Emanuel Souza](http://github.com/emanuelsouza)

Post original [Entendendo o que é Matriz de Confusão com Python](https://medium.com/data-hackers/entendendo-o-que-%C3%A9-matriz-de-confus%C3%A3o-com-python-114e683ec509)

