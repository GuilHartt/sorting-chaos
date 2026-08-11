+++
title = '2.2. Selection Sort: A Arte da Escolha 🌰'
date = '2026-08-10T13:00:00-03:00'
weight = 2
draft = false
+++


Se o Bubble Sort funciona empurrando o maior valor para o final (como uma bolha), o **Selection Sort** (Ordenação por Seleção) faz o caminho oposto de forma muito mais direta: ele varre a lista, encontra o *menor* elemento de todos e o coloca na primeira posição. Depois encontra o segundo menor, e coloca na segunda posição, e assim por diante.

Imagine um esquilo faminto diante de uma pilha de nozes de tamanhos variados. Ele quer comer a menor noz primeiro para abrir o apetite. Ele olha todas as nozes da pilha, pega a menorzinha e a separa. Depois olha o que sobrou, pega a próxima menor e separa. Ele está fazendo um Selection Sort!

![Esquilo organizando nozes por tamanho](/images/esquilo.png)

---

## 🔍 Entendendo o Passo a Passo

Vamos usar os mesmos números caóticos do nosso exemplo anterior:

{{< array values="5, 3, 8, 4, 2" show_index="true" >}}

### Passada 1

O algoritmo começa na primeira posição (o índice 0, onde está o **5**). O objetivo é descobrir se existe algum número menor que ele no resto do array.

Nós guardamos o **5** como o "menor número encontrado até agora".
{{< array values="5, 3, 8, 4, 2" compare="0" show_index="true" >}}

Agora olhamos o **3**. O 3 é menor que 5? Sim. Então atualizamos nosso "menor número" para ser o 3.
{{< array values="5, 3, 8, 4, 2" compare="1" show_index="true" >}}

Olhamos o **8**. É menor que 3? Não.
Olhamos o **4**. É menor que 3? Não.
Olhamos o **2**. É menor que 3? Sim! 

{{< array values="5, 3, 8, 4, 2" compare="4" show_index="true" >}}

Terminamos de olhar a lista inteira. O menor número de toda a lista é, definitivamente, o **2**. Como ele é o menor de todos, nós o **trocamos** de lugar com o número que estava na primeira posição (o 5).

{{< array values="2, 3, 8, 4, 5" swap="0,4" show_index="true" >}}

🎉 **Fim da Passada 1!** O **2** está na sua posição definitiva. A primeira noz do esquilo foi separada com sucesso.

{{< array values="2, 3, 8, 4, 5" sorted="0" show_index="true" >}}

### Passada 2

Ignoramos a primeira posição (porque já está ordenada) e focamos no resto do array. O primeiro número não-ordenado agora é o **3**. Ele é o nosso candidato a menor.

{{< array values="2, 3, 8, 4, 5" sorted="0" compare="1" show_index="true" >}}

Olhamos o **8**. É menor que 3? Não.
Olhamos o **4**. É menor que 3? Não.
Olhamos o **5**. É menor que 3? Não.

Ao final, descobrimos que o **3** já era o menor elemento do resto da lista! Ele não precisa trocar de lugar com ninguém, apenas garantimos o lugar dele.

{{< array values="2, 3, 8, 4, 5" sorted="0,1" show_index="true" >}}

### Passada 3

Agora o primeiro não-ordenado é o **8**.
Olhamos o **4**. É menor que 8? Sim! Nosso menor agora é o 4.
Olhamos o **5**. É menor que 4? Não.

O menor número restante é o **4**. Vamos **trocá-lo** de lugar com o cara que estava no início (o 8).

{{< array values="2, 3, 4, 8, 5" swap="2,3" sorted="0,1" show_index="true" >}}

O **4** está no lugar definitivo!

{{< array values="2, 3, 4, 8, 5" sorted="0,1,2" show_index="true" >}}

### Passada 4 (Final)

Temos apenas o 8 e o 5. O primeiro é o **8**. Comparamos com o **5**. O 5 é menor.
Trocamos o 8 pelo 5.

{{< array values="2, 3, 4, 5, 8" swap="3,4" sorted="0,1,2" show_index="true" >}}

E automaticamente, se o 5 está no lugar certo, o 8 (sendo o último) também está! O caos foi derrotado novamente.

{{< array values="2, 3, 4, 5, 8" sorted="0,1,2,3,4" show_index="true" >}}

---

## 📜 Como fica no Código?

A implementação do Selection Sort exige uma lógica de rastreamento de índices. Vamos analisar como os laços refletem a estratégia de encontrar o menor valor.

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        indice_menor = i
        for j in range(i + 1, n):
            if arr[j] < arr[indice_menor]:
                indice_menor = j  # Atualiza a posição do menor elemento encontrado.
        arr[i], arr[indice_menor] = arr[indice_menor], arr[i]
        
    return arr
```

### 🧠 Dissecando a Lógica

O código do Selection Sort é um ótimo exemplo prático de como rastrear índices. Vamos olhar de perto como ele constrói essa lógica:

1. **Onde começa a desordem? (`for i in range(n)`)**:
   A variável `i` funciona como uma divisória entre a "área limpa" e a "área bagunçada" do array. Tudo à esquerda de `i` já está ordenado. O trabalho desse laço é apontar para o primeiro assento vazio e dizer: *"Agora precisamos encontrar quem vai sentar na cadeira número `i`"*.

2. **Quem é o menor? (`indice_menor = i`)**:
   Antes de varrer a área bagunçada, o algoritmo faz uma aposta segura. Ele assume que a pessoa que já está sentada na cadeira `i` é o menor valor restante. Se ele achar alguém menor pelo caminho, ele só precisa atualizar quem ganha esse índice.

3. **Olhando para o resto da fila (`for j in range(i + 1, n)`)**:
   - Não começamos a busca do zero porque o lado esquerdo do array já está pronto. E começamos de `i + 1` porque não faz sentido o elemento atual apostar corrida contra ele mesmo!
   - Durante a busca, se acharmos um valor (`arr[j]`) menor que o nosso campeão atual (`arr[indice_menor]`), nós não trocamos os valores de lugar imediatamente. Nós simplesmente anotamos a posição do novo vencedor: `indice_menor = j`.

4. **Trocando de lugar apenas uma vez**:
   A troca real (o *swap*) só acontece totalmente fora do laço interno, quando já temos certeza absoluta de que olhamos todos os candidatos. É isso que faz o Selection Sort ser tão elegante: ele economiza processamento e acessos à memória realizando apenas uma troca por rodada!

{{< aside >}}
Hoje em dia a gente nem pisca antes de mandar o computador trocar duas variáveis de lugar, mas nem sempre foi assim. Nos primórdios da computação, "escrever" dados em fitas magnéticas causava um desgaste físico real no equipamento, enquanto apenas "ler" era inofensivo. Exatamente por fazer o número mínimo absoluto de trocas, o Selection Sort era o verdadeiro herói do hardware na época, salvando a vida útil de máquinas gigantescas que custavam milhões de dólares!
{{< /aside >}}

## ⏳ Complexidade (Big O)

O Selection Sort é mais limpo que o Bubble Sort, pois ele faz muito menos *trocas*. No entanto, o número de *comparações* continua alto. 

Para encontrar o menor elemento na primeira vez, você olhou todos os `n` elementos. Na segunda vez, `n - 1`. Depois `n - 2`... No final, você fez operações proporcionais a **O(n²)**, independentemente do array estar bagunçado ou já ordenado (pois ele sempre tem que procurar até o fim para ter certeza de que encontrou o menor).

![Balança antiga medindo a complexidade O(n²)](/images/balanca.png)

O Selection Sort não é super veloz, mas é elegante e muito intuitivo. No próximo capítulo, vamos aprender o algoritmo que você (provavelmente) usa quando está ordenando cartas de baralho na sua mão!
