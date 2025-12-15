# README -- Infraestrutura AWS com CloudFormation (EC2 + ALB + RDS)

## Descrição do Projeto

Este projeto utiliza AWS CloudFormation para provisionar automaticamente
três recursos principais:

1.  Instância EC2 Linux\
2.  Application Load Balancer (ALB)\
3.  Banco de Dados RDS (MySQL)

A EC2 recebe tráfego do Load Balancer, e o RDS representa um banco
simples.

## Estrutura do Projeto

    /projeto-iac/
    │
    ├── template.yaml
    └── README.md

## Como Executar o Deploy

### Pré-requisitos

-   Conta AWS ativa
-   AWS CLI instalada (`aws configure`)
-   Permissões de CloudFormation, EC2, ELB e RDS

### Criar o Stack

    aws cloudformation create-stack   --stack-name meu-stack-cloudformation   --template-body file://template.yaml   --capabilities CAPABILITY_IAM

### Acompanhar

    aws cloudformation describe-stacks --stack-name meu-stack-cloudformation

## Testando

### Load Balancer

Acesse:

    http://DNS-do-load-balancer

### EC2

Verifique no console AWS → EC2

### Banco RDS

Verifique no console AWS → RDS

## Deletar a Infraestrutura

    aws cloudformation delete-stack --stack-name meu-stack-cloudformation

## Explicação dos Componentes

### VPC & Subnets

Cria: - 2 subnets públicas\
- 1 subnet privada para o RDS\
- Internet Gateway\
- Route Table pública

### Security Groups

-   ALB → HTTP 80 público\
-   EC2 → HTTP apenas do ALB\
-   RDS → Acesso apenas da EC2

### EC2

-   Amazon Linux 2\
-   Apache instalado via UserData

### ALB

-   Encaminha tráfego para a EC2 via Target Group

### RDS MySQL

-   Armazenamento 20GB\
-   Instância db.t3.micro\
-   Acesso privado

## Roteiro de Apresentação em Vídeo

1.  Abertura\
2.  Mostrar o template e explicar seções\
3.  Executar o deploy\
4.  Testar ALB, EC2 e RDS\
5.  Explicar como remover a stack\
6.  Encerrar
