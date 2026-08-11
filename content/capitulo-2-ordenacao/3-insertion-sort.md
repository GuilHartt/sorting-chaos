+++
title = '2.3 Insertion Sort'
date = '2026-08-10T14:00:00-03:00'
weight = 3
draft = false
+++

Se você já jogou algum jogo de cartas onde precisava manter sua mão organizada (tipo Uno, Poker ou Truco), adivinhe só: **você já executou o algoritmo Insertion Sort mentalmente!**

Diferente do Bubble Sort (que empurra o maior pra frente) e do Selection Sort (que busca o menor lá no final), o **Insertion Sort** constrói a lista ordenada um pedacinho de cada vez, inserindo cada novo elemento na posição exata dele dentro da parte que já está arrumada.

Imagine que você está segurando um leque de cartas na mão esquerda. A sua mão esquerda tem as cartas já organizadas por valor. Quando você pega uma carta nova do baralho com a mão direita, o que você faz? Você corre os olhos da direita para a esquerda pelas cartas que já tem na mão, e "insere" a carta nova exatamente no buraco correto.

![Mão inserindo uma carta em um leque ordenado](/images/cartas-insertion.png)

---

## 🔍 Entendendo o Passo a Passo

Vamos usar os mesmos números caóticos de antes:

{{< array values="5, 3, 8, 4, 2" show_index="true" >}}

A regra de ouro aqui é: vamos imaginar que a primeira posição da lista (onde está o **5**) já é a nossa "mão esquerda organizada". Uma carta sozinha sempre está ordenada, certo? 

Então, nosso trabalho começa a partir da segunda carta.

### Inserindo a Carta 3

Nós olhamos para a próxima carta da pilha: o **3**. 
Onde ele entra na nossa mão (que só tem o **5**)? Como o 3 é menor que o 5, o 5 precisa dar um passinho para a direita para abrir espaço.

{{< array values="5, 3, 8, 4, 2" compare="1" hole="1" floating="1" show_index="true" >}}

Abrindo espaço (o 5 vai para a direita):
{{< array values="5, 5, 8, 4, 2" swap="1" hole="0" floating="0" floating_val="3" show_index="true" >}}

Pronto! Nossa mão organizada agora tem duas cartas: `[3, 5]`. O resto (`[8, 4, 2]`) continua bagunçado na mesa.

{{< array values="3, 5, 8, 4, 2" sorted="0,1" show_index="true" >}}

### Inserindo a Carta 8

A próxima carta da mesa é o **8**. 
Nós olhamos para a nossa mão (que tem o `[3, 5]`). O 8 é maior que o 5? Sim. Então ele já está no lugar certo, na ponta direita! Não precisamos empurrar ninguém.

{{< array values="3, 5, 8, 4, 2" compare="2" show_index="true" >}}

Nossa mão cresceu: `[3, 5, 8]`.

{{< array values="3, 5, 8, 4, 2" sorted="0,1,2" show_index="true" >}}

### Inserindo a Carta 4

Agora a coisa fica interessante. A próxima carta é o **4**.
Nós comparamos o 4 com o 8. O 4 é menor, então o 8 dá um passo para a direita.

{{< array values="3, 5, 8, 4, 2" compare="3" hole="3" floating="3" show_index="true" >}}

O 8 pula uma casa abrindo espaço:
{{< array values="3, 5, 8, 8, 2" swap="3" hole="2" floating="2" floating_val="4" show_index="true" >}}

Comparamos o 4 (nossa carta atual) com o 5. O 4 é menor, então o 5 também dá um passo para a direita.

{{< array values="3, 5, 5, 8, 2" swap="2" hole="1" floating="1" floating_val="4" show_index="true" >}}

Comparamos o 4 com o 3. O 4 é maior! Achamos o buraco dele, e encaixamos a carta lá.

Mão organizada: `[3, 4, 5, 8]`.

{{< array values="3, 4, 5, 8, 2" sorted="0,1,2,3" show_index="true" >}}

### Inserindo a Carta 2 (Última!)

Falta só o **2**. Ele é menor que todos os números da nossa mão.

{{< array values="3, 4, 5, 8, 2" compare="4" hole="4" floating="4" show_index="true" >}}

Ou seja, todo mundo vai ter que se espremer e dar um passo para a direita para abrir o primeiríssimo espaço para o 2 entrar.

{{< array values="3, 4, 5, 8, 8" swap="4" hole="3" floating="3" floating_val="2" show_index="true" >}}
{{< array values="3, 4, 5, 5, 8" swap="3" hole="2" floating="2" floating_val="2" show_index="true" >}}
{{< array values="3, 4, 4, 5, 8" swap="2" hole="1" floating="1" floating_val="2" show_index="true" >}}
{{< array values="3, 3, 4, 5, 8" swap="1" hole="0" floating="0" floating_val="2" show_index="true" >}}

E o 2 vai sentar lá na primeira cadeira.

🎉 **Mão perfeitamente organizada!**

{{< array values="2, 3, 4, 5, 8" sorted="0,1,2,3,4" show_index="true" >}}

---

## 📜 Como fica no Código?

A tradução dessa mecânica para código exige que pensemos no array como duas partes: uma sublista à esquerda (que cresce a cada iteração e está sempre ordenada) e os elementos restantes à direita.

O laço `for` avança sobre o array pegando uma "carta nova" por vez. Em seguida, um laço `while` faz o papel de olhar para trás (para a sublista ordenada) e arrastar todos os elementos maiores uma casa para a direita, liberando o exato espaço onde a carta atual deve ser inserida.

Veja a implementação:

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        carta_atual = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > carta_atual:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = carta_atual
        
    return arr
```

### 🧠 Dissecando a Lógica

O Insertion Sort tem uma cara diferente porque ele não apenas varre a fila, ele **arrasta** as coisas de lugar. 

1. **Pegando uma carta por vez (`for i in range(1, len(arr))`)**:
   Nós começamos no índice `1` (o segundo elemento) porque assumimos que a primeira carta (no índice `0`) já faz parte da nossa "mão" inicial. A partir daí, o laço de fora simplesmente puxa a próxima carta do baralho para organizá-la.

2. **Olhando para trás (`j = i - 1`)**:
   Sempre que pegamos uma `carta_atual`, nós precisamos compará-la com as cartas que já estão na nossa mão. A variável `j` serve exatamente para apontar para o vizinho imediato da esquerda e ir descendo até o início da fila.

3. **Abrindo espaço (`while j >= 0 and arr[j] > carta_atual`)**:
   Esse `while` é o coração do algoritmo. Enquanto a carta da nossa mão (`arr[j]`) for maior que a carta nova, nós movemos ela uma casa para a direita (`arr[j + 1] = arr[j]`). É literalmente o movimento físico de afastar as cartas para abrir um buraco.

4. **Encaixando no buraco (`arr[j + 1] = carta_atual`)**:
   Quando o laço de dentro termina (porque achamos uma carta menor ou batemos no início da fila), nós finalmente colocamos a `carta_atual` no buraco que ficou aberto.

{{< aside >}}
Imagine tentar testar o seu código sem um teclado ou monitor. A primeira menção formal ao algoritmo que hoje chamamos de Insertion Sort foi publicada em 1946 por John Mauchly, um dos engenheiros que construiu o ENIAC (o primeiro computador eletrônico do mundo). O mais fascinante e cômico é que, naquela época, para mandar o computador organizar uma lista, a equipe precisava literalmente espetar e desplugar dezenas de cabos grossos em um painel do tamanho de uma parede! Um "bug" no código podia ser apenas um cabo mal encaixado.
{{< /aside >}}

---

## ⏳ Complexidade (Big O)

O Insertion Sort tem uma característica que o torna especial entre os algoritmos de ordenação lentos: **ele se adapta à bagunça**.

- **Pior Caso:** A lista está invertida (`[5, 4, 3, 2, 1]`). Para cada elemento novo, temos que empurrar todos os outros. Isso nos dá uma montanha de trabalho e a complexidade bate em **O(n²)**, assim como seus primos Bubble e Selection.
- **Melhor Caso:** A lista já está ordenada (ou quase ordenada). Se a lista for `[1, 2, 3, 4, 5]`, o algoritmo só olha para o elemento anterior, vê que não precisa empurrar ninguém, e segue a vida. Ele faz apenas **O(n)** operações. Isso é absurdamente rápido!

![Escorregador deslizando velozmente O(n)](/images/escorregador.png)

É por causa desse comportamento brilhante no "melhor caso" que o Insertion Sort é usado na vida real dentro de algoritmos modernos muito mais complexos (como o Timsort, que é o padrão do próprio Python e do Java). Quando as listas que sobram ficam muito pequenininhas ou já quase ordenadas, os super-algoritmos "chamam" o humilde Insertion Sort para terminar o serviço de forma rápida e eficiente.
