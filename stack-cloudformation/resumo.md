# ☁️ AWS CloudFormation — Anotações e Resumo

> 💡 [Acessar prática do laboratório das aulas anteriores](../stack-cloudformation/stacks/)

---

## O que é o AWS CloudFormation?

O **AWS CloudFormation** é um serviço que permite **criar e gerenciar infraestrutura como código (IaC)**.  
Em vez de configurar recursos manualmente no console, a gente descreve tudo num **modelo (template)** — e o CloudFormation se encarrega de **provisionar, atualizar e excluir** os recursos de forma automatizada. 🚀

Basicamente:  
👉 você escreve o que quer (VPC, EC2, S3, RDS, etc.)  
👉 o CloudFormation lê o modelo  
👉 e cria tudo pra você, na ordem certa e com dependências resolvidas.

---

## Benefícios do CloudFormation

- **Automação total:** cria toda a infraestrutura com um comando.
- **Reprodutibilidade:** o mesmo modelo pode ser usado em várias contas ou regiões.
- **Controle de versão:** os modelos podem ser versionados no Git.
- **Consistência:** garante que todos os ambientes fiquem idênticos.
- **Rollback automático:** se algo falhar durante a criação da stack, ele desfaz tudo e mantém o ambiente limpo.  
- **Integração com outros serviços AWS:** dá pra usar junto com CodePipeline, CloudWatch, etc.

💬 *Resumindo:* menos cliques manuais, mais confiança na infraestrutura. 🫵😎

---

## Formatos dos modelos

Você pode escrever os modelos do CloudFormation em dois formatos:

1. **YAML (.yaml ou .yml)** — mais limpo e legível, o mais usado hoje.
2. **JSON (.json)** — funcional, mas mais verboso (e difícil de ler).

Exemplo básico em **YAML**:

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-exemplo
````

---

## Criando uma Stack

Uma **stack** é o conjunto de recursos criados a partir de um modelo.
Pra criar uma stack, dá pra usar:

* O **Console da AWS** (clicando em *Create stack*) 🖱️
* O **AWS CLI** (com `aws cloudformation create-stack`) 💻
* Ou até pipelines automatizadas (ex: CodePipeline + CloudFormation)

Durante a criação, o serviço lê o template, valida tudo e provisiona os recursos definidos.
Dá pra acompanhar o status (CREATE_IN_PROGRESS, CREATE_COMPLETE, etc.) pelo console.

---

## CloudFormation vs Terraform

| Característica    | CloudFormation                          | Terraform                                   |
| ----------------- | --------------------------------------- | ------------------------------------------- |
| 🔧 Provedor       | AWS (nativo)                            | Multi-cloud (AWS, Azure, GCP, etc.)         |
| 💬 Linguagem      | YAML / JSON                             | HCL (HashiCorp Configuration Language)      |
| 🧠 Estado (state) | Gerenciado automaticamente pela AWS     | Gerenciado manualmente (arquivo `.tfstate`) |
| 🌍 Portabilidade  | Somente AWS                             | Alta portabilidade                          |
| 🔄 Atualizações   | Stack Updates (Change Sets)             | `terraform plan` e `apply`                  |
| 💸 Custo          | Grátis (paga só pelos recursos criados) | Grátis também                               |

👉 **Resumo prático:**

* Se o foco é **AWS pura**, CloudFormation é ótimo.
* Se a ideia é **multi-cloud** ou ter mais controle sobre o *state*, Terraform é mais flexível.

---

## Insight pessoal

Fazer a prática me ajudou a entender de vez o conceito de **Infraestrutura como Código (IaC)** — ver os recursos sendo criados automaticamente foi beeem legal ✨
Antes eu achava que era algo super complexo, mas com CloudFormation ficou claro que é só descrever o que a gente quer e deixar a AWS trabalhar por nós.

---

✍️ *Anotação final:*

> IaC é o futuro — e CloudFormation é a forma da AWS mostrar como automatização e organização podem caminhar juntas.
> “Se dá pra codar, não precisa clicar!” 🫵
