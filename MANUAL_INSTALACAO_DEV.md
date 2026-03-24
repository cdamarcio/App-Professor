# Guia de Configuração do Ambiente de Desenvolvimento

## Pré-requisitos
- Docker & Docker Compose
- Node.js v18+ ou Flutter SDK (conforme stack escolhida)
- PostgreSQL 12+

## Passo a Passo
1. Clone o repositório: `git clone <url-repo>`
2. Configure o `.env` baseado no `.env.example`.
3. Suba o banco de dados: `docker-compose up -d`
4. Execute as migrações: `npm run migrate` ou `python manage.py migrate`
5. Inicie o servidor: `npm run dev`

## Comandos Úteis
- `npm test`: Executa a suíte de testes unitários.
- `npm run build`: Gera o pacote de produção.
