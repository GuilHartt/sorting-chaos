+++
title = 'Capítulo 1: O Caos do Dia a Dia e o Big O'
date = '2026-08-10T12:10:00-03:00'
weight = 1
draft = false
+++


Imagine que você está na biblioteca da sua faculdade na véspera da prova final de Cálculo. Você precisa desesperadamente do livro *"Cálculo - Volume 1"*.

Você chega à seção de matemática e se depara com a seguinte cena: a bibliotecária deixou cair todos os mil livros de matemática no chão. Uma pilha caótica, sem ordem alguma.

![Montanha caótica de livros de matemática](/images/pilha-de-livros.png)

Como você encontra o livro que precisa?
Você pega o primeiro livro da pilha. É Cálculo? Não. Joga para o lado.
Pega o segundo. É Cálculo? Não. Joga para o lado.

Você está executando um **algoritmo**, uma série de passos para resolver um problema. E neste caso, você está executando um algoritmo de **Busca Simples** (ou busca linear). 

Se o livro for o último da pilha de 1.000 livros, você terá que olhar 1.000 livros. Se a pilha tivesse 1.000.000 de livros, no pior dos casos, você olharia um milhão de livros!

---

## ⏳ A Notação Big O

Na Ciência da Computação, nós não medimos a velocidade de um algoritmo em segundos. Dependendo do seu computador (se é um PC da Xuxa ou um supercomputador da NASA), os segundos mudam. 

Nós medimos a velocidade em **crescimento do número de operações**. E para isso usamos a notação **Big O** (ou "Grande O").

O Big O diz o quão rápido o tempo de execução de um algoritmo aumenta à medida que o tamanho da entrada (a pilha de livros) aumenta.

![Gráfico da Notação Big O O(n)](/images/grafico-big-o.png)

### O(n) - Tempo Linear

No nosso exemplo da busca na pilha de livros, se temos `n` livros, no pior dos casos faremos `n` verificações. Chamamos isso de tempo de execução **O(n)**. O "O" significa *Order of magnitude* e o "n" é a quantidade de itens. 

Se a pilha dobrar de tamanho, o tempo que você leva para achar o livro também dobra. O tempo cresce *linearmente*.

### E se os livros estivessem ordenados?

Agora imagine que a bibliotecária já arrumou os livros e os colocou na prateleira, perfeitamente ordenados em ordem alfabética, do A ao Z.

Você precisa procurar livro por livro desde a letra A? Claro que não! Você vai direto no meio da estante, vê onde está a letra C (de Cálculo) e descarta metade dos livros. 

![Estante sendo cortada ao meio por tesoura](/images/tesoura-estante.png)

Isso é uma **Busca Binária**, que tem um tempo de execução de **O(log n)**. Mas espere! Para fazermos uma busca binária incrível e rápida, os dados *precisam* estar ordenados!

É por isso que a ordenação (Sorting) é tão importante. Sem ela, o caos reina. Nos próximos capítulos, vamos ver como domar esse caos e colocar as coisas em ordem.
