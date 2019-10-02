---
layout: post
title:  "Cinco algoritmos de clusterização"
date:   2019-09-29 08:00:00 -0300
categories: pos uel ML machine learning
---

### Os 5 algoritmos de dados que os cientistas precisam conhecer

O clustering é uma técnica de aprendizado de máquina que envolve o agrupamento de
Os pontos de dados. Dado um conjunto de pontos de dados, podemos usar um cluster
algoritmo para classificar cada ponto de dados em um grupo específico. Em teoria,
pontos de dados que estão no mesmo grupo devem ter propriedades semelhantes
e / ou recursos, enquanto os pontos de dados em diferentes grupos devem ter
propriedades e / ou recursos altamente diferentes. O agrupamento é um método de
aprendizado não supervisionado e é uma técnica comum para dados estatísticos
análise usada em muitos campos.

Em Data Science, podemos usar a análise de clustering para obter informações valiosas
insights de nossos dados, vendo em quais grupos os pontos de dados se enquadram
quando aplicamos um algoritmo de agrupamento. Hoje, vamos ver 5
algoritmos de agrupamento populares que os cientistas de dados precisam conhecer e
seus prós e contras!

K-Means Clustering
------------------

K-Means é provavelmente o algoritmo de agrupamento mais conhecido. Está
ensinado em muita ciência de dados introdutória e aprendizado de máquina
aulas. É fácil entender e implementar em código! Confira a
gráfico abaixo para uma ilustração.

<figure>
<img src="/pos-uel-big-data/assets/algoritmos-clustering/figura01.gif" class="hz n o hy y ng nh td te" width="480" height="480" alt="" /><figcaption>K-Means Clustering</figcaption>
</figure>

1. <span id = "59c3"> Para começar, primeiro selecionamos um número de classes / grupos
    para usar e inicializar aleatoriamente seus respectivos pontos centrais. Para
    descobrir o número de classes a usar, é bom dar uma rápida
    observe os dados e tente identificar agrupamentos distintos. o
    pontos centrais são vetores do mesmo comprimento que cada ponto de dados
    vector e são os "X" no gráfico acima. </span>
2. <span id = "8d8c"> Cada ponto de dados é classificado calculando-se o
    distância entre esse ponto e cada centro de grupo e, em seguida,
    classificando o ponto do grupo cujo centro está mais próximo de
    </span>
3. <span id = "86c4"> Com base nesses pontos classificados, recalculamos o
    centro do grupo, tomando a média de todos os vetores no
    grupo. </span>
4. <span id = "2ff6"> Repita estas etapas para um número definido de iterações ou
    até que os centros do grupo não mudem muito entre as iterações. Você
    também pode optar por inicializar aleatoriamente os centros do grupo algumas vezes,
    e, em seguida, selecione a execução com a aparência mais adequada
    resultados. </span>

K-Means tem a vantagem de ser bem rápido, já que todos nós somos realmente
fazer é calcular as distâncias entre pontos e centros de grupo; muito
alguns cálculos! Portanto, possui uma complexidade linear  O (n).

Por outro lado, o K-Means tem algumas desvantagens. Em primeiro lugar você
tem que selecionar quantos grupos / classes existentes. Isso nem sempre é
trivial e idealmente com um algoritmo de agrupamento, queremos que ele descubra
para nós, porque o objetivo é obter algumas dicas de
os dados. K-means também começa com uma escolha aleatória de centros de cluster
e, portanto, pode produzir resultados diferentes de agrupamento em diferentes
execuções do algoritmo. Assim, os resultados podem não ser repetíveis e não ter
consistência. Outros métodos de cluster são mais consistentes.

K-Medians é outro algoritmo de agrupamento relacionado ao K-Means, exceto
em vez de recalcular os pontos centrais do grupo usando a média, usamos o
vetor mediano do grupo. Este método é menos sensível a valores discrepantes
(por causa do uso da mediana), mas é muito mais lento para conjuntos de dados maiores, como
a classificação é necessária em cada iteração ao calcular o vetor Mediana.

Agrupamento de deslocamento médio
---------------------

O agrupamento por turnos médios é um algoritmo baseado em janela deslizante que tenta
para encontrar áreas densas de pontos de dados. É um algoritmo baseado em centróide
significando que o objetivo é localizar os pontos centrais de cada
grupo / turma, que trabalha atualizando os candidatos aos pontos centrais a serem
a média dos pontos dentro da janela deslizante. Estes candidatos
As janelas são filtradas em um estágio de pós-processamento para eliminar
quase duplicatas, formando o conjunto final de pontos centrais e suas
grupos correspondentes. Confira o gráfico abaixo para obter uma ilustração.

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura02.gif" class = "hz no hy y ng nh td te" width = "324" height = "324" alt = "" /> <figcaption> Shift Clustering para uma única janela deslizante </figcaption>
</figure>

1. <span id = "8d9d"> Para explicar o deslocamento médio, consideraremos um conjunto de
    pontos no espaço bidimensional como na ilustração acima. Nós
    comece com uma janela deslizante circular centralizada no ponto C (aleatoriamente
    selecionado) e tendo raio r como o kernel. O desvio médio é um
    algoritmo de escalada que envolve a mudança deste kernel
    iterativamente a uma região de maior densidade em cada etapa até
    convergência. </span>
2. <span id = "cc56"> A cada iteração, a janela deslizante é deslocada
    para regiões de maior densidade, deslocando o ponto central para
    a média dos pontos dentro da janela (daí o nome). o
    densidade dentro da janela deslizante é proporcional ao número de
    pontos dentro dele. Naturalmente, mudando para a média dos pontos
    na janela, ele se moverá gradualmente para áreas de ponto mais alto
    densidade. </span>
3. <span id = "61f9"> Continuamos a deslocar a janela deslizante de acordo com
    a média até que não haja direção na qual uma mudança possa
    acomodar mais pontos dentro do kernel. Confira o gráfico
    acima; continuamos movendo o círculo até não aumentarmos
    a densidade (ou seja, número de pontos na janela). </span>
4. <span id = "1fd8"> Este processo das etapas 1 a 3 é realizado com muitos
    janelas deslizantes até que todos os pontos fiquem dentro de uma janela. Quando múltiplos
    janelas deslizantes se sobrepõem à janela que contém mais pontos
    preservado. Os pontos de dados são então agrupados de acordo com o
    janela deslizante em que residem. </span>

Uma ilustração de todo o processo, de ponta a ponta, com todos os
janelas deslizantes é mostrada abaixo. Cada ponto preto representa o centróide
de uma janela deslizante e cada ponto cinza é um ponto de dados.

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura03.gif" class = "hz no hy y ng nh td te" width = "432" height = "432" alt = "" /> <figcaption> processo inteiro de cluster de mudança de média </figcaption>
</figure>

Ao contrário do cluster K-means, não há necessidade de selecionar o número
de clusters quando o deslocamento médio descobre isso automaticamente. Isso é uma enorme
vantagem. O fato de os centros de cluster convergirem para os pontos
de densidade máxima também é bastante desejável, pois é bastante intuitivo
entender e se encaixar bem em um sentido naturalmente orientado a dados. A desvantagem
é que a seleção do tamanho / raio da janela "r" pode não ser trivial.

Clustering espacial de aplicativos com base em densidade (DBSCAN)
-------------------------------------------------- ------------------

O DBSCAN é um algoritmo clusterizado baseado em densidade semelhante ao deslocamento médio, mas
com algumas vantagens notáveis. Confira outro gráfico chique
abaixo e vamos começar!

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura04.gif" class = "hz no h y n n t t te" width = "675" height = "424" alt = "" /> <figcaption> DBSCAN Agrupamento de carinha sorridente </figcaption>
</figure>

1. <span id = "b636"> DBSCAN começa com um ponto de dados inicial arbitrário
    que não foi visitado. A vizinhança deste ponto é
    extraído usando uma distância epsilon ε (todos os pontos que estão dentro
    a distância ε são pontos de vizinhança). </span>
2. <span id = "7dab"> Se houver um número suficiente de pontos
    (de acordo com minPoints) dentro desse bairro, então o
    processo de cluster começa e o ponto de dados atual se torna o
    primeiro ponto no novo cluster. Caso contrário, o ponto será rotulado
    como ruído (mais tarde, esse ponto barulhento pode se tornar parte do
    grupo). Nos dois casos, esse ponto é marcado como "visitado". </span>
3. <span id = "a6f6"> Para este primeiro ponto no novo cluster, os pontos
    dentro de sua vizinhança ε também se tornam parte do mesmo
    grupo. Este procedimento de fazer todos os pontos no bairro ε
    pertencer ao mesmo cluster é repetido para todos os novos
    pontos que foram adicionados recentemente ao grupo de clusters. </span>
4. <span id = "17b3"> Este processo das etapas 2 e 3 é repetido até que todos
    pontos no cluster são determinados, ou seja, todos os pontos dentro do ε
    as vizinhanças do cluster foram visitadas e rotuladas. </span>
5. <span id = "c6e5"> Após concluir o cluster atual, um novo
    ponto não visitado é recuperado e processado, levando à descoberta
    de outro cluster ou ruído. Esse processo se repete até todos os pontos
    são marcados como visitados. Como no final disso todos os pontos foram
    visitados, cada ponto será marcado como pertencendo a um
    aglomerado ou ruído. </span>

O DBSCAN apresenta grandes vantagens sobre outros algoritmos de clustering.
Em primeiro lugar, ele não requer um número definido de pares de clusters. Isso também
identifica valores extremos como ruídos, ao contrário da mudança de média que simplesmente lança
em um cluster, mesmo que o ponto de dados seja muito diferente.
Além disso, ele pode encontrar tamanhos e formatos arbitrários
clusters muito bem.

A principal desvantagem do DBSCAN é que ele não funciona tão bem quanto os outros
quando os aglomerados são de densidade variável. Isso ocorre porque a configuração de
o limite de distância ε e minPoints para identificar a vizinhança
os pontos variam de cluster para cluster quando a densidade varia. este
desvantagem também ocorre com dados de alta dimensão, uma vez que novamente o
limiar de distância ε torna-se um desafio para estimar.

Cluster de expectativa-maximização (EM) usando modelos de mistura gaussiana (GMM)
-------------------------------------------------- --------------------------

Uma das principais desvantagens do K-Means é o uso ingênuo do valor médio
para o centro do cluster. Podemos ver por que essa não é a melhor maneira de fazer
coisas olhando para a imagem abaixo. No lado esquerdo, parece
bastante óbvio para o olho humano que existem dois grupos circulares com
raio diferente 'centrado na mesma média. K-Means não pode lidar com isso
porque os valores médios dos clusters estão muito próximos. K-Means
também falha nos casos em que os clusters não são circulares, novamente como um
resultado do uso da média como centro do cluster.

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura05.png" class = "hz no hy y ng nh td te" width = "357" height = "180" alt = "" /> <figcaption> Dois casos de falha para K-Means </figcaption>
</figure>

Os modelos de mistura gaussiana (GMMs) nos dão mais flexibilidade do que o K-Means.
Com os GMMs, assumimos que os pontos de dados são distribuídos gaussianos; esta
é uma suposição menos restritiva do que dizer que são circulares usando
O significativo. Dessa forma, temos dois parâmetros para descrever a forma do
clusters: a média e o desvio padrão! Tomando um exemplo em dois
dimensões, isso significa que os clusters podem ter qualquer tipo de
forma (já que temos um desvio padrão em ambos xey
instruções). Assim, cada distribuição gaussiana é atribuída a uma única
grupo.

Para encontrar os parâmetros do Gaussian para cada cluster (por exemplo, a média
desvio padrão), usaremos um algoritmo de otimização chamado
Expectativa – Maximização (EM). Dê uma olhada no gráfico abaixo como um
ilustração dos gaussianos sendo ajustados aos clusters. Então nós podemos
Prossiga com o processo de armazenamento em cluster Expectativa – Maximização usando
GMMs.

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura06.gif" class = "hz no h y n n t t te" width = "360" height = "309" alt = "" /> <figcaption> EM Armazenamento em cluster usando GMMs </figcaption>
</figure>

1. <span id = "b71b"> Começamos selecionando o número de clusters (como
    K-Means faz) e inicializar aleatoriamente a distribuição Gaussiana
    parâmetros para cada cluster. Pode-se tentar fornecer uma boa
    estimativa de estimativa dos parâmetros iniciais, observando rapidamente o
    dados também. Embora observe, como pode ser visto no gráfico acima, este
    não é 100% necessário, pois os gaussianos começam nosso muito pobre, mas são
    rapidamente otimizado. </span>
2. <span id = "78e6"> Dadas essas distribuições gaussianas para cada cluster,
    calcular a probabilidade de que cada ponto de dados pertença a um determinado
    grupo. Quanto mais próximo o ponto do centro de Gauss, mais
    provavelmente pertence a esse cluster. Isso deve fazer sentido intuitivo
    uma vez que, com uma distribuição gaussiana, estamos assumindo que a maioria dos
    os dados estão mais próximos do centro do cluster. </span>
3. <span id = "db56"> Com base nessas probabilidades, calculamos um novo conjunto
    de parâmetros para as distribuições gaussianas, de modo a maximizar
    as probabilidades de pontos de dados dentro dos clusters. Computamos
    esses novos parâmetros usando uma soma ponderada do ponto de dados
    posições, onde os pesos são as probabilidades do ponto de dados
    pertencentes a esse cluster específico. Para explicar isso visualmente, nós
    pode dar uma olhada no gráfico acima, em particular o amarelo
    cluster como um exemplo. A distribuição inicia aleatoriamente no
    primeira iteração, mas podemos ver que a maioria dos pontos amarelos são
    à direita dessa distribuição. Quando calculamos uma soma ponderada por
    as probabilidades, mesmo que haja alguns pontos próximos ao
    centro, a maioria deles está à direita. Assim, naturalmente, o
    a média da distribuição é mais próxima desse conjunto de pontos. Nós podemos
    veja também que a maioria dos pontos é "do canto superior direito para o canto inferior esquerdo".
    Portanto, o desvio padrão muda para criar uma elipse que
    é mais adequado a esses pontos, para maximizar a soma ponderada pela
    probabilidades. </span>
4. <span id = "e471"> As etapas 2 e 3 são repetidas iterativamente até
    convergência, onde as distribuições não mudam muito de
    iteração para iteração. </span>

Existem duas vantagens principais no uso de GMMs. Em primeiro lugar, os GMMs são muito mais
** flexível ** em termos de covariância de cluster que K-Means; devido ao
parâmetro de desvio padrão, os clusters podem assumir qualquer elipse
forma, em vez de ficar restrito a círculos. K-Means é na verdade um
caso especial de GMM no qual a covariância de cada cluster ao longo de
dimensões se aproxima de 0. Em segundo lugar, como os GMMs usam probabilidades, eles
pode ter vários clusters por ponto de dados. Portanto, se um ponto de dados estiver no
No meio de dois agrupamentos sobrepostos, podemos simplesmente definir sua classe
dizendo que pertence X por cento à classe 1 e Y por cento à classe 2. I.e
Os GMMs oferecem suporte à associação mista.

Clustering Hierárquico Aglomerado
-------------------------------------

Os algoritmos de cluster hierárquicos se enquadram em 2 categorias: top-down ou
debaixo para cima. Os algoritmos bottom-up tratam cada ponto de dados como um único
agrupar desde o início e, em seguida, mesclar sucessivamente (ou * aglomerado *)
pares de clusters até que todos os clusters tenham sido mesclados em um único
cluster que contém todos os pontos de dados. Cluster hierárquico de baixo para cima
é, portanto, chamado * cluster aglomerado hierárquico * ou * HAC *.
Essa hierarquia de clusters é representada como uma árvore (ou dendrograma). o
raiz da árvore é o cluster exclusivo que reúne todas as amostras, o
deixa os clusters com apenas uma amostra. Confira o gráfico
abaixo para obter uma ilustração antes de passar para as etapas do algoritmo

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura07.gif" class = "hz no hy y ng nh td te" width = "720" height = "324" height = "324" alt = "" /> <figcaption> Aglomerativa Clustering hierárquico </figcaption>
</figure>

1. <span id = "bd76"> Começamos tratando cada ponto de dados como um único
    cluster, ou seja, se houver X pontos de dados em nosso conjunto de dados, temos X
    clusters. Em seguida, selecionamos uma métrica de distância que mede a
    distância entre dois grupos. Como exemplo, usaremos * average
    ligação * que define a distância entre dois clusters para ser o
    distância média entre pontos de dados no primeiro cluster e dados
    pontos no segundo cluster. </span>
2. <span id = "5d0a"> Em cada iteração, combinamos dois clusters em um.
    Os dois clusters a serem combinados são selecionados como aqueles com o
    menor ligação média. Ou seja, de acordo com a distância selecionada
    métrica, esses dois clusters têm a menor distância entre cada
    outro e, portanto, são os mais semelhantes e devem ser
    combinado. </span>
3. <span id = "e1c6"> O passo 2 é repetido até chegarmos à raiz do
    árvore, ou seja, temos apenas um cluster que contém todos os pontos de dados. No
    Dessa forma, podemos selecionar quantos clusters queremos no final, simplesmente
    escolhendo quando parar de combinar os clusters, ou seja, quando pararmos
    construindo a árvore! </span>

O armazenamento em cluster hierárquico não exige que especifiquemos o número de
clusters e podemos até selecionar qual número de clusters fica melhor
desde que estamos construindo uma árvore. Além disso, o algoritmo não é
sensível à escolha da métrica de distância; todos eles tendem a funcionar
igualmente bem, enquanto que com outros algoritmos de agrupamento, a escolha de
métrica de distância é crítica. Um caso de uso particularmente bom de
métodos de cluster hierárquico é quando os dados subjacentes têm uma
estrutura hierárquica e você deseja recuperar a hierarquia; de outros
algoritmos de agrupamento não podem fazer isso. Essas vantagens da hierarquia
clustering têm o custo de menor eficiência, já que tem um tempo
complexidade de *O (n³)*, diferente da complexidade linear de K-Means e GMM.

-------------------------------------------------------------------------

Conclusão
----------

Esses são os 5 principais algoritmos de cluster que um cientista de dados deve
conhecer! Terminaremos com uma visualização incrível de quão bem esses
algoritmos e alguns outros são executados, cortesia do Scikit Learn! Muito legal
para ver como os diferentes algoritmos comparam e contrastam com diferentes
dados!

<figure>
<img src = "/pos-uel-big-data/assets/algoritmos-clustering/figura08.png" class = "hz no hy y ng nh td te" width = "2100" height = "1250" alt = "" />
</figure>
