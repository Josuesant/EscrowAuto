# 🚀 Escrow Seguro Auto
A Escrow Seguro Auto é uma FinTech/LegalTech brasileira focada em eliminar fraudes no mercado C2C (venda entre pessoas físicas) de veículos usados. O mercado brasileiro movimenta mais de 9 milhões de transferências anuais, porém sofre com golpes de engenharia social e falta de garantia financeira.

Nossa solução utiliza uma **Conta Custódia (Escrow)** digital integrada a um **Gatilho Inteligente** que consulta bases oficiais (SERPRO/RENAVAM) para garantir que o dinheiro só chegue ao vendedor quando a propriedade for legalmente transferida ao comprador.

---

## 🧱 Arquitetura do Sistema

O projeto utiliza uma abordagem de **Monorepo de Microserviços** com **Clean Architecture**, garantindo separação de domínios e prontidão para auditorias de segurança (ISO 27001).

```
escrow-backend/
├── src/
│   ├── Services/
│   │   ├── Transaction/              # Core: Gestão de taxas e Orquestração 
│   │   │   ├── Transaction.Api
│   │   │   ├── Transaction.Application
│   │   │   ├── Transaction.Domain
│   │   │   └── Transaction.Infrastructure
│   │   ├── Vehicle/                  # Integração SERPRO/RENAVAM e Laudos ECV [cite: 14, 57, 59]
│   │   │   ├── Vehicle.Api
│   │   │   ├── Vehicle.Application
│   │   │   ├── Vehicle.Domain
│   │   │   └── Vehicle.Infrastructure
│   │   └── Identity/                 # KYC, Biometria e Conformidade LGPD [cite: 57, 92, 107]
│   │       ├── Identity.Api
│   │       ├── Identity.Application
│   │       ├── Identity.Domain
│   │       └── Identity.Infrastructure
│   └── Shared/                       # Kernel compartilhado (Cross-cutting)
└── docker-compose.yml

```

---

## 🖥️ Backend

### 🛠️ Stack Tecnológica

* **Backend: .NET 8 (Minimal APIs) com Entity Framework Core.**
* **Frontend: React + TypeScript + Tailwind CSS (com foco em componentes shadcn/ui).**
* **Dados: PostgreSQL para persistência e Redis para cache de consultas RENAVAM.**
* **Segurança: Autenticação via JWT e integração com e-CNPJ.**
* **Regulatório: Em conformidade com a Portaria SENATRAN 139/2025.**
---

### Responsabilidades

* Gestão de contratos de escrow
* Controle de estados (criado, em custódia, liberado, cancelado)
* Regras de liberação de valores
* Integração futura com gateways de pagamento
---

## 🔄 Fluxo de Confiança (Gatilho Automático)

Diferente de escrows comuns, nosso sistema atua como árbitro técnico:
  1. **Validação:** KYC das partes e checagem de débitos do veículo via RENAVAM.
  2. **Custódia:** O comprador deposita o valor em conta individualizada no Parceiro IP.
  3. **Vistoria:** O vendedor anexa o Laudo de Vistoria Cautelar (ECV) aprovado.
  4. **Gatilho SERPRO:** O sistema monitora o RENAVAM a cada 60 minutos.
  5. **Liquidação:** Assim que a propriedade consta em nome do comprador, o sistema retém o fee de 0,8% e libera o saldo ao vendedor.
  6. **Arbitragem:** Em caso de divergência, o conflito é mediado por uma Câmara de Arbitragem Digital parceira.

## 🧪 Como Executar
**Pré-requisitos**

  Docker & Docker Compose
  SDK .NET 8

  **Setup**
  # Clone o repositório
  git clone https://github.com/seu-usuario/escrow-seguro-auto.git
  
  # Suba a infraestrutura (Banco de Dados)
  docker-compose up -d
  
  # Execute o serviço de Transações
  cd src/Services/Transaction/Transaction.Api
  dotnet run


## Fluxo básico:

1. Comprador cria uma transação
2. Valor fica **em custódia**
3. Vendedor entrega o serviço/produto
4. Comprador confirma
5. Valor é liberado

---

## 📦 Status do Projeto

🚧 **Em desenvolvimento inicial**

Funcionalidades planejadas:

* [ ] Cadastro de usuários
* [ ] Criação de contratos de escrow
* [ ] Estados e transições seguras
* [ ] Autorização baseada em papéis
* [ ] Histórico e auditoria
* [ ] Integração com gateway de pagamento
* [ ] Frontend com dashboard

## 📄 Licença

Este projeto está sob a licença **MIT**.

## 📫 Contato

Projeto criado por **Josué Santos**.

> Construindo uma plataforma segura, simples e confiável para transações digitais.
