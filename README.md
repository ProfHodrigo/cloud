# Computação em Nuvem

## Objetivo da Disciplina

Capacitar os alunos a entender e aplicar soluções baseadas em computação em nuvem, incluindo a infraestrutura, plataformas e software como serviço (IaaS, PaaS, SaaS). Os alunos aprenderão sobre a arquitetura de sistemas em nuvem, gestão de serviços, segurança, escalabilidade, custos, e as principais plataformas de nuvem disponíveis no mercado, como AWS, Azure e Google Cloud.

---

## Ferramentas Gratuitas Utilizadas

| Ferramenta | Uso | Como obter |
|---|---|---|
| **AWS Free Tier** | EC2, S3, Lambda, RDS, IAM, CloudWatch, Cost Explorer | Conta gratuita em [aws.amazon.com/free](https://aws.amazon.com/free) |
| **Azure for Students** | VMs, Blob Storage, Azure SQL, Functions | Conta gratuita com $100 de crédito em [azure.microsoft.com/free/students](https://azure.microsoft.com/en-us/free/students/) |
| **Google Cloud Free Tier** | Compute Engine, Cloud Storage, Cloud Functions | Conta gratuita em [cloud.google.com/free](https://cloud.google.com/free) |
| **Docker Desktop** | Containers locais | [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/) |
| **Minikube** | Kubernetes local | [minikube.sigs.k8s.io](https://minikube.sigs.k8s.io/) |
| **LocalStack** | Simulação de serviços AWS localmente (sem conta AWS) | [localstack.cloud](https://localstack.cloud/) - versão Community |
| **Draw.io** | Diagramas de arquitetura | [app.diagrams.net](https://app.diagrams.net/) |
| **GitHub** | Repositório de código e entregas | [github.com](https://github.com/) |

---

## Calendário de Exercícios

| Exercício | Atribuído na | Entrega na | Tema |
|---|---|---|---|
| Exercício 1 | Aula 01 | Aula 03 | Segurança - Políticas IAM |
| Exercício 2 | Aula 03 | Aula 05 | Escalabilidade e Alta Disponibilidade |
| Exercício 3 | Aula 05 | Aula 07 | Armazenamento e Banco de Dados |
| Exercício 4 | Aula 07 | Aula 09 | Containers e Serverless |
| Exercício 5 | Aula 09 | Semana 10 (Prova) | Projeto final - Arquitetura em Nuvem |

---

## Aulas

---

### Aula 01 - Segurança em Nuvem: Políticas e Proteção de Recursos

**Conteúdo:**

- Planejamento e implementação de políticas de segurança para proteger recursos em nuvem
- Modelos de responsabilidade compartilhada (shared responsibility model)
- Controle de acesso e gerenciamento de identidades (IAM)
- Demonstração ao vivo: criação de usuários, grupos e políticas no AWS IAM (Free Tier)

**Exercício 1 - Criando Políticas de Segurança com IAM**

> **Objetivo:** Criar uma estrutura básica de segurança usando o AWS IAM (Free Tier).
>
> **Passo a passo:**
> 1. Crie uma conta na AWS: [aws.amazon.com/free](https://aws.amazon.com/free)
> 2. Acesse o painel do IAM no console da AWS
> 3. Crie **2 usuários** fictícios: `aluno-admin` e `aluno-leitor`
> 4. Crie **2 grupos**: `Administradores` e `SomenteLeitura`
> 5. Atribua ao grupo `Administradores` a política `AdministratorAccess`
> 6. Atribua ao grupo `SomenteLeitura` a política `ReadOnlyAccess`
> 7. Adicione cada usuário ao grupo correspondente
> 8. **Entrega:** Tire prints de cada etapa e crie um documento (PDF ou Google Docs) explicando com suas palavras o que cada política permite fazer e por que separar permissões é importante
>
> **Alternativa sem conta AWS:** Use o [IAM Policy Simulator](https://policysim.aws.amazon.com/) para simular políticas e explique as diferenças de permissão.

---

### Aula 02 - Segurança em Nuvem: Monitoramento e Resposta a Incidentes

**Conteúdo:**

- Monitoramento e auditoria de segurança
- Ferramentas de log: AWS CloudTrail (Free Tier), Azure Activity Log, Google Cloud Audit Logs
- Detecção de intrusão e resposta a incidentes em ambientes de nuvem
- Demonstração ao vivo: visualizando logs de atividade no CloudTrail

---

### Aula 03 - Escalabilidade e Alta Disponibilidade em Nuvem

**Conteúdo:**

- Definição de escalabilidade: vertical (scale up) e horizontal (scale out)
- Estratégias de alta disponibilidade e tolerância a falhas: replicação, backup e failover
- Configuração de autoescalonamento e balanceamento de carga
- Dimensionamento de recursos de nuvem com base na demanda

**Exercício 2 - Simulando Escalabilidade e Alta Disponibilidade**

> **Objetivo:** Entender na prática como funciona a escalabilidade e o balanceamento de carga.
>
> **Passo a passo:**
> 1. Instale o Docker Desktop na sua máquina: [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
> 2. Crie um arquivo chamado `docker-compose.yml` com o conteúdo abaixo - ele sobe um servidor web (Nginx) com **3 réplicas** e um balanceador de carga simples:
>    ```yaml
>    version: '3'
>    services:
>      web:
>        image: nginx:alpine
>        deploy:
>          replicas: 3
>    ```
> 3. Execute no terminal: `docker compose up -d --scale web=3`
> 4. Verifique os containers rodando: `docker compose ps`
> 5. Agora simule aumento de demanda subindo para 5 réplicas: `docker compose up -d --scale web=5`
> 6. Depois reduza para 1 réplica: `docker compose up -d --scale web=1`
> 7. **Entrega:** Documente com prints cada etapa e responda:
>    - Qual a diferença entre escalabilidade vertical e horizontal?
>    - O que você acabou de fazer foi escalabilidade vertical ou horizontal? Por quê?
>    - O que aconteceria se um dos containers falhasse com 3 réplicas? E com apenas 1?

---

### Aula 04 - Recuperação de Desastres em Nuvem

**Conteúdo:**

- Estratégias de recuperação de desastres (DR) em soluções de nuvem
- RPO (Recovery Point Objective) e RTO (Recovery Time Objective)
- Planos de contingência e testes de recuperação
- Como implementar estratégias de recuperação de desastres em soluções de nuvem
- Discussão em grupo: "Se o data center da sua empresa pegasse fogo hoje, o que aconteceria?"

---

### Aula 05 - Armazenamento e Banco de Dados em Nuvem

**Conteúdo:**

- Soluções de armazenamento em nuvem: armazenamento de objetos (Amazon S3, Google Cloud Storage) e armazenamento em bloco (Amazon EBS, Azure Disks)
- Bancos de dados em nuvem: relacionais (RDS, Azure SQL, Cloud SQL) e NoSQL (DynamoDB, Google Bigtable)
- Serviços de banco de dados gerenciados e escalabilidade automática
- Integração de soluções de nuvem com bancos de dados locais ou híbridos
- Backup, restauração e recuperação de dados em nuvem

**Exercício 3 - Armazenamento de Arquivos no Amazon S3**

> **Objetivo:** Aprender a usar o armazenamento de objetos na nuvem para guardar e organizar arquivos.
>
> **Passo a passo:**
> 1. Acesse o console da AWS com sua conta Free Tier
> 2. Vá até o serviço **S3** (Simple Storage Service)
> 3. Crie um **bucket** com um nome único (ex: `meunome-cloud-aula05`)
> 4. Faça upload de **3 arquivos** diferentes (imagens, PDFs, textos - o que preferir)
> 5. Crie **2 pastas** dentro do bucket para organizar os arquivos (ex: `documentos/` e `imagens/`)
> 6. Mova os arquivos para as pastas correspondentes
> 7. Selecione um arquivo e gere um **link de acesso temporário** (Presigned URL)
> 8. **Entrega:** Documente com prints cada etapa e responda:
>    - Qual a diferença entre armazenamento de objetos (S3) e armazenamento em bloco (EBS)?
>    - Por que o nome do bucket precisa ser único no mundo inteiro?
>    - O link temporário que você gerou vai funcionar para sempre? Por quê?
>
> **Alternativa sem conta AWS:** Use o [LocalStack](https://localstack.cloud/) para simular o S3 localmente com o comando `awslocal s3 mb s3://meu-bucket`.

---

### Aula 06 - Implementação de Aplicações em Nuvem

**Conteúdo:**

- Modelos de implementação: aplicações monolíticas, microserviços, containers e serverless
- Deploy e gerenciamento de containers com Docker e Kubernetes
- Execução de funções sem servidor (serverless): AWS Lambda, Azure Functions, Google Cloud Functions
- Demonstração ao vivo: deploy de um container simples com Docker

---

### Aula 07 - Performance e Gerenciamento de APIs em Nuvem

**Conteúdo:**

- Otimização de performance de aplicativos em nuvem: caching, CDNs, compressão de dados
- Gerenciamento de APIs em nuvem: API Gateway, autenticação e versionamento

**Exercício 4 - Criando uma Função Serverless e Expondo via API**

> **Objetivo:** Criar uma função serverless simples e entender como funciona a execução sem servidor.
>
> **Passo a passo:**
> 1. Acesse o console da AWS -> serviço **Lambda**
> 2. Clique em **Criar função** -> selecione "Criar do zero"
> 3. Dê o nome `minha-primeira-funcao` e escolha o runtime **Python 3.x**
> 4. No editor de código, substitua o conteúdo pelo código abaixo:
>    ```python
>    def lambda_handler(event, context):
>        nome = event.get("nome", "Mundo")
>        return {
>            "statusCode": 200,
>            "body": f"Olá, {nome}! Esta resposta veio de uma função serverless."
>        }
>    ```
> 5. Clique em **Test**, crie um evento de teste com o JSON: `{"nome": "SeuNome"}`
> 6. Execute e veja o resultado
> 7. (Opcional) Vá até o **API Gateway**, crie uma API REST e conecte à sua função Lambda
> 8. **Entrega:** Documente com prints cada etapa e responda:
>    - O que significa "serverless"? Realmente não existe servidor?
>    - Quais as vantagens de usar Lambda em vez de manter um servidor EC2 ligado 24h?
>    - Em que situações serverless **não** seria uma boa escolha?
>
> **Alternativa sem conta AWS:** Use o [LocalStack](https://localstack.cloud/) para criar a função Lambda localmente.

---

### Aula 08 - Custos e Faturamento em Soluções de Nuvem

**Conteúdo:**

- Modelos de cobrança em nuvem: pay-per-use, assinatura, instâncias reservadas
- Planejamento e monitoramento de custos: AWS Cost Explorer, Azure Cost Management, Google Cloud Billing
- Estratégias para otimização de custos: dimensionamento adequado, instâncias spot, escalabilidade automática
- Análise de custo-benefício entre diferentes modelos de serviços e plataformas
- Casos de uso: análise de custos de grandes empresas que utilizam soluções de nuvem
- Atividade em aula: explorar a [Calculadora de Preços da AWS](https://calculator.aws/) e comparar custos de cenários diferentes

---

### Aula 09 - Tendências Emergentes em Computação em Nuvem

**Conteúdo:**

- Computação em nuvem híbrida e multicloud: integração de diferentes plataformas
- Edge Computing: computação descentralizada na borda da rede
- Inteligência Artificial e Machine Learning na nuvem: serviços de IA/ML das principais plataformas
- Containers e Kubernetes: tendências no gerenciamento de microserviços
- Soluções de nuvem para Big Data: armazenamento, processamento e análise de grandes volumes de dados

**Exercício 5 - Projeto Final: Planejamento de Arquitetura em Nuvem**

> **Objetivo:** Planejar uma arquitetura completa de nuvem para um cenário fictício, respeitando um orçamento definido.
>
> ---
>
> ### Orçamento
>
> Cada cenário tem um orçamento mensal máximo definido. Sua arquitetura **deve caber dentro desse limite**. Justifique as escolhas de acordo com as restrições financeiras. Esse é um dos maiores desafios do trabalho real em cloud.
>
> | Cenário | Orçamento mensal máximo |
> |---|---|
> | **A** — Loja virtual com picos na Black Friday | R$ 3.000 / mês ($600 US) |
> | **B** — App de saúde com dados sensíveis | R$ 2.000 / mês ($400 US) |
> | **C** — Startup de IA com recomendação de produtos | R$ 5.000 / mês ($1.000 US) |
>
> > **Observação:** O orçamento se refere ao custo em operação normal. Picos pontuais (ex: Black Friday no Cenário A) podem ultrapassar temporariamente o limite, desde que você explique no documento como isso ocorre e como seria controlado.
>
> ---
>
> ### Passo a passo
>
> 1. Escolha **um** dos cenários abaixo (ou fale comigo sobre algum outro):
>    - **Cenário A:** Uma loja virtual que espera picos de acesso na Black Friday
>    - **Cenário B:** Um aplicativo de saúde que armazena dados sensíveis de pacientes
>    - **Cenário C:** Uma startup que precisa rodar um modelo de IA para recomendação de produtos
> 2. Usando o [Draw.io](https://app.diagrams.net/), crie um **diagrama de arquitetura** que inclua:
>    - Onde a aplicação vai rodar (EC2, Lambda, containers?)
>    - Como os dados serão armazenados (S3, RDS, DynamoDB?)
>    - Como a segurança será garantida (IAM, VPC, criptografia?)
>    - Como o sistema escala com aumento de demanda
>    - Estratégia de backup / recuperação de desastres
> 3. Use a [Calculadora de Preços da AWS](https://calculator.aws/) para estimar o **custo mensal** da sua solução e confirmar que está dentro do orçamento do cenário escolhido
> 4. Escreva um documento curto (1~2 páginas) explicando:
>    - Por que escolheu cada serviço
>    - Como a arquitetura se encaixa no orçamento (mostre os principais itens de custo)
>    - Quais os riscos da sua arquitetura
>    - O que faria diferente com orçamento ilimitado
> 5. **Entrega:** Diagrama (imagem ou link do Draw.io) + documento + print da estimativa na Calculadora AWS

---

### Semana 10 - Prova Final

**Formato:** Avaliação escrita presencial - 2 horas

- Conteúdo cobrado: Aulas 01 a 09
- **Entrega do Exercício 5 (Projeto Final)** também realizada nesta semana
- Não haverá revisão - apenas a aplicação da prova

---
