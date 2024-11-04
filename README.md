# EngeLab

## Visão Geral

**EngenLab** é uma aplicação de geração de laudos técnicos para engenheiros, projetada com uma arquitetura de microserviços para escalabilidade e alta disponibilidade. A aplicação inclui uma interface frontend para criação e visualização de laudos, além de múltiplos microserviços backend para gerenciamento de autenticação, laudos, usuários, e relatórios.

## Arquitetura da Aplicação

### Componentes Principais

1. **Frontend (React ou Vue)**: Interface do usuário onde engenheiros podem gerar e visualizar laudos.
   - Hospedado em um bucket Amazon S3, com distribuição via CloudFront.

2. **API Gateway**: Usado para gerenciar o tráfego e rotear para os microserviços correspondentes.

3. **Microserviços Backend**:
   - **Serviço de Autenticação**: Gerencia login e permissões com integração ao AWS Cognito.
   - **Serviço de Laudos**: Responsável pela criação e gerenciamento dos laudos técnicos.
   - **Serviço de Usuários**: Gerencia perfis e permissões dos engenheiros.
   - **Serviço de Relatórios**: Gerencia relatórios e históricos, com armazenamento em AWS S3.

4. **Banco de Dados**:
   - **Amazon RDS (PostgreSQL)** para dados relacionais.
   - **Amazon DynamoDB** para dados não-relacionais.

5. **Mensageria**: Amazon SQS ou SNS para comunicação entre microserviços, garantindo processamento assíncrono de atualizações e relatórios.

6. **Monitoramento e Logs**: AWS CloudWatch para monitoramento, logs e alertas de performance.

## Arquitetura na AWS

A aplicação será implantada com os seguintes componentes na AWS:

- **Frontend**: Amazon S3 e CloudFront.
- **Backend**: AWS API Gateway, AWS Lambda ou ECS Fargate.
- **Autenticação**: AWS Cognito.
- **Banco de Dados**: Amazon RDS (PostgreSQL) e DynamoDB.
- **Mensageria**: Amazon SQS/SNS.
- **Monitoramento**: AWS CloudWatch.

## Pipeline CI/CD com GitHub Actions

O pipeline no GitHub Actions incluirá:

1. **Build**: Construção das imagens Docker para os microserviços.
2. **Testes Automatizados**: Execução de testes unitários e de integração.
3. **Deploy**:
   - Atualização do frontend no S3 e invalidação do cache no CloudFront.
   - Atualização dos microserviços via AWS ECS ou Lambda.
4. **Banco de Dados e Mensageria**: Configurados via Terraform ou CloudFormation para gerenciar a infraestrutura.

## Tecnologias e Ferramentas

- **Frontend**: React ou Vue, Tailwind CSS ou Bootstrap.
- **Backend**: Node.js (Express ou NestJS).
- **Banco de Dados**: Amazon RDS (PostgreSQL) e DynamoDB.
- **CI/CD**: GitHub Actions, Docker, Terraform/CloudFormation para infraestrutura.

---

## Estrutura de Diretórios

```plaintext
EngenLab
├── frontend/               # Aplicação frontend em React ou Vue
├── services/
│   ├── auth-service/       # Serviço de autenticação
│   ├── report-service/     # Serviço de geração de laudos
│   ├── user-service/       # Serviço de gestão de usuários
│   ├── document-service/   # Serviço de relatórios e históricos
├── infra/                  # Configuração da infraestrutura como código (Terraform/CloudFormation)
└── .github/
    └── workflows/          # Workflows do GitHub Actions para CI/CD
