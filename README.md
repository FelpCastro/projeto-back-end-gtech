# API E-commerce - Projeto Geração Tech 3.0

# 🧩 Descrição do Projeto

## API RESTful de e-commerce com:
Usuários com cadastro e login JWT

## Categorias
Produtos com imagens, opções e vínculo em categorias
Pesquisa avançada (filtros por texto, categoria, preço e opções)

# Arquitetura:
Node.js + Express
Sequelize (ORM)
PostgreSQL
Swagger (documentação)
JWT (autenticação)
Padrão MVC (rotas / controllers / modelos / serviços)

# 🎯 Requisitos do Projeto

## 1. Funcionalidades Essenciais

### Endpoints implementados:
/v1/usuario, /v1/categoria, /v1/produto
/v1/usuario/token (login)
CRUD completo para usuário, categoria e produto
### Autenticação/Autorização:
POST /v1/usuario/token gera token com jsonwebtoken
Middleware auth (requer ajuste; hoje contém model Category incorreto, mas rotas usam authMiddleware)
Erros e HTTP:
Status: 200/201/204/400/401/404/500 conforme esperado
Respostas JSON claras ({error: ...} + details em alguns casos)

### Transações: ProductService usa transação em create/update

## 2. Qualidade de Código

### Code clean:
controllers com responsabilidades claras
service para lógica de produto complexa
modelos Sequelize independentes

### Comentários:
Swagger docs e explicações de parâmetros
structure coerente fácil de seguir

### Organização:
MVC: models/controllers/routes
src/database/index.js registra models e associações

## 3. Banco de Dados

### Modelos:
User: usuarios (nome, sobrenome, email único, senha criptografada via hook)
Category: categorias (nome, slug único, use_in_menu)
Product: produtos (nome, slug único, estoque, preço, desconto)
ProductImage, ProductOption

### Relacionamentos:
produto-categoria (many-to-many via produtos_categorias)
inherits hasMany/BelongsTo

### Migrations:
no repo atual não há pasta migrations (identificado).
recomenda-se adicionar migrations via sequelize-cli.

### Consultas:
.findAndCountAll + include eficientes e query params
DTOs com category_ids, images, paths

## 4. Documentação
Swagger (/api-docs)
Decorated via @swagger em cada rota
src/app.js config com swagger-jsdoc + swagger-ui-express

### Abordagem:
documentação dos endpoints
parâmetros query/body/resposta
README final (este conteúdo) cobre todo o setup e uso

# 🛠️ Setup

## Pré-requisitos
Node.js >= 18
PostgreSQL
npm
.env com:
Instalação
Rodar local
API: http://localhost:3001
Swagger: http://localhost:3001/api-docs

# Testes

npm test

# 🧾 Endpoints (resumo)

## Usuário
POST /v1/usuario (cadastro)
POST /v1/usuario/token (login)
GET /v1/usuario/:id
PUT /v1/usuario/:id (auth)
DELETE /v1/usuario/:id (auth)
## Categoria
GET /v1/categoria/pesquisa
GET /v1/categoria/:id
POST /v1/categoria (auth)
PUT /v1/categoria/:id (auth)
DELETE /v1/categoria/:id (auth)
## Produto
GET /v1/produto/pesquisa
GET /v1/produto/:id
POST /v1/produto (auth)
PUT /v1/produto/:id (auth)
DELETE /v1/produto/:id (auth)
