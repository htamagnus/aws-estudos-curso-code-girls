## Introdução à AWS e conceitos básicos

#### 1. Infraestrutura global 

https://aws.amazon.com/pt/about-aws/global-infrastructure/

---

- se você precisa impantar workloads de aplicações em todo o mundo, os próximos usuários finais terão a latência inferior a 10milissegundos, ou seja, somente o primeiro usuário irá demorar pra carregar;

a aws possui uma extensa rede global de data centers, chamados de “regions”e “availability zones”

- regions: áreas geográficas que contém várias availability zones;
- availability zones (data centers): são data centers independentes fisicamente, mas conectados logicamente, o objetivo é garantir alta disponibilidade
- a aws abrange 117 zonas de disponibilidade em 37 regiões geográficas

#### 2. Modelo de negócio da AWS

- o modelo de negócio da aws é chamado de could de OPEX: não necessita de uma grande infra para iniciar um projeto, diferente do modelo CAPEX: precisa de uma infra física para começar o projeto;
- pricing flexível: a aws oferece um modelo de pagamento conforme o uso;
- grande variedade de serviços;

---

**Saas x PaaS x Iaas**

**SaaS:** você não se preocupa com nada técnico: usa o **software pronto** pela internet. você USA. ex: gmail, google docs, slaesforce, dropbox;

**PaaS:** você aluga uma plataforma pronta para rodar suas aplicações. a infra e o sistema já estão configurados, você só coloca o código e roda. você CONSTRUE ex: heroku, vercel, netlify, aws elastic beanstalk

**IaaS:** você aluga ****infraestrutura bruta: servidores, rede, armazenamento. você cuida do sistema operacional, banco de dados, aplicações. você MIGRA. ex: aws ec2, google compute engine, azure virtual machines

---

#### 3. Conceitos fundamentais

**Regiões**

- cada region é projetada para ser isolada das outras regiões, isso proporciona a maior tolerância a falhas e estabilidade possível;
- uma região é composta por 2 ou mais zonas de disponibilidade, sendo o mínimo 2;

---

pontos para levar em consideração quando for escolher uma região:

- compliance;
- disponibilidade de serviços;
- custos;
- latência;

---

**Zonas de disponibilidade**

cada região é independente das demais regiões, o que significa que os recursos são exclusivos da região escolhida em que está sendo povisionado os recursos, isso contribui para maior tolerância a falhas e não há replicação automática entre as regiões, isso deve ser habilitado pelo admin da conta.


---

## Computação na Nuvem com EC2

#### 1. O que são instâncias EC2

são máquinas virtuais na AWS, podendo ser com sistema operacional windows ou linux, é composta por:

- cpu, memória, disco, rede e SO;
- é do tipo IAAS, ou seja, estamos utilizando o tipo infraestrutura como serviço;
- escolher a instância correta na AWS é crucial para garantir eficiência, escalabilidade e economia nos gastos com nuvem.I


#### 2. Tipos de instâncias EC2

[O que é o Amazon EC2? - Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/concepts.html)

é muito importante o conhecimento de todas as máquinas EC2 disponíveis para sabermos exatamente qual se adapta melhor ao nosso cenário, é possível fazer uma estimativa dentro do site da própria aws, no pricing calculator:

[AWS Pricing Calculator](https://calculator.aws/#/createCalculator/ec2-enhancement)

---


#### 3. Otimização de recursos

- otimizar recurso é poupar custos na aws;
- mesmo otimizando um recurso computacional, onde melhoramos o desempenho do sistema, estamos poupando custo, pois isso traz ganho para a nossa solução na nuvem.
- podemos remover recursos ociosos ou não utilizados, e se não há uso, desligar.

---

**Escalar recursos**

nós executamos o scale de recursor para processar os workloads em determinados momentos. temos a opção de aumentar ou diminuir de forma manual ou automática. 

- **escalando verticalmente:** significa aumentar ou diminuir a capacidade de um recurso em um mesmo nó e geralmente está relacionado a alterar o número de vCPUs, memória, storage, rede de uma instÂNCIa
- **escalando horizontalmente:** é quando você aumenta o número de recursos, adicionando mais uma instância para suportar a aplicação.

É possível adicionar capacidade (aumentar a escala verticalmente) para lidar com tarefas de computação pesada, como processos mensais ou anuais ou picos no tráfego do site. Quando o uso diminui, você pode reduzir a capacidade (reduzir a escala verticalmente) de novo.

---

#### 4. Amazon EBS

- é como se fosse um HD para uma instância EC2;
- com o EBS, é possível terr a capacidade de expansão de forma rápida;
- exemplo de uso: armazenamento de para DBs e armazenar dados para aplicativos web, logs e sistemas;


---

#### 5. Amazon S3

- é um serviço de armazenamento de objetos;
- ideal para armazenar, organizar e recuperar grandes volumes de dados de forma escalável;

----


#### 6. Criação e uso de imagens AMI (amazon machine image):

- o que é: uma ami é basicamente uma “foto” de uma máquina virtual na aws. ela contém o sistema operacional, pacotes, configurações e até apps que você quer usar.

- pra que serve: quando você lança uma instância ec2, você precisa de uma ami como base. é tipo escolher um modelo pronto da sua máquina.

- como criar: você sobe uma instância ec2, instala/configura o que precisa, e depois gera uma ami a partir dessa instância. isso salva todo o estado dela e pode ser usado pra lançar novas máquinas iguais.

vantagens:

- padronização (todas as instâncias lançam com a mesma config).

- agilidade (em vez de instalar tudo do zero, já vem pronto).

- backup/recuperação (se algo der ruim, dá pra lançar de novo a partir da ami).

- uso comum: automação de ambientes, clusters de servidores iguais, criação de ambientes de teste/produção idênticos.


---

#### 7. Snapshots EBS

o que é: um snapshot é uma cópia de backup de um volume ebs (elastic block store). ele guarda o estado do disco em um ponto no tempo.

- são incrementais: depois do primeiro snapshot (que pega tudo), os próximos só salvam as mudanças, economizando espaço e custo.

- ficam armazenados no s3 de forma gerenciada (você não vê direto no bucket).

pra que serve:

- restaurar volumes ebs em caso de falha.

- clonar volumes para criar novas instâncias.

- mover dados entre regiões ou contas (copiando snapshots).

uso comum:

- backup automático de bancos de dados.

- criar novos ambientes iguais (ex: criar um volume a partir de snapshot e anexar em outra ec2).

- disaster recovery (se o volume original quebrar, basta restaurar).

![diagrama aws](./docs/diagrama.svg)
