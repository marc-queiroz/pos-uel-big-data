---
layout: post
title:  "Explorando Probabilidade e Estatísticas Inferenciais"
date:   2019-09-21 08:00:00 -0300
categories: pos uel classification statistics probability naive bayes
published: false
---
[Método Naive Bayes para classificação de spam usando a lista Tabu (Traduzido para o português)](https://www.kaggle.com/marcqueiroz/m-todo-naive-bayes-para-classifica-o-de-spam)

## Explorando Probabilidade e Estatísticas Inferenciais

Probabilidade é um dos conceitos mais fundamentais em estatística. Para começar a fazer
senso de seus dados usando estatísticas, você precisa identificar algo tão básico quanto se
você está analisando estatísticas descritivas ou inferenciais. Você também precisa ter uma compreensão firme dos conceitos básicos de
distribuição de probabilidade. 

Uma estatística é um resultado derivado da realização de uma operação matemática em dados numéricos.
Em geral, você usa estatísticas na tomada de decisão. As estatísticas vêm em dois sabores:

**Descritivo:** As estatísticas descritivas fornecem uma descrição que ilumina algumas características
de um conjunto de dados numérico, incluindo distribuição do conjunto de dados, tendência central (como média, min ou
max) e dispersão (como no desvio e variância padrão).

**Inferencial:** em vez de focar nas descrições pertinentes de um conjunto de dados, as estatísticas inferenciais dividem uma seção menor do conjunto de dados e tentam deduzir informações significativas sobre o
conjunto de dados maior. Use esse tipo de estatística para obter informações sobre uma medida do mundo real em
que você está interessado.

É verdade que as estatísticas descritivas descrevem as características de um conjunto de dados numéricos, mas que
não diz por que você deveria se importar. De fato, a maioria dos cientistas de dados está interessada em
estatísticas apenas pelo que revelam sobre as medidas do mundo real que descrevem. 

Por exemplo, uma estatística descritiva é frequentemente associada a um grau de precisão, indicando a
o valor da estatística como uma estimativa da medida do mundo real.
Para entender melhor esse conceito, imagine que o proprietário de uma empresa queira estimar 
os lucros do trimestre. O proprietário pode utilizar uma média dos lucros dos últimos trimestres para usar como
estimativa de quanto ele ganhará no próximo trimestre. Mas se os lucros dos trimestres anteriores
variou amplamente, uma estatística descritiva que estimou a variação desse valor de lucro previsto (valor pelo qual essa estimativa em dólar pode diferir dos lucros reais que ele obterá)
indicar o quão longe o valor previsto pode estar do valor real. 

Você pode usar estatísticas descritivas de várias maneiras - para detectar discrepâncias, por exemplo, ou para
planejar requisitos de pré-processamento de recursos ou identificar rapidamente quais recursos você pode, 
deseja ou não deseja usar em uma análise.

Como as estatísticas descritivas, as estatísticas inferenciais são usadas para revelar algo sobre medidas do mundo real. As estatísticas inferenciais fazem isso fornecendo informações sobre uma pequena seleção de dados, para que você
possa usar essas informações para inferir algo sobre o conjunto de dados maior do qual foi retirado. Na
estatística, essa seleção de dados menor é conhecida como amostra e o conjunto de dados maior e mais completo de
qual a amostra é colhida é chamada população.

Se seu conjunto de dados for muito grande para ser analisado por inteiro, obtenha uma amostra menor desse conjunto de dados, analise-o,
e, em seguida, faça inferências sobre todo o conjunto de dados com base no que você aprendeu da análise da
amostra. Você também pode usar estatísticas inferenciais em situações em que simplesmente não pode se dar ao luxo de
coletar dados para toda a população. Nesse caso, você usaria os dados necessários para criar
inferências sobre a população em geral. Outras vezes, você pode se encontrar em situações em que
informações completas para a população não estão disponíveis. Nesses casos, você pode usar inferências
estatísticas para estimar valores para os dados ausentes com base no que você aprendeu ao analisar os dados
isso está disponível.

Para que uma inferência seja válida, você deve selecionar cuidadosamente sua amostra para obter uma verdadeira
representação da população. Mesmo que sua amostra seja representativa, os números no
 conjunto de dados de amostra sempre exibirá algum ruído - variação aleatória, em outras palavras - que
garante que a estatística da amostra não seja exatamente idêntica à estatística populacional correspondente.

## Distribuições de probabilidade

Imagine que você acabou de entrar em Las Vegas e se instalar na sua mesa de roleta favorita. Quando a roleta gira, você entende intuitivamente que existe uma igualdade é provável que a bola caia em qualquer um dos slots do cilindro na roda. O slot onde o
a bola vai pousar é totalmente aleatória e a probabilidade ou probabilidade da bola pousar em qualquer
slot sobre outro é o mesmo. Como a bola pode cair em qualquer slot, com igual probabilidade, há
uma distribuição de probabilidade igual ou uma distribuição de probabilidade uniforme - a bola tem igual
probabilidade de aterrissagem em qualquer das fendas do cilindro.
Mas os slots da roleta não são todos iguais - a roda possui 18 slots pretos e 20 slots
que são vermelhos ou verdes. Devido a esse arranjo, há uma probabilidade de 18/38 de que sua bola
vai pousar em um slot preto. Você planeja fazer apostas sucessivas para que a bola caia em um slot preto.

Seus ganhos líquidos aqui podem ser considerados uma variável aleatória, que é uma medida de uma característica ou
valor associado a um objeto, pessoa ou lugar (algo no mundo real) que seja
imprevisível. Como esse valor é imprevisível, não significa que você saiba
nada sobre isso. Além disso, você pode usar o que sabe sobre esse assunto para ajudá-lo em sua
tomando uma decisão. 

Uma média ponderada é o valor médio de uma medida em um número muito grande de pontos de dados. E se
você calcula uma média ponderada dos seus ganhos (sua variável aleatória) através da probabilidade
distribuição, isso renderia um valor esperado - um valor esperado para seus ganhos líquidos
ao longo de um número sucessivo de apostas. (Uma expectativa também pode ser considerada o melhor palpite, se você precisar adivinhar) Para descrevê-lo de maneira mais formal, uma expectativa é uma média ponderada de alguma medida associada a uma variável aleatória. Se seu objetivo é modelar uma variável imprevisível,
que você pode tomar decisões informadas por dados com base no que sabe sobre sua probabilidade em um
população, você pode usar variáveis aleatórias e distribuições de probabilidade para fazer isso.

Ao considerar a probabilidade de um evento, você deve saber quais são os outros eventos possíveis. Sempre defina o conjunto de eventos como mutuamente exclusivos - apenas um pode ocorrer a cada
Tempo. (Pense nos seis resultados possíveis de rolar um dado.) A probabilidade tem essas duas importantes
características:
* A probabilidade de qualquer evento único nunca fica abaixo de 0,0 ou excede 1,0.
* A probabilidade de todos os eventos sempre é exatamente igual a 1,0.

A distribuição de probabilidade é classificada de acordo com esses dois tipos:
* **Discreta:** Uma variável aleatória em que os valores podem ser contados por agrupamentos

* **Contínuo:** Uma variável aleatória que atribui probabilidades a um intervalo de valor. 

Para entender a distribuição discreta e contínua, pense em duas variáveis de um conjunto de dados
descrevendo carros. Uma variável "cor" teria uma distribuição discreta porque os carros têm
apenas uma gama limitada de cores (preto, vermelho ou azul, por exemplo). As observações seriam
contável pelo agrupamento de cores. Uma variável que descreve o consumo por litro dos carros "kpl" teria uma distribuição contínua porque cada carro poderia ter seu próprio valor separado para
"kpl".

* **Distribuições normais (contínua numérica):** Representadas graficamente por uma
curva modelada como um sino simétrico, essas distribuições modelam fenômenos que tendem a
observação (no topo do sino na curva do sino); observações nos dois extremos são menos
provável.

* **Distribuições binomiais (discretas numéricas):** modele o número de sucessos que podem ocorrer em um
certo número de tentativas quando apenas dois resultados são possíveis (a antiga moeda cara-ou-coroa)
cenário alternativo, por exemplo). Variáveis binárias - variáveis que assumem apenas um dos dois valores tem uma distribuição binomial.

* **Distribuições categóricas (não numéricas):** representam as categorias não numéricas
variáveis ou variáveis ordinais (um caso especial de variável numérica que pode ser agrupada e
classificados como uma variável categórica).

## Probabilidade condicional com Naïve Bayes

Você pode usar o método de aprendizado de máquina Naïve Bayes, que foi emprestado diretamente da
estatística, para prever a probabilidade de um evento ocorrer, com base nas evidências definidas em seu
recursos de dados - algo chamado probabilidade condicional. Naïve Bayes, que se baseia em
classificação e regressão, é especialmente útil se você precisar classificar dados de texto.
Para ilustrar melhor esse conceito, considere o conjunto de dados Spambase disponível nas UCIs
repositório de aprendizado de máquina [Spambase](https://archive.ics.uci.edu/ml/datasets/Spambase).
O conjunto de dados contém 4.601 registros de emails e, em seu último campo, designa se cada email é
Spam. Nesse conjunto de dados, você pode identificar características comuns entre emails de spam. Uma vez
você definiu recursos comuns que indicam email de spam, é possível criar um classificador Naïve Bayes
que prevê com segurança se um e-mail recebido é spam, com base na evidência empírica
suportado em seu conteúdo. Em outras palavras, o modelo prevê se um email é spam - o evento com base em recursos coletados a partir de seu conteúdo - a evidência.

Naïve Bayes vem nestes três sabores populares:
* **MultinomialNB:** use esta versão se suas variáveis (categóricas ou contínuas) descreverem
contagem de frequência discreta, como contagem de palavras. Esta versão do Naïve Bayes assume uma
distribuição multinomial, como geralmente ocorre com dados de texto. Exceto valores negativos.

* **BernoulliNB:** Se seus recursos forem binários, use o multinomial Bernoulli Naïve Bayes para criar
previsões. Esta versão funciona para classificar dados de texto, mas geralmente não é conhecida por apresentar um bom desempenho como o MultinomialNB. Se você deseja usar o BernoulliNB para fazer previsões de
variáveis contínuas, que funcionarão, mas primeiro é necessário subdividi-las em
agrupamentos de intervalos (também conhecidos como binning).

* **GaussianNB:** use esta versão se todos os recursos preditivos forem normalmente distribuídos. Não é uma
boa opção para classificar dados de texto, mas pode ser uma boa opção se seus dados contiverem ambos
valores positivos e negativos (e se seus recursos tiverem uma distribuição normal, é claro).

Antes de construir um classificador Bayes naturalmente, considere que o modelo possui uma suposição a priori. Suas previsões assumem que as condições passadas ainda são verdadeiras. Prevendo valores futuros
dos históricos gera resultados incorretos quando as circunstâncias atuais mudam.
