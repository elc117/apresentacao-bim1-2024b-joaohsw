# Enigma de Einstein
O "Enigma de Einstein" é um famoso quebra-cabeça lógico que, segundo a lenda, teria sido criado por Albert Einstein (não existe nada que comprove isso). O enigma original propõe uma série de informações sobre cinco casas de cores diferentes, onde vivem cinco pessoas de nacionalidades diferentes, cada uma dessas pessoas tem um animal de estimação, fuma uma marca de cigarros e bebe uma bebida diferente e o objetivo do enigma é descobrir quem é o dono do peixe, a partir das pistas fornecidas.
# Resolução utilizando Prolog
Problema: existem 3 casas alinhadas, cada uma com uma cor diferente: vermelha, verde e azul.

- Em cada casa vive uma pessoa: Alice, Bob e Carla.
- Cada pessoa tem um pet: gato, cachorro, hamster.
- Bob vive na casa vermelha.
- A pessoa que tem um gato vive na casa do meio.
- Carla vive na casa ao lado da casa azul.
- A pessoa que vive na casa verde tem um cachorro.

Qual a cor, o morador e o pet de cada casa?

Solução em Prolog, usando listas:

`ao_lado(X, Y, List) :- nextto(X, Y, List). % X à esquerda de Y
ao_lado(X, Y, List) :- nextto(Y, X, List). % Y à esquerda de X

solucao(Casas) :-
  Casas = [_,casa(_,_,gato),_],
  member(casa(_,verde,cachorro),Casas),
  member(casa(_,azul,_),Casas),
  member(casa(_,_,hamster),Casas),
  member(casa(alice,_,_),Casas),
  member(casa(bob,vermelha,_),Casas),
  member(casa(carla,_,_),Casas),
  ao_lado(casa(carla,_,_),casa(_,azul,_),Casas).`
