# ☁️ AWS CloudFormation Stack

---

### **Descrição do Desafio**

Este projeto foi desenvolvido como parte do **Desafio de Projeto da DIO**, com o objetivo de **implementar a primeira stack na AWS utilizando o CloudFormation**.
A proposta é compreender o funcionamento do **Infrastructure as Code (IaC)** na prática — criando, versionando e documentando recursos da AWS de forma automatizada.

O entregável do desafio consiste em um **repositório organizado** contendo:

* O **template YAML** usado para criação da infraestrutura;
* **Capturas de tela** da execução e da instância criada;
* E **anotações e insights** adquiridos durante a prática.

---

### **Stack Criada**

Durante o desafio, criei uma **instância EC2 simples** utilizando o CloudFormation e o template da aula.

```yaml
Description: Criar um Amazon EC2 simples
Resources:
  MinhaInstancia:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0360c520857e3138f
      InstanceType: t3.micro
      Tags:
        - Key: "Name"
          Value: "EC2"
```

📸 **Prints** da criação e execução estão disponíveis na pasta `/prints`.

Outros templates de prática estão organizados na pasta `/stacks` — prontos para serem utilizados ou adaptados.

---

### **Execução do Template**

1. Acesse o serviço **AWS CloudFormation** no console da AWS.
2. Clique em **"Create stack" → "With new resources (standard)"**.
3. Faça o upload do arquivo `.yaml` localizado na pasta `/stacks`.
4. Avance pelas etapas de configuração e clique em **"Create stack"**.
5. Aguarde a criação da instância EC2 e valide no **EC2 Dashboard**.

> 💡 O upload foi realizado **manualmente via interface do CloudFormation** (sem CLI).

---

### **Estrutura do Repositório**

```txt
stack-cloudformation/
├── prints/                  # Capturas de tela da execução
├── stacks/                  # Outros scripts CloudFormation de prática
└── README.md                # Documentação do projeto
```

---

### **Insights e Aprendizados**

* O **CloudFormation** simplifica muito o processo de provisionamento de recursos, garantindo **reprodutibilidade e padronização**.
* É uma ferramenta essencial para **Infraestrutura como Código (IaC)**, permitindo versionar ambientes e automatizar implantações.
* Mesmo uma stack simples, como uma EC2, já demonstra o potencial da automação para o dia a dia de **desenvolvedores e DevOps**.
