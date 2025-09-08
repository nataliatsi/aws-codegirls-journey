# AWS Diagram Certificates

## 📌 Proposta do Projeto

Este projeto foi desenvolvido como parte do desafio da **DIO (Santander Code Girls)**, cujo objetivo é **escolher um case de aplicação e modelar sua arquitetura na AWS**.

O case escolhido foi a modelagem de uma plataforma de **geração e envio automático de certificados digitais**, aproveitando serviços **serverless** e recursos nativos da nuvem para criar uma solução escalável, segura e de baixo custo.

---

## 🔄 Fluxo da Arquitetura

1. **Upload de arquivo pelo cliente**

   * O cliente acessa a interface web, realiza login e envia um arquivo (CSV, JSON ou XLSX).
   * O arquivo é armazenado em um bucket **Amazon S3**.

2. **Processamento inicial (Lambda 1)**

   * Um **AWS Lambda (Java)** é acionado pelo upload.
   * Ele processa os dados e salva as informações de usuários, eventos e certificados no **Amazon RDS** (controle, consultas e auditoria).
   * Em seguida, publica mensagens na fila **Amazon SQS** para dar continuidade ao fluxo.

3. **Geração e envio de certificados (Lambda 2)**

   * Outro **AWS Lambda** consome mensagens da **SQS**.
   * Ele gera os certificados digitais, salva em um bucket S3 específico e envia um e-mail com o link de acesso ao usuário.

4. **Acesso ao certificado**

   * O usuário acessa o link recebido por e-mail e realiza o download do certificado armazenado no **S3**.

---

## 🛠️ Serviços AWS Utilizados

* **Amazon S3** – Armazenamento de arquivos de entrada e certificados gerados.
* **AWS Lambda** – Funções serverless para processamento e envio.
* **Amazon RDS** – Banco de dados para auditoria, controle de eventos e usuários.
* **Amazon SQS** – Orquestração e comunicação entre Lambdas.

---

## 📊 Arquitetura

O fluxo completo da solução está representado no diagrama abaixo:

<img src="AWS diagram certificates.svg" alt="Diagrama da Arquitetura" width="700"/>
