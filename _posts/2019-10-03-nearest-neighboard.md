---
layout: page 
title:  "K-Vizinhos Mais Próximos"
date:   2019-10-03 08:00:00 -0300
categories: pos uel nearest neighbors 
---

# K-Vizinhos Mais Próximos

[Binder: Example Nearest Neighbors](https://mybinder.org/v2/gh/marc-queiroz/data-science-from-scratch/master)


Imagine que você está tentando prever como eu vou votar nas próximas eleições presidenciais. Se você não sabe mais nada sobre mim (e se você tiver os dados), uma abordagem lógica é considerar como meus vizinhos estão planejando votar. Como eu moro no centro de Seattle, meus vizinhos estão planejando votar no candidato democrata, o que sugere que o “candidato Democrata” é um bom palpite pra mim também.

Agora, imagine que você saiba mais sobre mim do que somente onde eu moro — talvez você saiba minha idade, meus rendimentos, quantos filhos eu tenho, e assim por diante. Considerando que o meu comportamento é influenciado (ou caracterizado) por tais coisas ao máximo, considerar apenas meus vizinhos que estão próximos de mim em todas essas dimensões parece ser uma classificação melhor do que considerar todos os meus vizinhos. Essa é a ideia por trás da classificação dos vizinhos mais próximos.

## O Modelo

Os vizinhos mais próximos é um dos modelos preditivos mais simples que existe. Ele não possui premissas matemáticas e não requer nenhum tipo de maquinário pesado. Ele apenas requer:

* Uma noção de distância

* Uma premissa de que pontos que estão perto um do outro são similares

A maioria das técnicas que veremos neste livro consideram o conjunto de dados como um todo a fim de aprender padrões nos dados. Os vizinhos mais próximos, por outro lado, rejeitam muitas informações conscientemente, uma vez que a previsão para cada ponto novo depende somente de alguns pontos mais próximos.

Mais ainda, os vizinhos mais próximos provavelmente não vão lhe ajudar a entender os fatores determinantes de quaisquer fenômenos os quais você esteja considerando. Prever os meus votos baseados nos votos dos meus vizinhos não lhe diz muito sobre o que me faz votar do meu jeito, enquanto que algum modelo alternativo que prevê meu voto baseado (digamos) no meu salário e no meu estado civil talvez possa dizer.

Em uma situação geral, temos alguns pontos de dados e um conjunto de rótulos correspondentes. Os rótulos podem ser True e False, indicando se cada entrada satisfaz algumas condições como “é spam?” ou “é venenoso?” ou “seria prazeroso assistir?” Ou eles poderiam ser categorias, como classificações indicativas de filmes (L, 10, 12, 14, 16, 18). Ou eles poderiam ser nomes dos candidatos à presidência. Ou eles poderiam ser linguagens de programação preferidas.

No nosso caso, os pontos de dados serão vetores, o que significa que podemos usar a função distance (calcula distância euclidiana entre dois pontos).

Digamos que escolhemos um número k como 3 ou 5. Então, quando queremos classificar alguns novos pontos de dados, encontramos os pontos rotulados k mais próximos e os deixamos votar na nova saída.

Para fazer isso, precisaremos de uma função que conte os votos. Uma possibilidade é:
```python
def raw_majority_vote(labels):
  votes = Counter(labels)
  winner, _ = votes.most_common(1)[0]
  return winner
```

Mas isso não faz nada de inteligente com as relações. Por exemplo, imagine que estamos classificando os filmes e os cinco filmes mais próximos são classificados em L, L, 10, 10, 12. L e 10 têm dois votos. Nesse caso, temos várias opções:

* Escolher um dos vencedores aleatoriamente.

* Ponderar os votos à distância e escolher o vencedor mais votado.

* Reduzir *k* até encontrarmos um vencedor único.

Implementaremos o terceiro:

```python
def majority_vote(labels):
  """presume que as etiquetas são ordenadas do mais próximo para o mais distante"""
  vote_counts = Counter(labels)
  winner, winner_count = vote_counts.most_common(1)[0]
  num_winners = len([count for count in vote_counts.values()
        if count == winner_count])
  if num_winners == 1:
    return winner                      # vencedor único, então o devolve
  else:
    return majority_vote(labels[:-1]) # tenta novamente sem o mais distante
```


É certeza que esse método funcionará em algum momento, já que na pior 
das hipóteses reduziríamos para somente um rótulo e, nesse caso, 
ele vence.

Com essa função é fácil criar um classificador:
```python
def knn_classify(k, labeled_points, new_point):
  """cada ponto rotulado deveria ser um par (point, label)"""
  # organiza os pontos rotulados do mais próximo para o mais distante
  by_distance = sorted(labeled_points,
         key=lambda (point, _): distance(point, new_point))
  # encontra os rótulos para os k mais próximos
  k_nearest_labels = [label for _, label in by_distance[:k]]
  # e os deixa votar
  return majority_vote(k_nearest_labels)
```
Vamos ver como isso funciona.

## Exemplo: Linguagens Favoritas

O resultado da primeira pesquisa de usuários da DataSciencester está de volta,
 e descobrimos as linguagens deprogramação preferidas dos nossos
 usuários em algumas cidades grandes:

```python
# cada entrada é ([longitude, latitude], favorite_language)
cities = [([-122.3, 47.53], "Python"),  # Seattle
   ([ -96.85, 32.85], "Java"),   # Austin
   ([ -89.33, 43.13], "R"),      # Madison
   # … e assim por diante
]
```

O vice-presidente do Envolvimento Comunitário quer saber se podemos
usar esses resultados para prever a linguagem de programação preferida para
 lugares que não fizeram parte da pesquisa.

Como sempre, um primeiro bom passo é demarcar os dados (Figura 1):

![Figura 1. Linguagens de programação preferidas](/pos-uel-big-data/assets/nearest-neighbors/figura01.png "Figura 1. Linguagens de programação preferidas")
*Figura 1. Linguagens de programação preferidas*

```python

# a chave é a linguagem, o valor é o par (longitudes, latitudes)
plots = { "Java" : ([], []), "Python" : ([], []), "R" : ([], []) }
# queremos que cada linguagem tenha marcador e cor diferentes
markers = { "Java" : "o", "Python" : "s", "R" : "^" }
colors = { "Java" : "r", "Python" : "b", "R" : "g" }
for (longitude, latitude), language in cities:
  plots[language][0].append(longitude)
  plots[language][1].append(latitude)
# cria uma série de dispersão para cada linguagem
for language, (x, y) in plots.iteritems():
  plt.scatter(x, y, color=colors[language], marker=markers[language],
         label=language, zorder=10)
plot_state_borders(plt)      # finge que temos uma função que faça isso
plt.legend(loc=0)           # deixa matplotlib escolher o local
plt.axis([-130,-60,20,55])  # ajusta os eixos
plt.title("Linguagens de Programação Preferidas")
plt.show()
```
Já que os lugares mais perto tendem a gostar da mesma linguagem, os *k* vizinhos mais próximos parecem ser uma boa escolha para um modelo preditivo.

Para começar, vamos ver o que acontece se tentarmos prever a linguagem 
preferida de cada cidade usando seus vizinhos em vez da própria cidade:

```python
# tenta vários valores diferentes para k
for k in [1, 3, 5, 7]:
  num_correct = 0
  for city in cities:
  location, actual_language = city
  other_cities = [other_city
          for other_city in cities
          if other_city != city]
  predicted_language = knn_classify(k, other_cities, location)
  if predicted_language == actual_language:
     num_correct += 1
  print k, "neighbor[s]:", num_correct, "correct out of", len(cities)
```
Parece que três vizinhos mais próximos desempenham melhor, mostrando o 
resultado correto em 59% das vezes:

1  vizinho\[s\]:  40 certos  de  75

3  vizinho\[s\]:  44 certos  de  75

5  vizinho\[s\]:  41 certos  de  75

7  vizinho\[s\]:  35 certos  de  75

Agora podemos ver quais regiões seriam classificadas para quais linguagens 
dentro do esquema dos vizinhos mais próximos. Podemos fazer isso ao 
classificar uma rede inteira cheia de pontos como fizemos com as cidades:

```python
plots = { "Java" : ([], []), "Python" : ([], []), "R" : ([], []) }
k = 1 # or 3, or 5, or ...
for longitude in range(-130, -60):
for latitude in range(20, 55):
predicted_language = knn_classify(k, cities, [longitude, latitude])
plots[predicted_language][0].append(longitude)
plots[predicted_language][1].append(latitude)
```

Por exemplo, a Figura 2 mostra o que acontece quando olhamos apenas o vizinho mais próximo (k = 1).

![Figura 2. Linguagens de programação 1-vizinho mais próximo](/pos-uel-big-data/assets/nearest-neighbors/figura02.png "Figura 2. Linguagens de programação 1-vizinho mais próximo")

Vemos muitas mudanças abruptas de uma linguagem para outra com limites bem acentuados. Conforme aumentamos o número de vizinhos para três, vemos regiões mais flexíveis para cada linguagem (Figura 3).

![Figura 3. Linguagens de programação 3-vizinhos mais próximos](/pos-uel-big-data/assets/nearest-neighbors/figura03.png "Figura 3. Linguagens de programação 3-vizinhos mais próximos")

E conforme aumentamos os vizinhos para cinco, os limites ficam cada vez mais acentuados (Figura 4).

![Figura 4. Linguagens de programação 5-vizinhos mais próximos](/pos-uel-big-data/assets/nearest-neighbors/figura04.png "Figura 4. Linguagens de programação 5-vizinhos mais próximos")

Aqui, nossas dimensões são bastante comparáveis, mas se elas não fossem você talvez quisesse redimensionar os dados.

