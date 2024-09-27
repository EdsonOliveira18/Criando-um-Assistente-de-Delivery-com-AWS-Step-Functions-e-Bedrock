# Desafio: Criando um Assistente de Delivery com AWS Step Functions e Bedrock

## Descrição do Projeto

Este projeto tem como objetivo criar um assistente de delivery utilizando **AWS Step Functions** e **Bedrock**. O assistente será capaz de gerenciar a lógica de entrega, desde o recebimento do pedido até a confirmação da entrega, orquestrando diferentes serviços da AWS para realizar essas tarefas. 

O uso de **AWS Step Functions** permitirá criar fluxos de trabalho complexos, enquanto o **Bedrock** irá fornecer a inteligência necessária para lidar com decisões automatizadas, como rotas de entrega e estimativa de tempo.

## Arquitetura do Sistema

A solução é composta pelas seguintes camadas:

1. **AWS Step Functions**: Orquestra as etapas do processo de entrega.
2. **AWS Lambda**: Responsável por executar funções específicas como o cálculo da rota de entrega.
3. **Amazon DynamoDB**: Armazena informações sobre os pedidos e status de entrega.
4. **Amazon Bedrock**: Fornece os modelos de IA para otimização de rotas e previsão de entrega.
5. **Amazon S3**: Armazena logs e relatórios das entregas realizadas.

## Funcionalidades

- **Criação de Pedidos**: O sistema registra os detalhes do pedido (cliente, itens, endereço).
- **Otimização de Rotas**: O Bedrock sugere a melhor rota de entrega com base em fatores como tráfego e distância.
- **Atualização de Status**: A cada etapa da entrega, o status do pedido é atualizado no DynamoDB.
- **Confirmação de Entrega**: Quando o pedido é entregue, o assistente atualiza o status para "Concluído" e envia uma notificação.

## Requisitos

- **AWS Account** com permissões adequadas para criar e gerenciar serviços AWS (Step Functions, Lambda, DynamoDB, Bedrock, S3).
- **AWS CLI** ou acesso ao console AWS.
- **Node.js** para desenvolvimento e teste de funções Lambda localmente (opcional).
- **Python 3.x** (opcional) para scripts auxiliares.
- **Terraform** (opcional) para infraestrutura como código.

## Configuração do Ambiente

1. **Clone o repositório**:
    ```bash
    git clone https://github.com/EdsonOliveira18/Criando-um-Assistente-de-Delivery-com-AWS-Step-Functions-e-Bedrock.git
    ```

2. **Configure as credenciais da AWS**:
    Certifique-se de que suas credenciais AWS estejam configuradas corretamente em seu ambiente. Você pode usar o `aws configure` ou configurar variáveis de ambiente diretamente.

3. **Criação de recursos via AWS Console**:
    - Crie uma **State Machine** no **AWS Step Functions** para orquestrar o fluxo de trabalho.
    - Crie funções **AWS Lambda** para executar tarefas específicas, como o cálculo da rota.
    - Configure uma tabela **DynamoDB** para armazenar os dados dos pedidos e status.
    - Crie um **Bucket S3** para armazenar logs e relatórios.
    - Configure o **Bedrock** para realizar a otimização de rotas.

## Deploy

Se preferir, você pode usar o **AWS CloudFormation** ou **Terraform** para automatizar o provisionamento dos recursos da AWS.

### Usando Terraform

1. **Instale o Terraform** se ainda não o tiver:
    ```bash
    brew install terraform
    ```

2. **Inicialize o Terraform** no diretório do projeto:
    ```bash
    terraform init
    ```

3. **Aplique a infraestrutura**:
    ```bash
    terraform apply
    ```

## Fluxo de Trabalho

1. **Recebimento de Pedido**: O cliente envia um pedido, que é recebido pela função Lambda de entrada e registrado no DynamoDB.
2. **Otimização de Rota**: O Bedrock calcula a melhor rota para entrega e atualiza a tabela DynamoDB.
3. **Início da Entrega**: A Step Function inicia o processo de entrega, passando por diferentes etapas (retirada, transporte, entrega).
4. **Confirmação de Entrega**: Após a conclusão, o status do pedido é atualizado e uma notificação é enviada ao cliente.

## Exemplo de Execução

Aqui está um exemplo de JSON de entrada para a Step Function:

```json
{
  "pedidoId": "123456",
  "cliente": {
    "nome": "João Silva",
    "endereco": "Rua das Flores, 100, São Paulo, SP"
  },
  "itens": [
    { "nome": "Pizza de Calabresa", "quantidade": 1 },
    { "nome": "Refrigerante 2L", "quantidade": 1 }
  ]
}
```
