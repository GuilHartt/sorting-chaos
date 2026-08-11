+++
title = '2.1 Bubble Sort'
date = '2026-08-10T12:25:00-03:00'
weight = 1
draft = false
+++

Imagine que você está em uma fila desorganizada esperando por um café. Para resolver a bagunça, o responsável pelo atendimento estabelece uma nova regra: *"A fila precisa ser reorganizada por ordem de altura!"*

Como você organizaria todo mundo?

O **Bubble Sort** (ou Ordenação por Flutuação) tem uma ideia muito simples e orgânica. Você vai do início ao fim da fila comparando as pessoas duas a duas. Se a pessoa da frente for maior que a pessoa de trás, elas trocam de lugar.

![Copos de café em fila, trocando de lugar](/images/copos-cafe.png)

Ao fazer isso repetidas vezes, os maiores valores vão "borbulhando" para o final da fila, assim como bolhas de ar sobem até a superfície da água.

---

## 🔍 Entendendo o Passo a Passo

Vamos pegar um pequeno grupo de números totalmente caóticos:

{{< array values="5, 3, 8, 4, 2" show_index="true" >}}

Nosso objetivo é deixá-los em ordem crescente (do menor para o maior). Vamos iniciar o que chamamos de **Passada 1** (ou *Pass 1*).

### Passada 1

Começamos olhando para os dois primeiros elementos. Comparamos o **5** e o **3**.
{{< array values="5, 3, 8, 4, 2" compare="0,1" show_index="true" >}}

A regra é: se o número da esquerda for maior, eles trocam de lugar. 5 é maior que 3? Sim! Então **trocamos**.
{{< array values="3, 5, 8, 4, 2" swap="0,1" show_index="true" >}}

Agora, avançamos uma casa. Vamos comparar o **5** (que andou para a direita) com o **8**.
{{< array values="3, 5, 8, 4, 2" compare="1,2" show_index="true" >}}

O 5 é maior que o 8? Não. Então eles ficam exatamente onde estão.
Avançamos novamente. Comparamos o **8** e o **4**.
{{< array values="3, 5, 8, 4, 2" compare="2,3" show_index="true" >}}

O 8 é maior que 4? Sim! Então eles **trocam** de lugar.
{{< array values="3, 5, 4, 8, 2" swap="2,3" show_index="true" >}}

Por fim, comparamos o **8** (que continua andando) e o **2**.
{{< array values="3, 5, 4, 8, 2" compare="3,4" show_index="true" >}}

8 é maior que 2? Com certeza. Eles **trocam**.
{{< array values="3, 5, 4, 2, 8" swap="3,4" show_index="true" >}}

🎉 **Fim da Passada 1!** Percebeu o que aconteceu? O maior número de todos (o 8) flutuou como uma bolha gigante até o final do array. Agora sabemos com absoluta certeza que o último elemento está na posição correta. 

![Bolha gigante flutuando com o número 8](/images/bolhas.png)

### Passada 2

Precisamos repetir o processo, mas agora não precisamos mais checar a última posição, porque o 8 já está ordenado.

Voltamos para o início: Comparamos **3** e **5**.
{{< array values="3, 5, 4, 2, 8" compare="0,1" show_index="true" >}}
Não trocam.

Comparamos **5** e **4**.
{{< array values="3, 5, 4, 2, 8" compare="1,2" show_index="true" >}}
O 5 é maior, então **trocam**.
{{< array values="3, 4, 5, 2, 8" swap="1,2" show_index="true" >}}

Comparamos **5** e **2**.
{{< array values="3, 4, 5, 2, 8" compare="2,3" show_index="true" >}}
O 5 é maior, então **trocam**.
{{< array values="3, 4, 2, 5, 8" swap="2,3" show_index="true" >}}

🎉 **Fim da Passada 2!** Agora o 5 está no seu lugar definitivo.
{{< array values="3, 4, 2, 5, 8" sorted="3,4" show_index="true" >}}

### Passada 3

Começamos de novo com o que sobrou. Comparamos **3** e **4**. Não trocam.
Comparamos **4** e **2**. O 4 é maior, então **trocam**.

{{< array values="3, 2, 4, 5, 8" swap="1,2" show_index="true" >}}

🎉 **Fim da Passada 3!** O 4 encontrou seu lugar.

### Passada 4 (Final)

Comparamos **3** e **2**. O 3 é maior, então **trocam**.
{{< array values="2, 3, 4, 5, 8" swap="0,1" show_index="true" >}}

O array está completamente ordenado! A paz voltou ao caos.
{{< array values="2, 3, 4, 5, 8" sorted="0,1,2,3,4" show_index="true" >}}

---

## 📜 Como fica no Código?

A implementação do Bubble Sort exige dois laços de repetição aninhados. Vamos analisar o porquê de cada linha existir e, em especial, entender a matemática por trás dos limites desses laços.

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                
    return arr
```

### 🧠 Dissecando a Lógica

Se a transição do visual para o código ainda não clicou perfeitamente, não se preocupe. Vamos olhar de perto como essas peças se encaixam:

1. **O controle de passadas (`for i in range(n)`)**: 
   Pense nesse laço como o maestro da operação. Ele não mexe nos elementos, apenas dita quantas vezes precisamos percorrer a fila. Como no pior dos casos temos `n` elementos fora do lugar, ele nos dá `n` rodadas para garantir que cada bolha chegue ao topo.
   
2. **Ignorando o que já está pronto (`n - i - 1`)**:
   Aqui está a grande sacada matemática do algoritmo!
   - A cada volta que o maestro (`i`) completa, sabemos que um novo número alcançou o seu destino final lá na ponta direita.
   - A subtração `- i` serve para dizer pro código: *"Ei, poupe energia! Não precisa olhar o final da fila, a gente já arrumou essa parte nas passadas anteriores"*.
   - E o `- 1`? Como o código sempre compara o elemento atual (`j`) com o vizinho seguinte (`j + 1`), nós precisamos parar um passo antes da fronteira. Se formos até o fim, o `j + 1` vai tentar ler um espaço vazio, gerando um erro de programa.

3. **Trocando os elementos de lugar**:
   Em muitas linguagens antigas, você precisaria criar uma variável auxiliar para guardar um valor antes de trocá-lo. O Python permite fazer `arr[j], arr[j + 1] = arr[j + 1], arr[j]`. É uma forma super elegante e direta de trocar duas variáveis de lugar na mesma linha.

{{< aside >}}
A reputação do Bubble Sort é tão péssima no mundo da performance que o coitado virou até piada política. Em 2007, durante uma sabatina no Google, perguntaram ao então candidato à presidência dos EUA, Barack Obama: *"Qual é a melhor maneira de ordenar um milhão de inteiros?"*. Ele abriu um sorriso sarcástico e respondeu na lata: *"Acho que o Bubble Sort não seria o caminho certo!"*. A plateia de engenheiros foi à loucura. Se até um candidato a presidente sabe que ele é lento, nós também deveríamos.
{{< /aside >}}

## ⏳ Complexidade (Big O)

Vamos pensar juntos. Se tivermos **10 elementos**, faremos cerca de 10 comparações na primeira passada, 9 na segunda, 8 na terceira... isso dá um número de operações que cresce em proporção quadrada ao número de elementos. 

- **Pior Caso:** Se o array estiver totalmente ao contrário, teremos que fazer todas as comparações e trocas possíveis. Isso leva a um tempo de **O(n²)**.
- **Caso Médio:** Também é **O(n²)**.
- **Melhor Caso:** Se a lista já estiver ordenada, podemos adicionar um truque no código para parar mais cedo. Mesmo assim, a versão clássica que escrevemos olhará os elementos e custará **O(n²)**, embora uma versão otimizada leve **O(n)**.

O Bubble Sort é lento para listas grandes. Lembra da pilha de 1.000 livros? Em um Bubble Sort no pior caso, faríamos `1000 * 1000` = **1 milhão de comparações**! Haja café para esperar isso rodar.

![Caracol dormindo num computador lento O(n²)](/images/caracol.png)

Apesar de ser lento na vida real, ele é excelente para aprender a pensar em algoritmos. Nos próximos capítulos, vamos ver estratégias muito mais espertas que o Bubble Sort.
