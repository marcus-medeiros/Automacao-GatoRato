# 🐈 Controle do fluxo de salas entre dois agentes (gato e o rato)
Este projeto modela um sistema clássico de eventos discretos envolvendo um gato e um rato que se movem livremente em uma torre com 5 salas dispostas em um ciclo. 

## 🔎 Descrição Geral
Este projeto modela um sistema clássico de eventos discretos envolvendo um gato e um rato que se movem livremente em uma torre com 5 salas dispostas em um ciclo. O objetivo é desenvolver um supervisor (um controlador automatizado) que restrinja os movimentos do gato para garantir a principal condição de segurança: o gato nunca deve ocupar a mesma sala que o rato. O sistema supervisionado deve ser não-bloqueante (nunca travar) e maximamente permissivo, concedendo a maior liberdade de movimento possível sem violar a regra de segurança.

## ⚙️ Componentes do Sistema
O sistema é composto por dois agentes (o Gato e o Rato), cujos comportamentos são modelados como plantas, e uma especificação de segurança que define a regra de controle.

### 🐈 O Gato
O gato é um dos agentes do sistema, capaz de se mover para salas adjacentes. Seus movimentos são considerados eventos controláveis, o que significa que o supervisor pode optar por desabilitá-los temporariamente para garantir a segurança.

#### Estados
- **SG0**, **SG1**, **SG2**, **SG3**, **SG4**: Representa os estados que o gato está posicionado, em que SG0 está relacionado à Sala1, SG1 à Sala1, e assim por diante.

#### Eventos
- **GD**, **GE**: Eventos controláveis que representam o movimento do gato.

<p align="center">
<img src= "img/GATO.png" height="250" align="center">
</p>
<p align="center"> Figura 01: Autômato do Gato</p>

### 🐁 O Rato
O rato é o segundo agente do sistema. Ele também se move livremente entre as salas, mas seus movimentos são não **controláveis**. Isso significa que eles ocorrem espontaneamente e o supervisor não pode impedi-los; ele deve antecipá-los.

#### Estados
- **SR0**, **SR1**, **SR2**, **SR3**, **SR4**: Representa os estados que o gato está posicionado, em que SR0 está relacionado à Sala1, SR1 à Sala1, e assim por diante.

#### Eventos
- **RD**, **RE**: Eventos não controláveis que representam o movimento do rato.

<p align="center">
<img src= "img/RATO.png" height="250" align="center">
</p>
<p align="center"> Figura 02: Autômato do Rato</p>
