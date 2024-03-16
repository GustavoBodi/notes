# Sistemas Operacionais I 

Fundamentos, histórico e arquitetura de núcleo.

## Introdução

Definição: Sistema  de computação
* Sistema para execução de programas de usuário.

Programas:
* Utilizam Disco, Memória, E/S.

A definição mostrada nos slides é pobre e deficitária, com um pouco de
pesquisa, descrevo da seguinte maneira: Sistema de gerência de recursos
para programa de usuário que interage com hardware e software.

Versão simplificada da interação entre os componentes, programa, S.O. e hardware.

| Hierarquia |
| - |
| Programas |
| S.O. |
| Hardware |

### Programas

Há essencialmente dois tipos de programas, aqueles ditos de aplicativos e
de sistema. Os aplicativos são os programas do dia a dia que normalmente
não tem uma relação estrita e fundamental com o S.O. Já os programas de
sistemas têm uma relação mais profunda, interagindo diretamente (por vezes)
com as chamadas do S.O. em âmbito de abstração.

* Programas Aplicativos: Word, Firefox, ...
* Programas de Sistema: Gerenciados de Tarefas (Windows), ps (linux), ...

Aqui fica âmbiguo se as próprias API's de sistema operacional seriam um
programa de sistema, já que são abstrações por si próprias.

### Aspectos

O S.O tem como objetivo maximizar o uso do hardware (distribuição de
recursos), e ainda criar um ambiente conveniente por meio da criação de
abstrações.


| Interface entre Usuário e Hardware | Usuário |
| - | - |
| Aplicativos | Usuário Final / Programador |
| Utilitários | Programador |
| Sistema Operational | Programador |
| Hardware | Projetista S.O. |


## Serviços de S.O.

Alguns dos serviçoes fundamentais do S.O são diretamente relacionados com a
gerência de recursos:

* Carregar e descarregar programas na memória.
* Gerência de arquivos.
* Gerência de periféricos e utilização.
* Gestão de usuários.
* Proteção de usuários.
* Interface com o usuário.
* Detecção de erros (hardware e programas).

## Tipos de Sistemas

Há uma de facto evolução nas abstrações de S.O. (ou ausência dele) que
possibilitaram uma maior simplicidade na criação de aplicativos e interação
com o Hardware.

### Iniciais

Por uma falta de descrição mais precisa ou simples desleixo para com a precisão, foi
assim que o professor apresentou e fizera os slides.

* Usuário deve programar e operar o computador (ENIAC).
* Alocação de memória feita por planilha.
* S.O inexistente.

Prolemas:

* Péssima utilização de recursos.
* Muito difícil

### Sistemas em Lote (Batch)

Passa a existir uma separação entre os operadores e usuários.

Surge um novo conceito: Jobs.

* Entende-se que um job é um programa que é compilado e executado, além disso, passa-se a criar lotes de programas de acordo com a necessidade do usuário.
* A alternância ainda era feita de forma manual.
* Os jobs eram organizados em lotes (batches), por seu tipo, necessidade,
  compilador e outros aspectos. Perceba que esse aspecto tem a melhor
  relação com o nome, não faça confusão com o sistema monitor residente. As
  alternâncias e trabalho manual ainda são predominante característica.

### Sistema com Monitor Residente

Efetivamente um sistema que contém um S.O. rudimentar.

* O programa monitor-residente é colocado na memória que transfere o processamento de um job para o outro (automaticamente).
* Ao término do job, o controle volta para o programa monitor-residente.
* Neste tipo de S.O. só consegue-se executar apenar um job por vez.

Extrai-se dessas características básicas que o monitor-residente é uma
evolução no entendimento de se tornar um programa na memória, mas
principalmente, pela automatização da mudança entre os Jobs. Um detalhe
inocente, mas que demonstra a inevitável transformação deste programa no
que viria a ser os sistemas operacionais modernos.

### Sistemas de Multiprogramação

Múltiplos programas estão carregados na memória, existindo assim, uma
melhor utilização de recursos. Programas aguardam os recursos um dos
outros.

* O que possibilitou a existência desse tipo de sistema foi o surgimento
  das interrupções de hardware e discos magnéticos.
* É junto com o sistema com Timesharing, aqueles que implementam
  preemptividade.
* Temos pois um programa logicamente ativo e vários programas logicamente
  inativos.

### Sistemas com Timesharing

São os sistemas operacionais utilizados hoje em dia, consistem em
transferir a execução de um programa para o outro rapidamente, criando a
ilusão de que estão sendo executados de forma paralela. Este tipo de
sistema, naturalmente, é baseado na preempção constante e utilização de
interupções. O que se torna primordial é a grande necessidade de se
obter um rápido tempo de resposta, ou seja não há a necessidade de se
executar grandes blocos de código por vez, mas definitivamente deve-se
alterar consistentemente quais programas estão fazendo uso da CPU para que
haja uma certa fluidez ou ilusão da mesma ao usuário.

### Sistemas de Tempo Real

É um tipo de sistema com uso em aplicações onde o tempo de resposta é
fundamental. É utilizada na aviação, em sondas, satélites e outros
programas que apresentam tempo de resposta previsíveis. Ao se olhar para
esse tipo de sistema, pode-se ter a ideia de que suas propriedades não dão
nenhuma garantia importante, no entanto essa visão é equivocada, dado que o
tempo de resposta faz-se procurado quando estamos lidando com programas
orientados a eventos que necessitam de garantias de execução e
previsibilidade que os outros S.Os não detêm por excelência.

* Sistemas de tempo real são preemptivos e normalmente são construídos com
  scheduling baseado em prioridade.

## Monotarefa e Multitarefa

Paralelo aos tipos de sistemas apresentados anteriormente, surge o conceito
de monotarefa e multitarefa. Vale dizer que essa classificação é
autoevidente dado o conhecimento prévio dos tipos de sistema, no entanto
para o caso de esquecimento, coloca-se a enumeração de sua definição:

* Monotarefa: Somente um programa logicamente ativo.
-- Somente os sistemas iniciais eram desse tipo.
* Multitarefa: Múltiplos programas logicamente ativos. -- Sistemas multiprogramados, com timesharing, em lote, monitor-resitente e tempo real.

### Multitarefas

Já que não bastasse as definições óbvias colocadas acima, existem ainda
outro tipo de definição fora da razoabilidade do intelecto, coloca-se aqui
sistemas preemptivos e não-preemptivos. Como se não já o tivesse feito,
realizo novamente a enumeração por uma questão de conveniência e obviamente
por almejar reeditar toda a folhar que copiei durante a aula.

* Não preemptivo: Executa do inicio ao fim sem interrupções: Sistemas em lote e monitor-residente.
* Preemptivo: Executa parando o programa no meio via interrupções: Timesharing e multiprogramados.


## Estruturas do Núcleo

Passo então a apresentar ao leitor dese texto a abstração efetiva do S.O,
ou se preferir, estrutura intrínseca do Kernel. Aqui teremos dois tipos de
de modos de operação. Modo Núcleo que apresenta a capacidade de executar
qualquer instrução, e o modo Usuário que detêm somente um subconjunto das
operações que o Kernelmode pode executar. Reflita que a existência de ambos
não é somente um parâmetro de segurança, mas também um de abstração que têm
implicações em todo o design posterior nas camadas acima de aplicação. Por
desing, os programas de usuário rodam em modo Usermode, escrever esta frase
definitivamente implicou em queima de alguns dos meus neurônios.

Segue abaixo uma tabela do papel do usermode e kernelmode em nossa
abstração inicial dos sistemas.

| Camada | Modo de execução |
| - | - |
| Interface do usuário | Usermode |
| Sistema Operacional | Kernelmode |
| Hardware |  |

Ao leitor que prestou atenção, percebeu que a frase acima é mentirosa, já
que esta tabela é diferente do que fora apresentado nos tópicos
anteriorers. Claro, que dentro das questões didático-pedagógicas, as aulas
seriam apresentadas sem trazer nenhum tipo de consistência lógica.

De qualquer maneira, nota-se que não há modo de execução no nível hardware,
banal a compreensão de tal fenômeno, uma vez entendido que o hardware
simplesmente existe e é executado, não há abstração, e a única camada que
comunica com o mesmo é o sistema operacional.

### Componentes

Por motivos que desconheço, troquei a ordem de apresentação, agora já é tarde. Até gostaria de fazer a descrição do que é um componente, mas traria cansaço psicológico além do que já causara as obviedades e repetições contidas no texto. 

Os componentes do kernel podem ser descritos como:

* Por uma questões de conveniência, S.O. será substituído por SO.

| Componente | Descrição |
| - | - |
| Núcleo | Coração do SO, gerencia o sistema e as principais abstrações. Junto a isso lida com as chamadas de SO. |
| Código de Inicialização | Terefas complexas? Configura os dispositivos, e inicia a execução do núcleo. Aqui existe um padrão estabelecido pela IEEE para as chamadas de SO chamado de POSIX. Lembre-se que em concorrente também apareciam alguns padrões estabelecidos pelo POSIX.|
| Drivers de Dispositivos | Módulos para dispositivos físicos (um para cada dispositivo normalmente, com alguns drivers genéricos disponíveis). |

Para entendedor meia palavra basta. A ordem imprime uma certa
hierarquia dentro do Kernel, tanto no sentido das abstrações quanto na sua
importância.

Descrevamos então a hierarquia do sistema junto do kernel de maneira geral:

| Aplicações e Programas utilitários |
| - |

| Núcleo |
| - |

| Código de Inicialização | Drivers de Dispositivo |
| - | - |

| Controladora de Dispositivos |
| - |

| Dispositivos Físicos |
| - |

Tome nota que tantos os dispositivos físicos quanto as controladoras são
elementos de hardware. Todos os outros níveis existem a nível de software.
Em adição, as aplicações e programas utilitários facilitam o uso do SO, uso
esse notável em apps de configuração, formatação, interface gráfica e
terminal.

## Tipos de Núcleo

Listam-se entre os núcleos, Microkernel, Monolithic Kernel, Cliente-Server
Kernel e Máquinas Virtuais.

### Microkernel

Baseado na concepção de pequenos módulos, para os que tem formação neste
sentido, observa-se as similaridades com arquiteturas baseadas em
microserviços.

Somente um módulo opera em kernelmode, o resto opera em usermode. O
fundamento é que somente o mais essencial rode em kernelmode, desta forma
bugs em módulos de usuário não quebram completamente o SO. 

Para o micronúcleo, temos que a descentralização impacta para, em tese, uma
segurança maior. Ao mesmo tempo que causaria inevitavelmente uma queda de
performance pela maior quantidade orgânica de Context Switches.

Ex: Symbian e Minx3

### Núcleo Monolítico

O núcleo do tipo monolítico consiste em um único programa grande programa
em kernelmode.

#### Chamadas de sistema

* Requisição de serviços ao SO.
* Rotinas do SO com interface padronizada.
* Modo usuário $\rightarrow$ modo núcleo.

Ex: Windows, Linux e MacOS.


### Núcleo Cliente-Servidor

Variação do micronúcleo. Distinguem-se em:

* Servidores: programas que prestam serviços ao SO.
* Clientes: programas usam os serviços do SO.

Comunicação entre servidores e clientes através de trocas de mensagens.

### Máquina Virtual

As máquinas virtuais são colocadas nos tópicos abaixo. 

## Máquinas Virtuais

Criam ilusões de
múltiplas máquinas com o auxílio de um hypervisor. Os benefícios estão
entre uma evitar falhas em uma VM não afeta outras, baixo custo, e
facilitação de testes.

Ex: VirtualBox, VMWare, Parallels e KVM.

### Paravirtualização

Este tipo de virtualizaçào não cria hardwares virtuais, Hypercalls fazem
com que o hóspede envie solicitações explícitas. Por causa disso, é
necessário modificar o SO ou utilizar drivers.

| Sistema 1 | Sistema 2 |
| - | - |

* Hypercall

| Hypervisor (Micronúcleo) |
| - |

| Hardware |
| - |

### Virtualização Completa

A virtualização completa implica na criação de um hardware virtual para a execução
de um SO, não necessitando de mudanças.

#### Hypervisor (Tipo 1)

* Camada de sofware de baixo nível que executa de modo privilegiado sobre o
  hardware.

* Cria-se hardwares virtuais idênticos aos reais.

* Chamada de virtualização bare-metal, hoje é a mais rápida e faz um
  compartilhamento do hypervisor de tipo 1.

| Window | Linux |
| - | - |

| Hypervisor Tipo 1 |
| - |

| Hardware |
| - |

#### Hypervisor (Tipo 2)

Já a virtualização de tipo 2 executa sobre o SO hospedeiro. Temos então o
hypervisor não como kernel, mas como um programa, gerando uma performance
menor. O hóspede executa então sobre o hypervisor tipo 2.

| SO Hóspede |
| - |

| Hypervisor Tipo 2 | Programas do hospedeiro |
| - | - |

| SO hospedeiro |
| - |

| Hardware |
| - |
