# Aula 01 - Segurança em Nuvem: Políticas e Proteção de Recursos

**Computação em Nuvem**

---

## Agenda

1. Por que segurança em nuvem é importante?
2. Modelo de responsabilidade compartilhada
3. Gerenciamento de identidades (IAM)
4. Políticas e permissões
5. Boas práticas de segurança
6. Demonstração: AWS IAM
7. Exercício 1

---

## Por que segurança em nuvem é importante?

- Dados sensíveis estão fora do nosso controle físico
- Ataques a ambientes cloud crescem a cada ano
- Uma configuração errada pode expor dados de milhões de pessoas
- Exemplos de vazamentos:
  - **Capital One (2019):** 100 milhões de registros expostos por má configuração de firewall na AWS
  - **Facebook (2019):** 540 milhões de registros em servidor S3 público


---

## Segurança On-Premises vs Nuvem

| Aspecto | On-Premises | Nuvem |
|---|---|---|
| Controle físico | Total | Nenhum |
| Responsabilidade | 100% sua | Compartilhada |
| Atualizações | Manual | Automática (infra) |
| Custo de segurança | Alto (hardware) | Incluso em parte |
| Escalabilidade | Limitada | Sob demanda |

---

## Modelo de Responsabilidade Compartilhada

**O que é?** Um acordo que define o que o provedor protege e o que é responsabilidade do cliente.

### Responsabilidade do Provedor (AWS, Azure, GCP):
- Segurança física dos data centers
- Hardware, rede e infraestrutura
- Hypervisors e camada de virtualização

### Responsabilidade do Cliente:
- Dados e criptografia
- Gerenciamento de identidades e acessos
- Configuração de firewall e redes
- Atualizações do sistema operacional (em IaaS)

---

## Modelo de Responsabilidade Compartilhada - Diagrama

![Modelo de Responsabilidade Compartilhada AWS](https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg)

> Fonte: AWS - Shared Responsibility Model

---

## Responsabilidade muda conforme o modelo de serviço

| Camada | IaaS | PaaS | SaaS |
|---|---|---|---|
| Dados | Cliente | Cliente | Cliente |
| Aplicação | Cliente | Cliente | Provedor |
| Sistema Operacional | Cliente | Provedor | Provedor |
| Rede / Firewall | Cliente | Provedor | Provedor |
| Infraestrutura Física | Provedor | Provedor | Provedor |

**Quanto mais gerenciado o serviço, menos você precisa se preocupar com a infra, mas seus dados são SEMPRE sua responsabilidade.**

---

## O que é IAM?

**IAM = Identity and Access Management**

É o sistema que controla **quem** pode fazer **o quê** nos seus recursos de nuvem.

### Conceitos principais:

- **Usuário (User):** Uma pessoa ou aplicação com credenciais
- **Grupo (Group):** Conjunto de usuários com as mesmas permissões
- **Função/Role (Role):** Permissões temporárias que podem ser assumidas
- **Política (Policy):** Documento JSON que define o que é permitido ou negado

---

## IAM - Analogia Simples

Imagine um **prédio comercial:**

| Conceito IAM | Analogia |
|---|---|
| **Usuário** | Uma pessoa com crachá |
| **Grupo** | Departamento (todos do RH têm o mesmo acesso) |
| **Política** | As regras do crachá (quais portas abre) |
| **Role** | Um crachá temporário para visitantes |
| **MFA** | Além do crachá, precisa da digital |

---

## Anatomia de uma Política IAM (AWS)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

### Traduzindo:
- **Effect:** Permitir (`Allow`) ou Negar (`Deny`)
- **Action:** O que pode fazer -> `s3:GetObject` = ler arquivos do S3
- **Resource:** Em qual recurso -> apenas no bucket `meu-bucket`

---

## Princípio do Menor Privilégio

**"Dê a cada pessoa apenas as permissões que ela precisa e nada mais."**

### Exemplo prático:

❌ **Errado:** Dar `AdministratorAccess` para todo mundo

✅ **Certo:** O estagiário do marketing só precisa ler relatórios -> `ReadOnlyAccess`

### Por quê?
- Se uma conta for comprometida, o dano é limitado
- Reduz o risco de erros acidentais (alguém deletar um servidor sem querer)

---

## Políticas Gerenciadas vs Inline

### Políticas Gerenciadas (Managed Policies)
- Pré-criadas pela AWS ou por você
- Podem ser reutilizadas em múltiplos usuários/grupos
- Exemplos: `AdministratorAccess`, `ReadOnlyAccess`, `AmazonS3ReadOnlyAccess`

### Políticas Inline
- Criadas diretamente dentro de um usuário/grupo
- Não podem ser reutilizadas
- Úteis para regras muito específicas

**Recomendação:** Use **Políticas Gerenciadas** sempre que possível.

---

## MFA - Autenticação Multifator

**MFA = Multi-Factor Authentication**

Adiciona uma camada extra de segurança além da senha.

### Como funciona:
1. Você digita seu usuário e senha
2. O sistema pede um **código temporário** de 6 dígitos
3. Esse código vem de um app no celular (Google Authenticator, Authy)

### Por que usar?
- Mesmo que alguém descubra sua senha, não consegue entrar sem o código
- **Obrigatório** para a conta root da AWS

---

## Boas Práticas de Segurança em Nuvem

1. **Nunca use a conta root** para tarefas do dia a dia
2. **Ative MFA** em todas as contas, especialmente a root
3. **Use grupos** em vez de atribuir permissões diretamente a usuários
4. **Aplique o menor privilégio** - comece com zero permissões e vá adicionando
5. **Rotacione credenciais** regularmente (chaves de acesso)
6. **Nunca coloque credenciais no código-fonte** (use variáveis de ambiente)
7. **Monitore atividades** com CloudTrail, Azure Monitor, etc.

---

## Demonstração

### Criando usuários, grupos e políticas no AWS IAM

1. Acessar o console AWS -> IAM
2. Criar grupo `Administradores` com política `AdministratorAccess`
3. Criar grupo `SomenteLeitura` com política `ReadOnlyAccess`
4. Criar usuário `aluno-admin` -> adicionar ao grupo `Administradores`
5. Criar usuário `aluno-leitor` -> adicionar ao grupo `SomenteLeitura`
6. Testar permissões de cada usuário

---

## Exercício 1 - Criando Políticas de Segurança com IAM

**Prazo:** 2 semanas (entrega na Aula 03)

### Passo a passo:
1. Crie uma conta na AWS: [aws.amazon.com/free](https://aws.amazon.com/free)
2. Acesse o painel do IAM
3. Crie **2 usuários:** `aluno-admin` e `aluno-leitor`
4. Crie **2 grupos:** `Administradores` e `SomenteLeitura`
5. Atribua as políticas `AdministratorAccess` e `ReadOnlyAccess`
6. Adicione cada usuário ao grupo correspondente

### Entrega:
- Prints de cada etapa
- Documento explicando o que cada política permite e por que separar permissões é importante

> **Dica:** Usem o [IAM Policy Simulator](https://policysim.aws.amazon.com/)

> **Entrega:** Entregar antes da Aula 03

---

## Resumo da Aula

| Conceito | O que aprendemos |
|---|---|
| Responsabilidade compartilhada | Provedor cuida da infra, você cuida dos dados e acessos |
| IAM | Sistema que controla quem faz o quê |
| Políticas | Documentos JSON que definem permissões |
| Menor privilégio | Dar apenas as permissões necessárias |
| MFA | Camada extra de segurança |

---

## Próxima Aula

**Aula 02 - Segurança em Nuvem: Monitoramento e Resposta a Incidentes**

- Como monitorar tudo que acontece na sua conta cloud
- Ferramentas de log (CloudTrail, Azure Activity Log)
- O que fazer quando algo dá errado
