# API E-commerce - Projeto Geração Tech 3.0

# 📋 Descrição do Projeto
A API E-commerce - Projeto Geração Tech 3.0 é uma aplicação backend robusta e escalável, desenvolvida para suportar operações completas de um sistema de e-commerce. Construída com tecnologias modernas, ela oferece uma arquitetura RESTful que facilita a integração com frontends e outras APIs, garantindo segurança, eficiência e manutenibilidade.

## Principais Funcionalidades
Gerenciamento de Usuários: Cadastro, autenticação via JWT e operações CRUD seguras, com criptografia de senhas.<br>
Gerenciamento de Categorias: Criação e organização de categorias de produtos, com suporte a filtros e exibição em menus.<br>
Gerenciamento de Produtos: CRUD avançado para produtos, incluindo associações com imagens, opções personalizáveis (como tamanhos e cores) e categorias múltiplas.<br>
Pesquisa Avançada: Filtros dinâmicos por texto, categorias, faixas de preço e opções específicas, com paginação eficiente.<br>
Documentação Interativa: Interface Swagger para exploração e teste de endpoints em tempo real.<br>

# Arquitetura e Tecnologias
### Plataforma
Node.js<br>
Express 5 (API REST)
### Banco de dados
PostgreSQL<br>
Sequelize ORM<br>
Sequelize CLI (dev dependency)
### Autenticação
jsonwebtoken (JWT)<br>
bcryptjs (hash de senha)
### API docs
swagger-jsdoc<br>
swagger-ui-express
### Utilidades
cors<br>
dotenv (variáveis de ambiente)<br>
nodemon (dev)<br>
### Testes
Jest (scripts de teste)

# 📦 Dependências (extração de package.json)
bcryptjs<br>
cors<br>
dotenv<br>
express<br>
jsonwebtoken<br>
pg<br>
pg-hstore<br>
sequelize<br> 
swagger-jsdoc<br> 
swagger-ui-express

# 🧩 DevDependencies
nodemon<br>
sequelize-cli

## Categorias
Produtos com imagens, opções e vínculo em categorias<br>
Pesquisa avançada (filtros por texto, categoria, preço e opções)


# 🎯 Requisitos do Projeto

## 1. Funcionalidades Essenciais

### Endpoints implementados:
/v1/usuario, /v1/categoria, /v1/produto<br>
/v1/usuario/token (login)<br>
CRUD completo para usuário, categoria e produto
### Autenticação/Autorização:
POST /v1/usuario/token gera token com jsonwebtoken<br>
Middleware auth (requer ajuste; hoje contém model Category incorreto, mas rotas usam authMiddleware)<br>
Erros e HTTP:
Status: 200/201/204/400/401/404/500 conforme esperado<br>
Respostas JSON claras ({error: ...} + details em alguns casos)<br>

### Transações: ProductService usa transação em create/update

## 2. Qualidade de Código

### Code clean:
controllers com responsabilidades claras<br>
service para lógica de produto complexa<br>
modelos Sequelize independentes

### Comentários:
Swagger docs e explicações de parâmetros<br>
structure coerente fácil de seguir<br>

### Organização:
MVC: models/controllers/routes<br>
src/database/index.js registra models e associações

## 3. Banco de Dados

### Modelos:
User: usuarios (nome, sobrenome, email único, senha criptografada via hook)<br>
Category: categorias (nome, slug único, use_in_menu)<br>
Product: produtos (nome, slug único, estoque, preço, desconto)<br>
ProductImage, ProductOption

### Relacionamentos:
produto-categoria (many-to-many via produtos_categorias)
inherits hasMany/BelongsTo

### Migrations:
no repo atual não há pasta migrations (identificado).
recomenda-se adicionar migrations via sequelize-cli.

### Consultas:
.findAndCountAll + include eficientes e query params<br>
DTOs com category_ids, images, paths

## 4. Documentação
Swagger (/api-docs)<br>
Decorated via @swagger em cada rota<br>
src/app.js config com swagger-jsdoc + swagger-ui-express

### Abordagem:
documentação dos endpoints<br>
parâmetros query/body/resposta<br>
README final (este conteúdo) cobre todo o setup e uso

# 🛠️ Setup

## Pré-requisitos
Node.js >= 18<br>
PostgreSQL<br>
npm<br>
### .env com:
Instalação<br> 
Rodar local<br>
API: http://localhost:3001<br>
Swagger: http://localhost:3001/api-docs

# Testes

npm test

# 🧾 Endpoints (resumo)

## Usuário
POST /v1/usuario (cadastro)<br>
POST /v1/usuario/token (login)<br>
GET /v1/usuario/:id<br>
PUT /v1/usuario/:id (auth)<br>
DELETE /v1/usuario/:id (auth)
## Categoria
GET /v1/categoria/pesquisa<br>
GET /v1/categoria/:id<br>
POST /v1/categoria (auth)<br>
PUT /v1/categoria/:id (auth)<br>
DELETE /v1/categoria/:id (auth)
## Produto
GET /v1/produto/pesquisa<br>
GET /v1/produto/:id<br>
POST /v1/produto (auth)<br>
PUT /v1/produto/:id (auth)<br>
DELETE /v1/produto/:id (auth)
## 🛠️ Tech Stack
```
- Node.js
- Express 5
- Sequelize + PostgreSQL
- JWT auth (`jsonwebtoken`)
- Hash de senha (`bcryptjs`)
- CORS (`cors`)
- Variáveis de ambiente (`dotenv`)
- Documentação Swagger (`swagger-jsdoc`, `swagger-ui-express`)
- Hot reload (`nodemon`)
- Migrations (`sequelize-cli`)
- Testes (`jest`)```