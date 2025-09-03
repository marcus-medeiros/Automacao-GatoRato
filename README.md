## Projeto da disciplina de Sistemas de Eventos Discretos 
Projeto realizado por: 
> Marcus Vinícius de Medeiros - 121110400

> William Santos Moreira - 121110532

> Ygor de Almeida Pereira - 121110166


## 🐈 Controle do fluxo de salas entre dois agentes (gato e rato) com auxílio de portas

Este projeto aborda a modelagem de um sistema clássico de eventos discretos, no qual um gato e um rato se deslocam livremente em uma torre composta por 5 salas organizadas em ciclo.

## 🔎 Descrição Geral

O objetivo é desenvolver um controlador automatizado capaz de restringir os movimentos do gato e do rato, assegurando a principal condição de segurança: eles nunca podem ocupar a mesma sala ao mesmo tempo.
O sistema supervisionado deve ser não bloqueante (isto é, nunca travar) e maximamente permissivo, garantindo a maior liberdade possível de deslocamento sem violar a regra de segurança.

## ⛔ Problema Encontrado

Na construção dos autômatos, surge uma limitação importante: a não controlabilidade dos movimentos do rato. Como ele pode se mover de forma totalmente autônoma, sem restrições externas, torna-se inviável controlar o sistema apenas com base em eventos observáveis.

Assim, embora o sistema seja observável, não é controlável. A incerteza sobre a direção escolhida pelo rato, somada à ausência de garantias sobre a realização efetiva das transições de movimento, gera uma dificuldade adicional na modelagem das especificações.

Diante dessa condição, duas abordagens podem ser consideradas para superar o problema.

## 🎯 Premissa

Ao introduzir portas de controle no sistema (limitadas a quatro), os deslocamentos do rato deixam de ser totalmente livres e passam a ser influenciados pelo estado das portas (abertas ou fechadas).
Com isso, os movimentos do rato tornam-se controláveis, eliminando os problemas de controlabilidade inicial. Dessa forma, é possível modelar o sistema de maneira permissiva, não bloqueante e plenamente controlável.

Portanto, podemos deduzir que o autômato do gato e do rato pode ser resumido, essencialmente, à construção dos autômatos do gato, do rato e das especificações do sistema, que simulam o comportamento das portas e determinam a controlabilidade dos eventos de movimento do rato.

## ⚙️ Componentes do Sistema
O sistema em estudo é constituído por dois agentes, denominados Gato e Rato, cujos comportamentos foram modelados na forma de plantas. A regra de operação é definida por uma especificação de segurança, responsável por estabelecer as condições de controle. No entanto, devido à característica de não controlabilidade associada ao agente Rato, tornou-se necessária a introdução de portas entre as salas, de modo a viabilizar o cumprimento da especificação e garantir o correto funcionamento do sistema.

### 🐈 O Gato
O gato é um dos agentes do sistema, capaz de se mover para salas adjacentes. Seus movimentos são considerados eventos controláveis, o que significa que o supervisor pode optar por mover-se ou não quando necessário.

#### Estados
- **S0** (Inicial), **S1**, **S2**, **S3**, **S4**: Representa os estados que o gato está posicionado, em que S0 está relacionado à Sala1, S1 à Sala2, e assim por diante.

#### Eventos
- **G_01**, **G_10**, **G_12**, **G_21**, **G_23**, **G_32**, **G_34**, **G_43**, **G_40**, **G_04**: Eventos controláveis que representam o movimento do gato.

<p align="center">
<img src= "img/EventosGato.png" height="150" align="center">
</p>
<p align="center"> Figura 01: Eventos do autômato do Gato</p>


#### Planta: Autômato do Gato

<p align="center">
<img src= "img/GATO.png" height="150" align="center">
</p>
<p align="center"> Figura 02: Autômato do Gato</p>

### 🐁 O Rato
O rato é o segundo agente do sistema. Ele também se move livremente entre as salas, mas seus movimentos são não **controláveis**. Isso significa que eles ocorrem espontaneamente e o supervisor não pode impedi-los; ele deve antecipá-los.

#### Estados
- **S0**, **S1**, **S2** (Inicial), **S3**, **S4**: Representa os estados que o gato está posicionado, em que S0 está relacionado à Sala1, S1 à Sala2, e assim por diante.

#### Eventos 
- **R_01**, **R_10**, **R_12**, **R_21**, **R_23**, **R_32**, **R_34**, **R_43**, **R_40**, **R_04**: Eventos controláveis e não controláveis que representam o movimento do rato.

<p align="center">
<img src= "img/EventosRato.png" height="150" align="center">
</p>
<p align="center"> Figura 03: Eventos do autômato do Rato</p>

### ⚠️ Observação: Mudança na interpretação
Podemos observar que os movimentos do rato, antes totalmente não controláveis, tornaram-se em grande parte controláveis devido à inserção das portas entre as salas. No entanto, os movimentos do rato entre as salas 5 e 1 permanecem não controláveis, em razão da limitação de utilização de apenas quatro portas.

#### Planta: Autômato do Rato

<p align="center">
<img src= "img/RATO.png" height="150" align="center">
</p>
<p align="center"> Figura 04: Autômato do Gato</p>

## ⚙️ Modelagem das Portas
Além dos autômatos que modelam os agentes Gato e Rato, faz-se necessária a inclusão de plantas adicionais que representem o funcionamento das portas entre as salas. Essas plantas têm como finalidade viabilizar o controle dos movimentos dos agentes no sistema, atuando como elementos de restrição e coordenação, de modo a garantir que a especificação de segurança seja satisfeita.

Esses autômatos tem como objetivo representarem o funcionamento das portas entre as salas, modelando duas ações possíveis: abrir ou fechar a porta.

### 🕹️ Porta 1 (Entre as salas 1 e 2)

#### Estados
- **P01** (Inicial): Indica que a porta está aberta.
- **P01_F**: Indica que a porta está fechada.

#### Eventos Próprios
- **P01_Abrir**: Ação para abrir a porta.
- **P01_Fechar**: Transição para fechar a porta.

<p align="center">
<img src= "img/EventosPorta_01.png" height="150" align="center">
<p align="center"> Figura 05: Eventos do autômato da Porta_01</p>

#### Planta: Autômato do Porta_01

<p align="center">
<img src= "img/Porta_01.png" height="150" align="center">
</p>
<p align="center"> Figura 06: Autômato da Porta_01</p>


### 🕹️ Porta 2 (Entre as salas 2 e 3)

#### Estados
- **P12** (Inicial): Indica que a porta está aberta.
- **P12_F**: Indica que a porta está fechada.

#### Eventos Próprios
- **P12_Abrir**: Ação para abrir a porta.
- **P12_Fechar**: Transição para fechar a porta.

<p align="center">
<img src= "img/EventosPorta_12.png" height="150" align="center">
<p align="center"> Figura 07: Eventos do autômato da Porta_12</p>

#### Planta: Autômato do Porta_12

<p align="center">
<img src= "img/Porta_12.png" height="150" align="center">
</p>
<p align="center"> Figura 08: Autômato da Porta_12</p>


### 🕹️ Porta 3 (Entre as salas 3 e 4)

#### Estados
- **P23** (Inicial): Indica que a porta está aberta.
- **P23_F**: Indica que a porta está fechada.

#### Eventos Próprios
- **P23_Abrir**: Ação para abrir a porta.
- **P23_Fechar**: Transição para fechar a porta.

<p align="center">
<img src= "img/EventosPorta_23.png" height="150" align="center">
<p align="center"> Figura 09: Eventos do autômato da Porta_23</p>

#### Planta: Autômato do Porta_23

<p align="center">
<img src= "img/Porta_23.png" height="150" align="center">
</p>
<p align="center"> Figura 10: Autômato da Porta_23</p>

### 🕹️ Porta 4 (Entre as salas 4 e 5)

#### Estados
- **P34** (Inicial): Indica que a porta está aberta.
- **P34_F**: Indica que a porta está fechada.

#### Eventos Próprios
- **P34_Abrir**: Ação para abrir a porta.
- **P34_Fechar**: Transição para fechar a porta.

<p align="center">
<img src= "img/EventosPorta_34.png" height="150" align="center">
<p align="center"> Figura 11: Eventos do autômato da Porta_34</p>

#### Planta: Autômato do Porta_34

<p align="center">
<img src= "img/Porta_34.png" height="150" align="center">
</p>
<p align="center"> Figura 12: Autômato da Porta_34</p>


## 🛑 Especificações
Este autômato tem como função assegurar que o Gato e o Rato nunca ocupem a mesma sala simultaneamente. Para atender a esse objetivo, torna-se necessário o desenvolvimento de autômatos adicionais que imponham restrições sobre determinados movimentos (eventos), de modo que o sistema resultante opere conforme o comportamento esperado.

Foram elaboradas duas especificações para a modelagem do sistema. A primeira corresponde ao resultado da composição paralela dos autômatos que representam o Gato e o Rato, enquanto a segunda refere-se à composição das portas entre as salas. A partir desses autômatos resultantes, foram então aplicadas as restrições necessárias para garantir o atendimento à especificação de segurança do sistema.

### 🎌 Especificação: Gato e Rato

Inicialmente, após a geração da especificação por meio da composição entre as plantas que representam os agentes do sistema, foram aplicadas as restrições necessárias. Em essência, essas restrições correspondem aos estados em que o Gato e o Rato ocupam simultaneamente a mesma sala, situação que deve ser evitada no modelo.

#### Especificação: Autômato do Gato||Rato

<p align="center">
<img src= "img/Especific_GATOeRATO.png" height="300" align="center">
</p>
<p align="center"> Figura 13: Especificação GATO||RATO</p>

**Observação:** Observa-se que o modelo apresenta estados com restrição, destacados em azul, enquanto os outros permanecem representados na cor verde.

### 🎌 Especificação: Autômato da Composição das Portas

**Objetivo:** O objetivo é representar de forma completa as condições em que as portas devem permanecer abertas ou fechadas, considerando os possíveis movimentos do Gato e do Rato, de modo a garantir que cada transição dos agentes resulte na configuração correta de acesso entre as salas. Por se tratar de uma especificação, os eventos que violam essas condições devem ser bloqueados. Como o autômato das portas define que os movimentos de entrada em uma sala dependem do estado atual das portas, surgem restrições automáticas no sistema. Dessa forma, após a composição de todos os autômatos, obtém-se uma especificação completa que descreve todos os movimentos permitidos para os agentes, assegurando a operação correta e segura do sistema.



### 🧩 Autômato Resultante (Após a Síntese dos autômatos)

Realizando-se a composição paralela, temos o autômato resultante da síntese supervisionada dos autômatos *Gato*, *Rato*, e das **Portas* e as *Especificações*. 
O sistema resultante apresenta as seguintes propriedades:

- Permite que o Gato e o Rato se movimentem de forma simultânea, garantindo uma interpretação rigorosa do comportamento do sistema;

- Assegura que, em nenhum momento, os dois agentes ocupem a mesma sala;

- É não bloqueante, ou seja, não existem estados em que todos os movimentos possíveis dos agentes sejam impedidos;

- É maximamente permissivo dentro das restrições de segurança impostas.

Com essa composição, o autômato resultante da síntese é capaz de localizar as posições de ambos os agentes e permitir seus deslocamentos de maneira aleatória e/ou simultânea. Entretanto, apenas movimentos seguros são autorizados, de modo que o Gato e o Rato nunca compartilhem a mesma sala em nenhum instante da execução do sistema.

### 🧩 Considerações

A condição que garante a simultaneidade dos movimentos dos agentes impõe limitações às possibilidades de deslocamento, de modo que o Gato e o Rato não podem ocupar salas adjacentes ao mesmo tempo. Caso essa restrição não fosse necessária, seria possível permitir uma maior flexibilidade nos movimentos dos agentes entre as salas, ampliando as combinações de estados possíveis no sistema.


### 🎥 Link do vídeo: https://youtu.be/e5iRtu5eMLY

### 🖊️ Documento: 
doc/
├─ Automato_GatoRato_ALTERNANDO.wmod (Modelagem com alternância - antiga)
├─ GatoRato_Project.wmod (Modelagem do Projeto Completa - nova)
└─ main

img/
|- Imagens...

✉ README.md    [selected]


