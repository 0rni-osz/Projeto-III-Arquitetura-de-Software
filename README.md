# E-commerce — Projeto 3

API de e-commerce em Node.js + TypeScript com InversifyJS, Prisma (PostgreSQL), Docker Compose e arquitetura em camadas (`dev` e `test`).

## Como rodar

1. Copie o arquivo de variáveis de ambiente:

```bash
cp .env.example .env
```

2. Suba o banco de dados PostgreSQL e a API com o Docker Compose:

```bash
docker compose up --build
```

A API sobe em `http://localhost:3000`.

### Exemplos de uso

Criar um pedido (`POST /orders`):

```bash
curl -X POST http://localhost:3000/orders \
  -H "Content-Type: application/json" \
  -d '{
    "customer": "cliente@ethereal.email",
    "items": [{ "productId": 1, "quantity": 1 }],
    "paymentMethod": "pix"
  }'
```

Consultar um pedido pelo ID (`GET /orders/:id` — retorna `200` ou `404`):

```bash
curl http://localhost:3000/orders/1
```

Para parar os containers mantendo os dados salvos no volume:

```bash
docker compose down
```

## Estrutura

```text
src/
├── container/     # o único lugar com classes concretas
├── domain/        # produtos, pedido e erros de negócio
├── repositories/  # interfaces e implementações (Prisma e memória)
├── providers/     # e-mail (Ethereal e console)
├── payments/      # formas de pagamento
├── services/      # regras de negócio
├── controllers/   # só HTTP
└── app.ts         # rotas
```