+++
title = 'Capítulo 3: Recursividade'
date = '2026-08-12T09:50:00-03:00'
weight = 3
draft = false
+++

Imagine a seguinte situação: você ganha uma **Matrioska** autêntica (aquelas clássicas bonecas russas de madeira). Você sabe que dentro da menor bonequinha de todas existe uma joia escondida.

O problema? Ao abrir a primeira boneca, você encontra outra. E dentro dessa, outra. E assim por diante, num nível quase infinito de "bonecas dentro de bonecas".

Como você escreve um algoritmo para encontrar a joia?

Existem duas formas principais de pensar para resolver esse problema.

### Abordagem Iterativa

A primeira forma é usar os laços de repetição clássicos (como o `while` ou `for`). Você cria uma pilha física de bonecas para abrir e entra num ciclo:

1. Pegue uma boneca da pilha.
2. Abra a boneca.
3. Se você encontrar a joia, ótimo! Você terminou.
4. Se encontrar *outra* boneca lá dentro, jogue-a na sua pilha para olhar depois.
5. Repita o processo até a pilha de tarefas acabar.

Isso funciona. É prático e seguro. No entanto, a lógica para controlar essa "pilha de tarefas" iterativamente pode se tornar complexa e difícil de ler rapidamente.

### Abordagem Recursiva

A segunda forma é usar a **Recursividade**. Uma função recursiva é, de forma simples, uma função de código que *chama a si mesma*. O algoritmo recursivo é projetado para operar assim:

1. Abra a boneca.
2. Se encontrar a joia, o problema está resolvido.
3. Se encontrar outra boneca, execute esta exata mesma lista de instruções para a nova boneca.

O código fica consideravelmente mais simples e limpo, pois você não precisa gerenciar uma lista manual de tarefas a verificar. A própria arquitetura do computador faz isso por você.

![Ilustração de Matrioskas sendo abertas sucessivamente revelando uma pequena joia](/images/matrioska.png)

A recursividade é uma das ferramentas matemáticas mais poderosas da programação, mas também exige atenção redobrada. Se você a projetar de forma incorreta e esquecer de definir a condição de parada, a função continuará executando até causar um colapso na memória do computador.

Nos próximos subcapítulos, vamos destrinchar como o sistema gerencia essa memória por meio da **Pilha de Chamadas** e como construir algoritmos recursivos de maneira segura.
