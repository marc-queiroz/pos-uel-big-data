---
layout: post
title:  "Algoritmos utilizados no aprendizado de máquina"
date:   2019-09-29 08:00:00 -0300
categories: pos uel ML machine learning algorithms
published: false
---
## Selecionando algoritmos com base na função

Quando você precisa escolher uma classe de algoritmos de aprendizado de máquina, é útil considerar cada classe de modelo com base em sua funcionalidade. Na maioria das vezes, a funcionalidade algorítmica cai no categorias mostradas na figura abaixo. 

![Mind Map - ML algorithms](/pos-uel-big-data/fundamentos-big-data-2/images/mind_map.png "Mind Map - ML algorithms")

**Algoritmo de regressão:** Você pode usar esse tipo de algoritmo para modelar relacionamentos entre
recursos em um conjunto de dados. 

**Algoritmo de aprendizado de regras de associação:** esse tipo de algoritmo é um conjunto de métodos baseado em regras que você pode usar para descobrir associações entre recursos em um conjunto de dados.

**Algoritmo baseado em instância:** se você deseja usar observações em seu conjunto de dados para classificar novas observações baseadas em similaridade, você pode usar esse tipo. Para modelar com instâncias, você pode usar métodos como a classificação de vizinhos k-mais próximos.

**Algoritmo de regularização:** você pode usar a regularização para introduzir informações adicionais como um meios pelos quais evitar o ajuste excessivo do modelo ou resolver um problema incorreto.

**Método Naïve Bayes:** se você deseja prever a probabilidade de ocorrência de um evento com base em alguma evidência em seus dados, você pode usar esse método, com base na classificação e regressão.

**Árvore de decisão:** uma estrutura em árvore é útil como uma ferramenta de suporte à decisão. Você pode usá-lo para criar modelos que preveem possíveis quedas associadas a qualquer decisão.

**Algoritmo de cluster:** você pode usar esse tipo de método de aprendizado de máquina não supervisionado para descobrir subgrupos dentro de um conjunto de dados não rotulado.

**Método de redução de dimensão:** se você estiver procurando um método para usar como filtro para remover informações redundantes, ruído e outliers de seus dados, considere as técnicas de redução de dimensão como análise fatorial e análise de componentes principais. 

**Rede neural:**  uma rede neural imita como o cérebro resolve problemas, usando uma camada de unidades neurais interconectadas como um meio pelo qual aprender e inferir regras a partir de dados observados.  É frequentemente usado em aplicativos de reconhecimento de imagem e visão computacional.

Imagine que você está decidindo se deve ir à praia. Você nunca vai à praia se
está chovendo e você não gosta de ir se estiver mais frio do que 23 graus lá fora. Estes
são as duas entradas para sua decisão. Sua preferência de não ir à praia quando chove é
muito mais forte do que a sua preferência para não ir à praia quando está mais frio que 23 graus, então
você pesa essas duas entradas adequadamente. Para qualquer instância em que você decida se
você vai à praia, considera esses dois critérios, soma o resultado e decide
se deve ir. Se você decidir ir, seu limite de decisão foi atendido. Se você decidir não
para ir, seu limite de decisão não foi atendido. Essa é uma analogia simplista de como neural
redes funcionam.

Agora, para uma definição mais técnica. O tipo mais simples de rede neural é o
Perceptron. Ele aceita mais de uma entrada, que pesa e adiciona em uma camada do processador,
e, com base na função de ativação e no limite definido para ela, gera um resultado. 
A função de ativação é uma função matemática que transforma entradas em um sinal de saída. A
camada de processador é chamada de camada oculta. Uma rede neural é uma camada de Perceptrons conectados
que todos trabalham juntos como uma unidade para aceitar entradas e retornar saídas que sinalizam se alguma
critérios são atendidos. Uma característica fundamental das redes neurais é que elas são auto-didátas - em outras palavras,
eles adaptam, aprendem e otimizam por alterações nos dados de entrada. A Figura abaixo é um layout esquemático que
descreve como um Perceptron está estruturado.

![As redes neurais são camadas conectadas de unidades neurais artificiais](/pos-uel-big-data/fundamentos-big-data-2/images/figura4-3.png "As redes neurais são camadas conectadas de unidades neurais artificiais")


**Método de aprendizado profundo (Deep learning):** este método incorpora redes neurais tradicionais em sucessivas camadas
para oferecer treinamento em camadas profundas para gerar resultados preditivos.

**Algoritmo de grupo:** você pode usar algoritmos de grupo para combinar aprendizado de máquina
abordagens para obter resultados melhores do que os disponíveis em qualquer máquina
método de aprendizagem por si próprio.

