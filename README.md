# 🎥 API de Gerenciamento de Vídeos - Node.js do Zero

Uma API RESTful completa para gerenciamento de vídeos, construída do zero com Node.js, demonstrando conceitos fundamentais de desenvolvimento backend moderno.

## 📋 Sobre o Projeto

Esta API permite realizar operações CRUD (Create, Read, Update, Delete) em um catálogo de vídeos. O projeto foi desenvolvido com foco em aprendizado e demonstra a evolução de uma aplicação simples em memória para uma versão completa com banco de dados PostgreSQL.

### ✨ Funcionalidades

- ✅ **Criar vídeos** - Cadastrar novos vídeos com título, descrição e duração
- ✅ **Listar vídeos** - Buscar todos os vídeos ou filtrar por título
- ✅ **Atualizar vídeos** - Modificar informações de vídeos existentes
- ✅ **Deletar vídeos** - Remover vídeos do catálogo
- ✅ **Busca inteligente** - Filtrar vídeos por título usando ILIKE
- ✅ **Persistência de dados** - Armazenamento em banco PostgreSQL (Neon)

## 🛠️ Stack Tecnológica

### Backend

- **Node.js** - Runtime JavaScript
- **Fastify** - Framework web rápido e eficiente
- **PostgreSQL** - Banco de dados relacional

### Banco de Dados

- **Neon Database** - PostgreSQL serverless na nuvem
- **@neondatabase/serverless** - Driver otimizado para Neon

### Ferramentas de Desenvolvimento

- **ES Modules** - Sintaxe moderna de importação
- **dotenv** - Gerenciamento de variáveis de ambiente
- **REST Client** - Testes de API via arquivo `.http`

## 🚀 Como Utilizar

### Pré-requisitos

- Node.js (versão 18 ou superior)
- npm ou yarn
- Conta no [Neon Database](https://neon.tech/) (gratuita)

### 📦 Instalação

1. **Clone o repositório**

   ```bash
   git clone https://github.com/igortriveloni86/node-do-zero.git
   cd node-do-zero
   ```

2. **Instale as dependências**

   ```bash
   npm install
   ```

3. **Configure as variáveis de ambiente**

   Crie um arquivo `.env` na raiz do projeto:

   ```env
   DATABASE_URL='postgresql://username:password@host/database?sslmode=require'
   PORT=3333
   ```

4. **Crie a tabela no banco de dados**

   ```bash
   node create-table.js
   ```

5. **Inicie o servidor**

   ```bash
   # Modo desenvolvimento (com auto-reload)
   npm run dev

   # Modo produção
   npm start
   ```

O servidor estará rodando em `http://localhost:3333`

## 📡 Endpoints da API

### 📌 **POST** `/videos` - Criar vídeo

Cadastra um novo vídeo no sistema.

**Request Body:**

```json
{
  "title": "Meu Vídeo",
  "description": "Descrição do vídeo",
  "duration": 180
}
```

**Response:** `201 Created`

---

### 📌 **GET** `/videos` - Listar vídeos

Retorna todos os vídeos ou filtra por título.

**Query Parameters (opcional):**

- `search` - Busca por título (case-insensitive)

**Exemplos:**

```
GET /videos
GET /videos?search=node
```

**Response:** `200 OK`

```json
[
  {
    "id": "uuid",
    "title": "Meu Vídeo",
    "description": "Descrição do vídeo",
    "duration": 180
  }
]
```

---

### 📌 **PUT** `/videos/:id` - Atualizar vídeo

Atualiza as informações de um vídeo existente.

**Request Body:**

```json
{
  "title": "Título Atualizado",
  "description": "Nova descrição",
  "duration": 240
}
```

**Response:** `204 No Content`

---

### 📌 **DELETE** `/videos/:id` - Deletar vídeo

Remove um vídeo do sistema.

**Response:** `204 No Content`

## 🧪 Testando a API

O projeto inclui um arquivo `routes.http` com exemplos de todas as requisições. Para usar:

1. **VS Code:** Instale a extensão "REST Client"
2. **Abra o arquivo:** `routes.http`
3. **Clique em:** "Send Request" acima de cada requisição

### Exemplo de uso completo:

```http
# 1. Criar um vídeo
POST http://localhost:3333/videos
Content-Type: application/json

{
  "title": "Node.js Fundamentals",
  "description": "Curso completo de Node.js",
  "duration": 3600
}

###

# 2. Listar todos os vídeos
GET http://localhost:3333/videos

###

# 3. Buscar vídeos por título
GET http://localhost:3333/videos?search=node

###

# 4. Atualizar um vídeo (substitua o ID)
PUT http://localhost:3333/videos/uuid-aqui
Content-Type: application/json

{
  "title": "Node.js Avançado",
  "description": "Curso avançado de Node.js",
  "duration": 7200
}

###

# 5. Deletar um vídeo (substitua o ID)
DELETE http://localhost:3333/videos/uuid-aqui
```

## 📁 Estrutura do Projeto

```
node-do-zero/
├── 📄 server.js              # Servidor principal com rotas
├── 📄 database-postgres.js   # Classe de acesso ao PostgreSQL
├── 📄 database-memory.js     # Implementação em memória (para estudos)
├── 📄 db.js                  # Configuração da conexão com Neon
├── 📄 create-table.js        # Script para criar tabelas
├── 📄 routes.http            # Exemplos de requisições HTTP
├── 📄 .env                   # Variáveis de ambiente (não versionado)
├── 📄 package.json           # Dependências e scripts
└── 📄 README.md              # Documentação do projeto
```

## 🔄 Scripts Disponíveis

```bash
# Iniciar em modo desenvolvimento (auto-reload)
npm run dev

# Iniciar em modo produção
npm start

# Criar tabelas no banco
node create-table.js

# Verificar versão do Node.js
node -v
```

## 💾 Configuração do Banco de Dados

O projeto utiliza o **Neon Database**, uma plataforma PostgreSQL serverless:

1. **Crie uma conta gratuita** em [neon.tech](https://neon.tech/)
2. **Crie um novo projeto**
3. **Copie a connection string** e cole no arquivo `.env`
4. **Execute o script** `create-table.js` para criar as tabelas

### Estrutura da Tabela

```sql
CREATE TABLE videos (
    id TEXT PRIMARY KEY,
    title TEXT,
    description TEXT,
    duration INTEGER
);
```

## 🎯 Conceitos Demonstrados

- **ES Modules** - Sintaxe moderna de import/export
- **Async/Await** - Programação assíncrona
- **REST API** - Padrões de API RESTful
- **CRUD Operations** - Create, Read, Update, Delete
- **Environment Variables** - Configuração segura
- **Database Integration** - Conexão com PostgreSQL
- **Error Handling** - Tratamento de erros
- **Code Organization** - Separação de responsabilidades

## 🤝 Como Contribuir

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## 📝 Licença

Este projeto está sob a licença ISC. Veja o arquivo `package.json` para mais detalhes.

---

**Desenvolvido com ❤️ para aprender Node.js do zero!**

---

## 📞 Contato

- **GitHub:** [@igortriveloni86](https://github.com/igortriveloni86)
- **Projeto:** [node-do-zero](https://github.com/igortriveloni86/node-do-zero)

---

_Este projeto faz parte de uma jornada de aprendizado em desenvolvimento backend com Node.js, demonstrando desde conceitos básicos até implementações mais avançadas._
