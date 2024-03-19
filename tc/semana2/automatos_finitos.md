# Teoria da Computação

Problema

* Representação do Problema.
* Linguagem.
* Verificação de instância. -- Sim ou Não
* Máquina -- Conguração -- Computação

## Intuição do conceito

Existem dois potes, um de três litros e um de quatro litros, deve-se a
partir das opções de esvaziamento e transferência determinar sequência que
terminem com o pote de quatro litros com 2 litros e o de 3 litros vazio.

Defina-se as seguintes operações:

| Operação | Descrição |
| - | - |
| $e_3$  | Encher pote 3 |
| $e_4$  | Encher pote 4 |
| $v_3$  | Esvaziar pote 3 |
| $v_4$  | Esvaziar pote 4 |
| $d_{34}$ | Derramar o conteúdo de 3 em 4 |
| $d_{43}$ | Derramar o conteúdo de 4 em 3 |

Esta pode ser uma das soluções do problema:

* $(0, 0)$ -- Estado Inicial
* $(4, 0)$ -- $e_4$
* $(1, 3)$ -- $d_{43}$
* $(1, 0)$ -- $v_3$
* $(0, 1)$ -- $d_{43}$
* $(4, 1)$ -- $e_4$
* $(2, 2)$ -- $d_{43}$
* $(2, 0)$ -- $e_3$

Desta forma, temos aqui um alfabeto que consiste das operações:

| Estado/Ação | $e_4$ | $e_3$ | $v_4$ | $v_3$ | $d_{43}$ | $d_{34}$ |
| - | - | - | - | - | - | - |
| $\rightarrow(0, 0)$ | $(4, 0)$ | $(0, 3)$ | $-$ | $-$ | $-$ | $-$ |
| $(4, 0)$ | $-$ | $(4, 3)$ | $(0, 0)$ | $-$ | $(1, 3)$ | $-$ |
| $(0, 3)$ | $(4, 3)$ | $-$ | $-$ | $(0, 0)$ | $-$ | $(3, 0)$ |
| $(4, 3)$ | $-$ | $-$ | $(0, 3)$ | $(4, 2)$ | $-$ | $-$ |
| $(1, 3)$ | $(4, 3)$ | $-$ | $(0, 3)$ | $(1, 0)$ | $-$ | $(4, 0)$ |
| $(3, 0)$ | $(4, 0)$ | $(3, 3)$ | $(0, 0)$ | $-$ | $(0, 3)$ | $-$ |
| $(1, 0)$ | $(4, 0)$ | $(1, 3)$ | $(0, 0)$ | $-$ | $(0, 1)$ | $-$ |
| $(3, 3)$ | $(4, 3)$ | $-$ | $(0, 3)$ | $(3, 0)$ | $-$ | $(4, 2)$ |
| $(0, 1)$ | $(4, 1)$ | $(0, 3)$ | $-$ | $(0, 0)$ | $-$ | $(1, 0$ |
| $(4, 2)$ | $-$ | $(4, 3)$ | $(0, 2)$ | $(4, 0)$ | $(3, 3)$ | $-$ |
| $(4, 1)$ | $-$ | $(4, 3)$ | $(0, 1)$ | $(4, 0)$ | $(2, 3)$ | $-$ |
| $(0, 2)$ | $(4, 2)$ | $(0, 3)$ | $-$ | $(0, 3)$ | $-$ | $(2, 0)$ |
| $(2, 3)$ | $(4, 3)$ | $-$ | $(0, 3)$ | $(2, 0)$ | $-$ | $(4, 1)$ |
| $(2, 0)$ | $(4, 0)$ | $(2, 3)$ | $(0, 0)$ | $-$ | $(0, 2)$ | $-$ |
| $-$      | $-$ | $-$ | $-$ | $-$ | $-$ | $-$ |

Detalhe: A seta $\rightarrow$ indica o estado inicial do sistema.

## Avaliar

Avaliando-se a seguinte palavra, teremos que:

* $w = e_3d_{43}e_3d_{34}v_4d_{34}$

| $e_3$ | $d_{34}$ | $e_3$ | $d_{34}$ | $v_4$ | $d_{34}$ | |
| - | - | - | - | - |  - | - |
| $(0, 0)\rightarrow$ | $(0, 3)\rightarrow$ | $(3, 0)\rightarrow$ | $(3, 3)\rightarrow$ | $(4, 2)\rightarrow$ | $(0, 2)\rightarrow$ | $(2, 0)$ |

* Como $(2, 0)$ é estado de aceitação, o resultado é sim.

Neste exemplo não é instância de linguagem:

| $v_4$ | $v_3$ | $d_{34}$ | $e_3$ | |
| - | - | - | - | - |

### Configuração

Foto da máquina em um estado do seu processo.

$[(0, 0), e_3d_{34}e_3d_{34}v_4d_{34}] \dashv$

$[(0, 3), d_{34}e_3d_{34}v_4d_{34}] \dashv$

$[(3, 0), e_3d_{34}v_4d_{34}] \dashv$

$[(3, 3), d_{34}v_4d_{34}] \dashv$

$[(4, 2), v_4d_{34}] \dashv$

$[(0, 2), d_{34}] \dashv$

$[(2, 0), \epsilon] \dashv$

Essa sequência de configurações de um estado inicial até um estado final
define uma computação.

## Máquina

$L_1=\lbrace w|w \in \Sigma^*\ \exist\ \delta(0,0) \rightarrow (2, 0) \rbrace$

A partir dessa linguagem definiremos uma máquina:

$M = (K, \Sigma, \delta, q_0, F)$

Os valores podem ser definidos por:

| - | $K$ | $\Sigma$ | $\delta$ | $q_0$ | $F$ |
| - | - | - | - | - | - |
| Definição | Conjunto finito de estados | Conjunto finito não vazio de símbolos de entrada (alfabeto) | Conjunto de todas as transições | Estado Inicial | Conjunto de Estados de Aceitação |

$\delta(K\times \Sigma)\rightarrow K$, estado e símbolo define uma transição, o operador em questão é um produto cartesiano.

Sendo que:

$q_0 \in K$

$F \sube K$

$\delta(q_0, w)\rightarrow F$ , descreve-se como: saindo de um estado
inicial com um palavra, chega-se em um estado de aceitação.

## Exemplos de Máquinas

$L_1 \lbrace w | w \in \Sigma^* e\ \exist \delta(q_0, w)\rightarrow w_F \in F$

$\Sigma = \lbrace a, b \rbrace$

$\Sigma^* = \lbrace \epsilon, a, b , aa, ab, ba, bb , \dots \rbrace$

Crie então uma máquina que reconhece $\Sigma^*$.

$M = (K, \Sigma, \delta, q_0, F)$

| ação/estado | a | b |
| - | - | - |
| $\rightarrow q_0^*$ | $q_0$ | $q_0$ |

Importante: $*$ Significa que é um estado de aceitação.

| a | a | b | |
| - | - | - | - |

$[q_0, aab] \vdash [q_0, ab] \vdash [q_0, a] \vdash [q_0, \epsilon]$

$K = \lbrace q_0 \rbrace$

$\Sigma = \lbrace a, b \rbrace$

$\delta = \lbrace(q_0, a) \rightarrow q_0,\ (q_0, b) \rightarrow q_0 \rbrace$

$q_0 = q_0$

$F = q_0$

