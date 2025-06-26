# Design e Arquitetura de Software-2
**Rafael Luiz Souza de Lima**

## Aula 27/02/2025

Ao criar o design de uma solução, serão necessarias escolhas de troca, pois nunca será possível ter tudo de melhor em um sistema, e ainda pagar barato.

*Exemplos: Bancos Não relacionais trocam o espaço de armazenamento para obter uma velocidade de processamento maior.*

EC2 auto-scale: Escala automaticamente o numero de maquinas quando necessario maior processamento.

Amazon CloudWatch: Monitora o servidor e automaticamente fornece informaçoes sobre desempenho do sistema, fornecendo insights sobre como otimiza-lo. 

IaC: Infraestrutura como codigo\
    Rapidamente entrega ambientes duplicados;\
    Reduz erros de configuração de configurações manuais;\
    Propaga mudanças constantes a todos os stacks;

Tratar recursos como algo descartável\
    Parar recursos que não estão em uso;\
    Automatizar lançamento de novos recursos com configs identicas;\
    Testar updates em recursos novos, e então substituir os recursos antigos com os novos.
        
## Aula 06/03/2025

Usar componentes com baixo acomplamento\
    Elastic Load Balancing(ELB): Responsavel por balancear a carga entre copias do banco de dados.\
    Criar redundâncias de Load Balancer para evitar um ponto de quebra.

Design de serviços, não de servidores\
    Quando apropriado, considerar usar containers ou soluções serverless.\
    Comunicação em mensagens.\
    Sites estaticos armazenados em um bucket S3.\
    Usar a abundância dos serviços AWS, não limitar a infra em servidores.

Escolher a opção de banco de dados correta\
    Analisar requisitos de escrita e leitura.\
    Necessidade de tamanho de armazenamento.\
    Tipo de objeto e natureza do objeto.\
    Durabilidade.\
    Latência.\
    Usuarios concorrentes máximos.\
    Natureza das buscas.\
    Integridade dos controles.\
    *Em resumo, analisar os fatores importantes para o sistema, para fazer a escolha correta do banco de dados.*

Evitar pontos únicos de falha(Ponto de quebra)\
    Criar copias do banco para assumir em caso de falhas.

Otimização de custo\
    Tomar vantagem da flexibilidade da AWS para otimizar eficiencia de custo.

Utilizando Caching\
    (Netflix and chill)\
    Minimizar operações de retorno de dados redundantes, melhorando performance e preço.

Contruir segurança nas camadas da infraestrutura\
    Usar serviços gerenciados.\
    Utilizar o principio do menor privilégio.\
    Encriptar dados.

Infraestrutura Global AWS\
    Região é uma área geografica do mundo.\
    Availability zone(AZ's) é uma região que possue um centro de dados AWS, podendo ter multiplos em uma região.\
    Local Zone serve para rodar serviços computacionais em locais onde não possue uma região AWS ainda. 

## Aula 10/03/2025

AWS PoP\
    Pontos de presença ou edge location, a menor parte da infraestrutura AWS.\
    Entrega de menor latência.

Securing Access\
    AWS shared responsability model.\
    Cliente: Responsavel pela segurança NA nuvem;\
    AWS: Responsavel pela segurança DA nuvem.

    Cliente: Plataforma,aplicações,identidades e acesso,trafego de rede,sistemas operacionais;\
    AWS: Armazenamento,Database,Rede,Regiões,servidores,firewalls.

### SideQuest: S3

Server Side Encryption\

4 modelos:\
    -SSE-S3: Criptografia em uma chave unica(Default);\
    -SSE-KMS: A empresa tem controle da chave;\
    -SSE-CE: O cliente sobe o objeto E a chave, AWS não possue acesso á chave;\
    -SSE-DKMS: Criptografia dupla;

### Fim da sidequest

Principios para uma aplicação segura\
    Implementar um sistema forte de indentidade;\
    Proteger dados em transito e em descanso;\
    Aplicar segurança em todas as camadas;\
    Manter Rastreabilidade;\
    Manter pessoas longe dos dados;\
    Preparar para eventos de segurança;\
    Automatizar praticas de segurança. 

3 pilares de autenticação\
    O que você sabe(senhas)\
    Quem você é(biometria)\
    O que eu tenho(Dispositivo com gerador de chaves)

Autorização\
    IAM: Ferramenta de controle de permissões da AWS.\
    Principio do privilégio mínimo: Conceder apenas o minimo de acesso necessário para uma função.\
    Começar com o minimo de permissões, adicionar permissões apenas em casos necessários. 
    
## USE CRIPTOGRAFIA!!!!


## Aula 13/03/2025

IAM - ID da conta - 12 digitos necessarios pro acesso da conta\
    grupos\
    Contas\
    Usuarios\
    Funções\
    Politicas

Boas praticas\
    Seguir o privilegio minimo;\
    Usar autenticação de multiplos fatores;\
    Sempre designar um tempo de duração às contas;\
    Em caso de credenciais de longa duração, renovar access keys;\
    Use grupos;

Protegendo o usuário root\
    NUNCA USE A CONTA ROOT PARA TAREFAS DO DIA A DIA!!!!!!!
    TEM ACESSO A TUDO.\
    Primeira coisa ao criar uma conta AWS, habilitar MFA.\
    Criar outros usuários para que eles possam utilizar a conta.

Roles\
    Permitem o usuario assumir uma posição do sistema, ganhando acessos que normalmente sua conta não teria, por um tempo limitado.\
    É importante justamente por ser temporária.\
    Tambem serve para dar permissões a máquinas.\
    Extremamente importante no ambiente AWS.

Acesso programático\
    Acesso ao ambiente sem ter acesso ao console AWS.\
    Feito através do console de comando, SDK ou API REST.

## Aula 17/03/2025

IAM policies\
    RBAC - Role Base Access Control.\
    De acordo com o papel, o usuario tem permissões.\
    Permissão de administrador - Maior permissão abaixo do root.\
    Policies por papel x por recursos:\
        papel: Preso à uma role de usuário;\
        recursos: Preso à um recurso da AWS;\
    Policies com "principal" = policies de recursos.

Determinando permissões em tempo de request\
    Deny sempre tem prioridade sobre permissão.\
    Usuários sem permissão, mesmo se n tiver um deny, não terão acesso às funções.

Tipos de armazenamento\
    Armazenamento por blocos: dados armazenados em blocos de tamanho fixo. (EBS)\
    Armazenamento por Arquivos: dados armazenados em uma estrutura hieraquica. (EFS)\
    Armazenamento por objetos: dados armazenados como objetos baseados em atributos e metadados. (S3)

Amazon S3\
    Virtualmente ilimitado.\
    5Tb por objeto/arquivo.\
    Arquivos são chamados de objetos pois se armazenam metadados junto do binário.\
    Não existem 2 buckets com o mesmo nome no mundo.\
    url de s3: S3 - (região) - amazonaws/ - (nome do bucket)/(nome do objeto)\
    USE PREFIXOS PARA FACILITAR BUSCAS EM BUCKETS(/"alguma coisa" na URL).
    
## Aula 20/03/2025

Amazon s3 - continuação\
    Por padrão, URLs de S3 não são publicas.\
    S3 garante 11 9s de durabilidade no objeto(99.999999999%)Adquiridos pois o objeto é salvo em 3 AZs diferentes.\
    Disponibilidade de 99.99%(pode aumentar).\
    Varios sistemas(Netflix) utilizam S3 para disponibilizar conteudo por causa da alta performance.

Usos do S3\
    Hospedar um site estático.\
    Armazenar dados financeiros que outros serviços conseguem usar tambem.\
    Soluções de backup de dados para suporte de disastres.\
    Distribuição de midia.

Buckets\
    São regionais, portanto tem uma latência menor para máquinas na mesma região.

Movendo dados no S3\
    Não existe limites de objetos.\
    Requer permissão.\
    Tudo é criptografado(durante download e upload).

Como subir um arquivo\
    Pelo console da AWS(160GB).\
    Pela linha de comando("aws s3 cp arquivoorigem s3://bucketdestino").\
    Codigo em alguma linguagem.\
    Chamada de API REST(PUT).\
    Upload de multipart: Dividir um arquivo muito grande em partes de tamanho igual.

S3 transfer aceleration\
    Otimiza velocidade de transferencia.\
    Utiliza redes da AWS para evitar trafego de rede.

AWS Transfer family\
    Usado pra transferir arquivos para dentro e para fora de um S3, através de protocolos FTP.

Classes de Armazenamento de objetos\
    Quentes:\
        Uso geral: S3 Standard.\
        Intelligent tiering: S3 Intelligent Tiering.\
        Acesso infrequente: S3 Standard-IA --- S3 One Zone-IA.\
    Frios:\
        Arquivo: S3 Glacier --- S3 on Outposts.\
        Glacier: glacier Instant Retrieval;\
                glacier Flexible Retrieval;\
                glacier Deep Archive.

Custos\
    A lista acima está em ordem de mais caro para mais barato para armazenar.\
    O preço é ditado de acordo com o tipo de armazenamento da classe.\
    Standard permite acesso direto ao arquivo, por isso é o mais caro, enquanto o tier dos glaciers "congela" o arquivo, tendo que re-hidratar o arquivo para receber o acesso, podendo levar horas ou até dias, por isso é mais barato.\
    Mesmo sendo mais barato para guardar, possui o preço para retirar o arquivo, que se torna mais caro.
    
## Aula 24/03/2025

Configurando um ciclo de vida do S3\
    Ações de transissão: Transiciona de uma classe a outra.\
    Ações de Expiração: Definem quando o objeto expira.\
    Fazer des do começo, ao configurar o S3.

Versionamento\
    Todo balde nasce com versionamento desligado.\
    Uma vez habilitado, não pode mais desabilitar ele.\
    Cria um novo objeto com um id de versão diferente, e ambos podem ser recuperados pelo id de versão.\
    Adiciona um marcador de delete, mas o objeto ainda é recuperavel pelo id.

Cors\
    É uma proteção aos arquivos do site.\
    Bloqueio de acesso à paginas que não são reconhecidas pelo site.

Modelo de consistência de dados no S3\
    Sempre será consistente com os objetos.

## Aula 27/03/2025

    Pratica no ambiente aws.

## Aula 31/03/2025

    Pratica no ambiente aws.

## Aula 03/04/2025

Virtualização de maquinas EC2.\
    EC2 é uma maquina virtual hospedada em um servidor fisico.\
    Amazon machine image: Um template do volume root.\
    Beneficios: Repetibilidade, Reusabilidade e recuperabilidade.

EC2 instance name type.\
    familia - geração - familia do processador - capacidades adicionais - tamanho.\
    exemplo = "c7gn.xlarge".

AWS Compute Optimizer: Recomenda tipos de instancia e tamanho para otimizar o uso de maquinas.

Arquivos compartilhados em instancias EC2.\
Amazon EFS.
    
## Aula 07/04/2025
    
EBS - Elastic Block Storage - HD do servidor.\
EFS - Elastic File Share - Linux.\
FSx - File share para Windows.

EC2-instance user data.\
    Pode especificar dados de usuario para rodar um script de inicialização.
    
Instance Metadata - Informações sobre sua instância.

AMI Deployment Models.\
    Basic - Silver - Golden.\
    Silver precisa de algumas configurações manuais.\
    Golden precisa ser totalmente configurada manualmente.

Placement group.\
    Cluster - Amazon tenta agrupar as maquinas na mesma AZ para ganhar em latência.\
    Spread - Amazon espalha as maquinas na maior quantidade de AZ's possiveis, dentro da mesma região. Ganha mais confiabilidade porem perde em latência.\
    Partition - Divisão do banco em fragmentos, utilizado para reduzir o escopo de busca.

AWS Pricing Options.\
    AWS Free Tier: Amazon EC2.\
    750 horas por mês de uma t3.micro ou t4g.small.\

EC2 pricing models.\
    Modelo de compra.\
    On-demand, Reserved Instance, Savings plan, EC2 spot.\
    Preserved Instance para cargas fixas.\
    On demand para picos de trabalho.\
    Spot instance para tolerancias de falhas.

AWS Well Architected Framework.\
    Segurança - Automatizar mecanismos de proteção.\
    Eficiencia e performance - usar o tipo e tamanho de maquina correto.\
    Otimização de custo - Selecionar os corretos tamanhos de recurso, escolher o modelo de precificação correto.\
    
## Aula 10/04/2025

Adicionando uma camada de database.\
    Considerações: Escalabilidade, requerimentos de storage, characterísticas dos dados, durabilidade.
    
Bancos relacionais e não relacionais.\
    Bancos não relacionais possuem uma melhor flexibilidade, escalabilidade e performance em comparação com relacionais.\
    Bancos relacionais - RDS
    Bancos não relacionais - DynamoDB, Neptune, ElastiCache.

Ao utilizar um serviço gerenciado de banco AWS, o cliente só precisa se preocupar com a aplicação do banco.

Amazon RDS.\
    Seriço gerenciado AWS para bancos relacionais.

Amazon Aurora.\
    Simula um MySQL ou um PostgreSQL.\
    5x mais rapido que MySQL e 3x mais rapido que PostgreSQL.
    
## Aula 17/04/2025
     
RDS Proxy.\     
    Se localiza entre a aplicação e o banco.\
    Cria um pool de conexões e engana a aplicação para se conectar a ele.\
    Diminui a exaustão do servidor.

Secrets Manager.\
    Guarda segredos.\
    Pode se conectar ao banco para guardar uma string de conexão.\
    Pode ser configurado para automatizar a renovação de segredos.

Mecanismos de backup.\
    Backup automatizado - Restaura de 7 a 35 dias o banco.\
    Snapshot - Para retornar backups muito antigos.\
    Backup cross-region - Armazenar copias de backup em outras regiões.

Criptografia.\
    Chaves de criptografia podem ser armazenadas no AWS KMS.\
    Chaves Simetricas - Chave unica.\
    Chaves assimetricas - par de chaves, uma para encriptar e uma para desencriptar.\

DynamoDB.\
    Banco que suporta a Amazon.com\
    Gerenciado, Serverless, NoSQL.\
    Entrega consultas com 1 digito de ms.\
    Utilizado em aplicações de uso extremo.
    
    Mecanismo de stream para arquiteturas orientadas a eventos, grava as alterações no momento que são feitas.

    Criptografia por padrão.\

    Dados ficam espalhados por servidores.\
    Chave de partição serve para localizar os registros.\
    Chave de ordenação serve para ordenar os registros.\

    Global tables - permite criar tabelas em multi-regiões e acesso multi-regiões tambem.\

    CRIE PERMISSÕES DE ROLE PARA AUTENTICAR O ACESSO!!!\

## Aula 05/05/2025

    Networking Environment\
    VPC - Logicamente possui uma topologia diferente da fisica.

    Toda VPC tem o seu Cidr.\
    Criar subnets para ficar mais facil de gerenciar a VPC.\
    Toda VPC tem uma tabela de rotas padrão.\
    Regra: Cidr da rede permite trafego local na rede.\
    Subnets vivem dentro de uma AZ.
    
    Subnet publica: Os recursos dentro dela estão viziveis pra internet.\
    Criar regra de saída para internet gatway.\
    Endereço que estiver conectado ao internet gateway deve ter um endereço publico.

## Aula 08/05/2025

    toda maquina tm 2 tipos de ips, privados e publicos, e os publicos a aws so disponibiliza 5 por região.\
    
    subnet privada: 
        não tem acesso, nem é accessada pela internet, é boa para bancos de dados.\
    
    lembrar da entreda para permitir a saida.\
    
    Camadas dde segurança AWS.\
    Security Group: firewall que se configura quando cria um servidor AWS.\
    Network ACL: é implementado na tecnologia de redes da AWS, é um firewall de subnet.\
    Necessário criar regra de entreda e saida, pois não lembra.\

    Network Firewall.\
    Servidor de firewall que pode subir em uam subnet propria, onde se pode controlar regras de
    entrada e saída de internet.

    VPC endpoint: cria uma placa de rede virtual dentro da sua rede, criando um tunel dentro da AWS 
    conectando no s3 por um ip privado

    Gateway VPC endpoint: só de conecta com dois serviços, ou com o s3 ou com o dynamodb

    Load Balancer: serve para não precisar expor as maquinas na internet, ai ele fica exposto, 
    e depois redireciona para as maquinas

    Gateway Load Balancer endpoint:  serve apenas caso você não queria utilizar o load balancer da aws, deixando esse novo load balancer que você comprou exposto para a internet, é um load balancer de um load balancer

    Amazon VPC flow logs: é oque monitora as redes das maquinas, para ver se elas estão conversando uma com a outra corretamente


## Aula 19/05/2025

    rede: é um isolador
        full mech: tudo fala com tudo, não pode ter colisão entre VPCs
        shared VPC(hub-and-spoke): você tem uma VPC principal(hub), e tem as spokes que falam com o hub

    AWS Transit Gateway: é um gerenciador central, centraliza as redes VPC, e se custo é por dados processados,
    ele é um serviço regional, e consegue conectar 5 mil attachments(5mil coisas)

    Transit gateway peering: conecta mais de 1 transit gateway

    VPC peering: ele conecta VPCs uma na outra, mais simples que o transit gateway

    Connection site to site VPN.
    Conexão de 2 pontos por VPN.
    Direct connection.
    Conexão exclusiva literal, não passa pela internet publica.


## Aula 26/05/2025

    IAM Groups: criar um role para associar todas as permissões que as pessoas desse grupo devem ter, e depois vincular essas pessoas ao grupo.
    ele sempre vai dar prioridade para negar o acesso, ex: caso tenha 20000 mil acessos e um "deny" ele vai perder seus acessos

    RBAC - Role Base Access Control.
    Concedar permissão para os usuarios através de roles para melhor controle de quem acessa oque.
    Toda vez que um usuário assume uma role, ele recebe uma credencial nova e temporária.
    Ao terminas o prazo, pode-se assumir a role novamente, porém a credencial irá ser diferente

    AWS Cognito.
    Ele permite acesso usando conta de outras plataformas


## Aula 29/05/2025

    Iriamos criar um Cognito para cirar uma autenticação java

    User pool: banco de dados de usuarios e senhas, independente da linguagem, ao invés de ter uma tela de login por exemplo em java, ele leva lá para a aws verifica e depois retorna a resposta, ele faz a autenticação da aplicação, e também a atutenticação para que o seu software se comunique com a AWS

    AWS Organization: serviso da aws que permite você gerenciar multiplas contas usando uma extrutura ierarquica, e você ganha desconto por volume

    service control polices: politicas de governanca da tua conta da aws, por exemplo se eu tenho carteira de abilitação, mas a policia me impede de dirigir babado, ou seja ela faz a governancia, eu posso dirigir, mas a policia não me deixa dirigir bebado, no caso ela limita de fazer algo fora dela

    Police de limite não dão permissão
    Police de grant dão permissão

    Criptografia simetrica: tem uma chave só para criptografar e descriptografar
    Criptografia asimetrica: tem duas chaves uma para criptografar e outra para descriptografar

    Server side encryption: criptografia dentro da nuvem

    AWS Key Management Service(AWS KMS): cofre de chaves e ferrameta de criptografia padrão da AWS, e é baseada em software
    HSMs: igual ao KMS mas as chaves ficam em um servidor fisico ao invés da nuvem

    Amazon Detective: detecta comportamentos estranhos na sua conta


## Aula 02/06/2025

    Monitoramento de recursos
        motivos de implementação: saude operacional, utilização de recursos, performance da aplicação, segurança

    CloudWatch: coleta métricas de serviços AWS atraves de regiões em um repositório de métrica, coleta logs, métricas são gratuitas, logs são pagos, pode criar alarmes para avisar sobre limites atingidos

    EventBridge: barramento de eventos, jeito de monitorar a AWS em tempo real

    Custos: cost explorer


## Aula 05/06/2025

    Auto Scaling: scala baseada na data e tempo, é para cargas de trabalho previsíveis, scala baseada em métricas rastreadas, é para cargas de trabalho moderadamente intensas


## Aula 16/06/2025

    Scaling AWS databases
    Escalando um cluster de Aurora: escala verticalmente mudando o tamanho da instancia de aurora, escala horisontalmente usando aurora auto scaling para gerenciar a leitura de números de replicas


    Load Balance: distribui trafego entre multiplos alvos em um ou mais zonas abitaveis, pode receber trafego publico ou privado, verifica a saude das maquinas antes de mandar a requisição, scala automático. 

    4 tipos de load balancer: 
        o load balancer classico, você pode usar, mas ele não é mais indicado;
        application load balancer: camada 7, é o mais utilizado, diferencia produto de cliente;
        network load balancer: usar tls offloading diferencia tcp de udp, é o segundo mais utilizado;
        gateway load balancer: é para quando você não quer utilizar o load balancer da AWS;

    Load Balancer Componentc: 
    TLS Certificate: são de graça, mas tem que renovar a cada 3 meses

    DNS lookups: 

    Route 53: um servidor de dns que traduz seu dominio para uma hosted zones, ele tem SLA 100%, pode monitorar dcloudwatch alarms, suporta multiplas rotas

    AAAA IPCV6
    CNAME: é uma entrada no sistema de nomes de domínio (DNS) que mapeia um nome de dominio (um alias) para outro nome de dominio (o nome canonico ou verdadeiro)
    TXT: prova que você é dono de um DNS
    MX
    NS: e-mail


## Aula 23/06/2025

    CloudFormation: serviso aws permite que você fassa criação, atualização e exclusão de recursos de forma automatizada, posso criar arquivo "YAML"(usa mesma ideia do python, ele precisa de identação, mas tem menos texto) e arquivo "JSON"(mais verboso e mais fácil de escrever)

    Drift detection: permite que você identifique discrepâncias entre o estado atual dos seus recursos AWS implantados e o estado esperado, conforme definido nos seus modelos do CloudFormation

    AWS Quick Start: acelerador de criação de produtos e servisos

    Cache content: sempre que precisar melhorar a performance do banco, se usa cache por exemplo;
        ElastiCache: geralmente mais utilizado para banco, se coloca na frente do banco de dados para entregar mais rápido
        CloudFront: clocar na frente do site para entregar recursos mais rápidos, na frente do LoadBalancer


## Aula 26/06/2025

    Para reduzir problema de acoplamento entre as camadas da aplicação, pode ser utilizado load balancer entre as camadas

    Outra maneira de melhorar a aplicação, ao invés de você ter um monolito, é bom você modularizar a sua aplicação, aumentando a resiliencia e reduzindo problema de acoplamento, exemplo ideal, seria aplicar a arquitetura de microserviços

    Amazon SQS: serviço de filas
    Amazon SNS: serviço de tópicos
    Amazon MQ: serviço que possui tanto filas quanto tópicos

    Short Polling vs Long Polling: tempo de busca de fila, impacta no seu custo

    (👉ﾟヮﾟ)👉    👈(⌒▽⌒)👉    👈(ﾟヮﾟ👈)