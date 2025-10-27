# AWS Distributed Orders Processor

## 📌 Proposta do Projeto

Este projeto tem como objetivo processar **pedidos em lote** de forma **distribuída e paralela**, utilizando os recursos da **AWS Step Functions** e **Lambda**, garantindo validação, aplicação de regras de precificação e checagem de estoque.

A solução é **serverless**, escalável e permite processar grandes volumes de pedidos de forma eficiente, registrando os resultados no **DynamoDB** e gerando um **resumo do batch** ao final.

---

## 🔄 Fluxo da Arquitetura

1. **Injeção de pedidos de exemplo (InjectSampleOrders)**

   * Os pedidos são carregados em JSON, incluindo `orderId`, `customerId`, `items` e regras de precificação.
   * Cada batch também possui metadados e identificador único (`batchId`).

2. **Validação em lote (ValidateBulkOrder)**

   * Um **AWS Lambda** valida todos os pedidos.
   * Apenas pedidos corretos seguem para o processamento distribuído.

3. **Processamento distribuído de pedidos (ProcessOrders)**

   * Cada pedido é processado **em paralelo** utilizando o **Distributed Map** do Step Functions.
   * Sub-fluxo de cada pedido:

     1. Inicialização de variáveis do batch.
     2. Checagem de estoque via Lambda.
     3. Aplicação de regras de precificação via Lambda.
     4. Roteamento:

        * Se estoque disponível → atualiza pedido no **DynamoDB** como `PROCESSING` com preço final.
        * Se problema de estoque → registra issue no **DynamoDB**.

4. **Geração do resumo do batch (GenerateBatchSummary)**

   * Lambda finaliza o fluxo, gerando estatísticas e resumo do batch processado.

---

## 🛠️ Serviços AWS Utilizados

* **AWS Step Functions (Distributed Map)** – Orquestração do fluxo distribuído de pedidos.
* **AWS Lambda** – Validação de pedidos, checagem de estoque, aplicação de regras de preço e geração de resumo.
* **Amazon DynamoDB** – Armazenamento de pedidos processados e registro de problemas.
* **Pass / Choice / Task States** – Tipos de estados do Step Functions:

  * **Pass:** inicializa dados e passa informações adiante.
  * **Task:** invoca funções Lambda ou atualiza DynamoDB.
  * **Choice:** realiza decisões condicionais no fluxo.

---

## 📊 Arquitetura

O fluxo completo da solução está representado no diagrama abaixo:

![Diagrama da Arquitetura](aws-distributed-orders.svg)
