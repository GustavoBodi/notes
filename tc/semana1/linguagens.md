# Linguagens

Dentro do assunto de linguagens, ou mais em geral Teoria da Computação
temos as seguintes definições e propriedades importantes:

* Símbolo.
* Palavra.
* Alfabeto.
* Operações sobre linguagens.

## Símbolo

Entende-se como símbolo uma representação, membro de um alfabeto.

## Palavra

Uma palavra é uma concatenação de símbolos que pertencem a um alfabeto.

## Linguagem

Conjunto de palavras constituídas a partir de um determinado alfabeto.

Exemplo de definição de linguagem:

Define-se alfabeto $\Sigma$ como: $\Sigma = \lbrace a, b, c, \dots, z \rbrace$

$L_1=\lbrace w\ |\ w \in \Sigma^* e\ |w|\ é\ par\ \rbrace$

$L_2=\lbrace w\ |\ w \in \Sigma^* e\ |w|\ é\ ímpar\ \rbrace$

## Concatenação

Uma concatenação pode ser definida como colocar um em seguida do outro,
retendo ordem, implicando em algo similar a uma tupla com capacidade de
crescimento. Esta operação está definida tanto para palavras e símbolos
quanto para conjuntos de linguagens.


Exemplo de concatenação:

Defina-se $a$ como: $conca$

Defina-se $b$ como: $tenacao$

$c = a \sdot b = concatenacao$

## Feixo de Kleene

O Feixo de Kleene é uma operação sobre o alfabeto, que retorna todos as
possíveis combinações daquele alfabeto e também a palavra vazia $\epsilon$.

Define-se a operação sobre alfabeto feixo de Kleene:

Dado um alfabeto:

$\Sigma_1 = \lbrace a, b \rbrace$

O valor subscrito inferiormente é somente para nomear este alfabeto.

Temos que:

$\Sigma^*_1 = \lbrace \epsilon, a, b, aa, ab, ba, bb, aaa, \dots \rbrace$

* Note a sempre inclusão da palavra vazia aqui.

Também pode-se definir a operação de outra forma muitíssimo útil:

$\Sigma^*_1 = \Sigma^0_1 + \Sigma^1_1 + \Sigma^2_1 + \dots$

Defina-se então para este alfabeto:

$\Sigma^n=$ Todos as palavras possíveis de tamanho $n$ dado este alfabeto.

Desta forma, teremos que:

$\Sigma^0_1 = \epsilon$

$\Sigma^1_1 = \lbrace a, b \rbrace$

$\Sigma^2_1 = \lbrace aa, ab, ba, bb \rbrace$

$\Sigma^3_1 = \lbrace aaa, aab, aba, abb, baa, bba, bab, bbb \rbrace$

### Feixo na linguagem

Pode-se aplicar o feixo também à linguagem diretamente:

$L_1^* = \Sigma_1^*$

Para uma linguagem definida por:

$L_1 = \lbrace w | w \in \Sigma^* \rbrace$

## Propriedade Fundamental

Note-se então que de acordo com as definições do Feixo de Kleene, dos
alfabetos e das linguagens, teremos que:

$L_1 \subseteq \Sigma^*$

Isto, claro, para quando a linguagem é composta por esse alfabeto.

## Palavras

Pode-se enumerar as palavras de um alfabeto:



## Operações sobre a linguagem

Defina-se a linguagem como:

$\Sigma=\lbrace a, b \rbrace$

$L_1 = \lbrace w | w \in \Sigma^* \rbrace$


### Filtragem por tamanho

$L_1^0 = \epsilon$

$L^1_1 = \lbrace a, b \rbrace$

$L^2_1 = \lbrace aa, ab, ba, bb \rbrace$

### Concatenação

Defina-se:

$L_1=\lbrace w\ |\ w \in \Sigma^* e\ |w|\ é\ par\ \rbrace$

$L_2=\lbrace w\ |\ w \in \Sigma^* e\ |w|\ é\ ímpar\ \rbrace$

Então a concatenação aqui:

$L_1 \cdot L_1 = L_1$

$L_2 \cdot L_2 = L_1 - \lbrace \epsilon \rbrace$

### Feixo de Kleene

Exemplo da definição do Feixo de Kleene:

$L_1^* = L_1^0 \cup L_1^1 \cup L_1^2 \cup \dots = L_1$

Note que somente é igual a $L_1$ no final, por causa da definição dada ao alfabeto e a linguagem.

## Conjuntos

As operações de conjuntos estão todas definidas para as linguagens e alfabetos.

Ex:

$L_1 \cup L_2 = \Sigma^*$

$L_1 \cap L_2 = \empty$ Detalhe: $((L = \empty) \neq (L = \lbrace \epsilon \rbrace))$

## Potência na concatenação

Esta operação está definida:

$a^n = a$ n vezes.

Exemplos::

$a^3 = aaa$

$(ab)^4 = abababab$

$a^0=\epsilon$

## Classes de Linguagem

$\Sigma = \lbrace a, b \rbrace$

$L_1 = \lbrace w | w \in \Sigma^*$ e $w$ começa com a e termina com $b \rbrace$

$L_2 = \lbrace a^nb^n | n \in \N \rbrace$

$L_3 = \lbrace a^i(ab)^ib^i | i \in \N \rbrace$
