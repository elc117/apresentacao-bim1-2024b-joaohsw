# Enigma de Einstein
O "Enigma de Einstein" é um famoso quebra-cabeça lógico que, segundo a lenda, teria sido criado por Albert Einstein (não existe nada que comprove isso). O enigma original propõe uma série de informações sobre cinco casas de cores diferentes, onde vivem cinco pessoas de nacionalidades diferentes, cada uma dessas pessoas tem um animal de estimação, fuma uma marca de cigarros e bebe uma bebida diferente e o objetivo do enigma é descobrir quem é o dono do peixe, a partir das pistas fornecidas.
# Resolução utilizando Prolog
A seguir vamos analisar uma versão simplificada do enigma resolvida utilizando Prolog. \
Problema: existem 3 casas alinhadas, cada uma com uma cor diferente: vermelha, verde e azul. 

- Em cada casa vive uma pessoa: Alice, Bob e Carla.
- Cada pessoa tem um pet: gato, cachorro, hamster.
- Bob vive na casa vermelha.
- A pessoa que tem um gato vive na casa do meio.
- Carla vive na casa ao lado da casa azul.
- A pessoa que vive na casa verde tem um cachorro.

Qual a cor, o morador e o pet de cada casa?

Solução em Prolog, usando listas:

`ao_lado(X, Y, List) :- nextto(X, Y, List). % X à esquerda de Y`\
`ao_lado(X, Y, List) :- nextto(Y, X, List). % Y à esquerda de X`

`solucao(Casas) :-`\
  `Casas = [_,casa(_,_,gato),_],`\
  `member(casa(_,verde,cachorro),Casas),`\
  `member(casa(_,azul,_),Casas),`\
  `member(casa(_,_,hamster),Casas),`\
  `member(casa(alice,_,_),Casas),`\
  `member(casa(bob,vermelha,_),Casas),`\
  `member(casa(carla,_,_),Casas),`\
  `ao_lado(casa(carla,_,_),casa(_,azul,_),Casas).`

  # Minha análise do código

  Inicialmente o código busca verificar se X e Y são adjacentes em uma lista\
  `ao_lado(X, Y, List) :- nextto(X, Y, List). % X à esquerda de Y`\
  `ao_lado(X, Y, List) :- nextto(Y, X, List). % Y à esquerda de X`

  Em seguida, cria-se uma lista Casas que é preenchida com a única posição que se tem certeza de acordo com o enunciado (gato na casa do meio)\
  `solucao(Casas) :-`\
  `Casas = [_,casa(_,_,gato),_],`

  Logo após, são listadas todas as informações do enunciado e o código utilizando o *predicado* member tenta correlacionar as informações *(tipo uma função que retorna um boolean)* \
  `member(casa(_,verde,cachorro),Casas),`\
  `member(casa(_,azul,_),Casas),`\
  `member(casa(_,_,hamster),Casas),`\
  `member(casa(alice,_,_),Casas),`\
  `member(casa(bob,vermelha,_),Casas),`\
  `member(casa(carla,_,_),Casas),`\

  Por fim, na última linha é feita a conferência se Carla vive ao lado da casa azul\
  `ao_lado(casa(carla,_,_),casa(_,azul,_),Casas).`


# Checagem no SWI-Prolog

Ao digitar a query `solucao(X).` no SWI-Prolog ele vai indicar que existe mais de uma solução, para descobrir de maneira simples a quantidade de soluções utilizamos a query `findall(X, solucao(X), Solucoes), length(Solucoes, Len).` que nos dá a resposta definitiva: 2 soluções sendo elas: **[[casa(carla, verde, cachorro), casa(alice, azul, gato), casa(bob, vermelha, hamster)]**, **[casa(bob, vermelha, hamster), casa(alice, azul, gato), casa(carla, verde, cachorro)]]**

# Fontes

https://stackoverflow.com/questions/42380563/finding-a-specific-sequence-of-elements-in-a-list-prolog
https://stackoverflow.com/questions/62094580/how-does-next-predicate-work-making-two-opposite-choices
https://www.reddit.com/r/prolog/comments/rava4a/understanding_member2_with_lists_in_predicates/
https://www.reddit.com/r/prolog/comments/f48grt/difference_between_predicate_and_function/#:~:text=You%20can%20treat%20predicate%20as,output%20(due%20to%20unification) \
https://dcm.ffclrp.usp.br/~augusto/teaching/ia/IA-Prolog-Introducao-Tutorial.pdf
https://pt.wikipedia.org/wiki/Problema_de_%22einstein%22
