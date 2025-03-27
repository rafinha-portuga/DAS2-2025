# Design e Arquitetura de Software-2
**Rafael Luiz Souza de Lima**

## Aula 26/02/2025

**Interfaces:**\
São contratos que definem métodos que uma classe deve implementar, promovendo desacoplamento, padronização e facilidade de manutenção.

**Pacotes:**\
Agrupam logicamente classes e interfaces relacionadas, ajudando na organização, modularidade e controle de acesso dentro do software.

**Componentes:**\
São unidades independentes e reutilizáveis que encapsulam funcionalidades específicas, permitindo fácil integração e manutenção no sistema.

**Módulos:**\
Representam agrupamentos de componentes ou funcionalidades relacionadas que podem ser desenvolvidos, testados e implantados separadamente.

**Camadas:**\
Estruturas organizacionais que dividem o software em níveis de responsabilidade específicos (ex.: apresentação, lógica de negócio, acesso a dados), facilitando manutenção e escalabilidade.

**Serviços:**\
Unidades independentes que disponibilizam funcionalidades ou recursos específicos via interfaces bem definidas, permitindo interoperabilidade e integração entre diferentes partes de uma aplicação ou sistemas externos.


**Monolito**\
**Repositório único de código:**\
Todo o código-fonte fica armazenado em um único local centralizado, facilitando o gerenciamento e controle de versão.

**Uso de uma única tecnologia padrão:**\
O desenvolvimento ocorre usando uma única tecnologia ou linguagem predominante, padronizando o ambiente e facilitando a manutenção.

**Compilado, testado, único pacote:**\
O sistema inteiro é compilado, testado e empacotado de uma só vez, resultando em uma única entrega integrada.

**Deploy como um único sistema:**\
A aplicação é implantada integralmente, como uma única unidade indivisível, sem separação de funcionalidades.

**Executado como um único processo no sistema operacional:**\
A aplicação roda em um único processo no sistema operacional, o que pode limitar escalabilidade horizontal e robustez.

**Único banco de dados:**\
Toda a aplicação utiliza apenas um banco de dados compartilhado, concentrando o armazenamento e simplificando a administração, mas potencialmente gerando gargalos de desempenho.


## Aula 05/03/2025
**Padrão arquitetural:**\
É um conjunto pré-definido de soluções que orienta a organização estrutural e funcional de sistemas, auxiliando na resolução recorrente de problemas arquiteturais.

**MVC (Model-View-Controller):**\
**Um padrão arquitetural que separa o sistema em três partes:**\
**Model:** responsável pelos dados e regras de negócio.

**View:** cuida da apresentação e interface com o usuário.

**Controller:** gerencia a comunicação entre Model e View.

Essa separação promove clareza, manutenção simplificada e desenvolvimento paralelo.


**Estilo de arquitetura:**
Representa uma abordagem geral que define princípios e diretrizes para projetar sistemas, indicando características estruturais comuns, como arquitetura em camadas, arquitetura orientada a serviços (SOA) ou arquitetura baseada em eventos.


**Arquitetura em Camadas:**\
**Divisão de responsabilidade:**\
Divide o software em camadas bem definidas, com responsabilidades específicas, promovendo organização e clareza.

**Performance:**\
Permite otimizar desempenho isoladamente por camada, embora possa gerar atrasos por múltiplas chamadas internas entre elas.

**Segurança:**\
Facilita implementação de mecanismos de segurança específicos por camada, protegendo melhor os dados e processos sensíveis.

**Manutenibilidade:**\
Torna o sistema mais fácil de manter, permitindo alterações isoladas sem impacto direto nas demais camadas.

**Camada de Apresentação:**\
Responsável pela interação direta com o usuário (interface), possuindo requisitos específicos ligados à usabilidade e experiência do usuário.

**Camada de Lógica de Negócio (Aplicação):**\
Local central para definição e atualização das regras: Centraliza todas as regras e validações do negócio.

Escalabilidade do backend: Permite que a camada cresça de forma independente para suportar mais requisições e maior carga.

**Camada de Persistência:**\
Banco de dados relacional consolidado: Armazena e gerencia dados estruturados com eficiência e consistência.

Resolve problemas de concorrência: Gerencia transações e acessos simultâneos sem perda ou inconsistência.

Permite compartilhamento de dados: Facilita o acesso uniforme às informações por diferentes partes do sistema.



## Aula 06/03/2025
**Who Needs an Architect?**\
Todo projeto complexo precisa de um arquiteto para definir estratégias claras, garantir qualidade estrutural, promover padronização, controlar riscos e facilitar comunicação técnica eficaz entre equipes.

**O que é arquitetura?**\
É a estrutura fundamental de um sistema de software, que define componentes, relacionamentos e propriedades essenciais, formando a base técnica para seu desenvolvimento e manutenção.

**Qual o comportamento do arquiteto da "Matrix"?**\
É representado como distante, arrogante, extremamente controlador e rígido. Cria sistemas complexos, mas incompreensíveis para os usuários finais, simbolizando um arquiteto desconectado das necessidades reais.

**Qual o comportamento do arquiteto ideal?**\
É colaborativo, comunicativo, flexível, e orientado às necessidades dos usuários e stakeholders. Equilibra requisitos técnicos com visão prática e acessível, facilitando a compreensão e garantindo que a arquitetura resolva problemas reais.


## Aula 13/03/2025
**Fundamentos da Arquitetura de Software**\
**Pensamento Arquitetônico**\
O pensamento arquitetônico é uma forma estruturada de raciocínio que envolve entender o sistema como um todo, identificando suas responsabilidades, partes essenciais e relacionamentos entre essas partes.



**Principais aspectos abordados são**\
Abstração: Capacidade de simplificar o sistema destacando elementos importantes e omitindo detalhes irrelevantes.

Visão Sistêmica: Consideração ampla do contexto do sistema, entendendo como suas partes interagem e como ele se encaixa no ambiente maior.

Tomada de Decisão: Escolher soluções e estruturas baseando-se em trade-offs (custos e benefícios), levando em conta os requisitos funcionais e não funcionais.

Antecipação de Mudanças: Projetar o sistema para ser adaptável, prevendo futuras alterações sem grandes impactos negativos.

Comunicação Efetiva: Transmitir claramente as decisões arquiteturais para equipes técnicas e não técnicas, usando diagramas, modelos e documentação adequada.

Esse tipo de pensamento garante que a arquitetura de software seja sólida, flexível e sustentável ao longo do tempo.


## Aula 19/03/2025
**Trade-offs:**\
São decisões técnicas onde se avaliam prós e contras ao escolher uma abordagem ou solução. Envolvem considerar fatores como performance, custo, escalabilidade, segurança e manutenção para atingir um equilíbrio adequado.

**Tópicos:**\
Em arquiteturas orientadas a eventos e mensageria, tópicos são canais lógicos usados para categorizar ou agrupar mensagens, permitindo comunicação organizada e eficiente entre componentes desacoplados.

**Filas:**\
São estruturas usadas em sistemas distribuídos para armazenar mensagens ou requisições temporariamente até serem processadas, garantindo a comunicação assíncrona, confiabilidade, e permitindo o balanceamento de carga.

**Fan out:**\
Padrão onde uma mensagem publicada por um único componente é distribuída simultaneamente para vários consumidores ou serviços diferentes. É muito usado em arquiteturas orientadas a eventos para escalar processamento paralelo e desacoplar sistemas.