+++
title = '1.1 Contando Operações'
date = '2026-08-11T12:00:00-03:00'
weight = 1
draft = false
+++

Entender a teoria do Big O é essencial, mas o verdadeiro benefício surge na prática: quando você olha para um algoritmo e consegue prever se ele continuará eficiente ou se ficará excessivamente lento à medida que a quantidade de dados cresce.

E como fazemos essa previsão? Nós contamos as operações que o computador precisa realizar. Mas não se preocupe, não vamos contar cada instrução de forma exata. Na verdade, a contagem é feita de um jeito prático e simplificado, focando apenas no comportamento geral e ignorando os detalhes menores.

### **\( O(1) \)**: Tempo Constante

Veja este trecho de código:

```python
def ler_primeiro_livro(estante):
    print(estante[0])
```

Não importa se a `estante` tem 10 livros ou 10 bilhões de livros. O computador sempre vai direto no primeiro espaço da memória e pega o valor. Ele dá **um único passo**. Aumentar os dados não muda em nada o trabalho do computador. Isso é o glorioso **\( O(1) \)**.

### **\( O(n) \)**: Tempo Linear

Agora, veja este:

```python
def ler_todos_os_livros(estante):
    for livro in estante:
        print(livro)
```

Se a estante tem 10 livros, o laço de repetição (o `for`) roda 10 vezes. Se tem 1.000 livros, roda 1.000 vezes. O tempo de execução cresce na mesma exata proporção que a entrada de dados. Como forma uma linha reta perfeita num gráfico, chamamos de **\( O(n) \)** (Tempo Linear).

### A Regra de Descartar Constantes

E se tivermos isso aqui?

```python
def procurar_em_secoes_independentes(estante):
    for livro in estante:
        print(livro)
        
    for livro in estante:
        print(livro)
```

O primeiro laço roda `n` vezes. O segundo roda mais `n` vezes. No total, fazemos `2n` operações, certo? 
Na escola, sim. Para o Big O, não.

Lembra da regra fundamental? **Jogue fora as constantes**. Nós cortamos o `2` e declaramos solenemente que esse código é apenas **\( O(n) \)**. Porque, quando `n` atinge a casa dos bilhões, um fator fixo de 2 não muda a inclinação natural do desastre. O que importa para nós é que o crescimento continua sendo uma linha reta, e não uma curva explosiva.

### **\( O(n^2) \)**: Tempo Quadrático e a Soma de Gauss

E quando a gente acaba precisando colocar um `for` dentro de outro `for`?

```python
def comparar_cada_livro_com_todos_os_outros(estante):
    for livro in estante:
        for outro_livro in estante:
            print(livro, outro_livro)
```

Para cada **um** livro do primeiro laço, o segundo laço é forçado a rodar **todos** os `n` livros. Você está multiplicando \( n \times n \). O resultado é a terrível curva **\( O(n^2) \)**.

![Hamster exausto correndo na roda de exercícios para ilustrar a repetição O(n²)](/images/hamster-roda.png)

{{< aside >}}
**E se o laço interno for diminuindo?**  
Muitas vezes, em algoritmos reais, o segundo laço (o laço interno) não percorre todos os itens em todas as voltas. Ele vai encolhendo. Na primeira iteração do laço principal, ele faz `n` verificações; na segunda, faz `n-1`; depois `n-2`, e assim por diante.  
A soma de todos esses passos decrescentes (uma Progressão Aritmética) resulta na clássica fórmula matemática de Gauss:
\[ \frac{n(n - 1)}{2} \]

Se expandirmos a equação, teremos:
\[ \frac{n^2 - n}{2} \]

E o que a notação Big O faz com divisões e termos menores, como aquele `- n`? Ela descarta. O termo \( n^2 \) domina o crescimento, a divisão por 2 é ignorada, e o código continua sendo implacavelmente classificado como **\( O(n^2) \)**.
{{< /aside >}}

Aprendeu a ler o código e caçar os loops escondidos? Ótimo. Agora vamos encarar o fantasma que assombra os calouros de computação no próximo subcapítulo: o maldito logaritmo.
