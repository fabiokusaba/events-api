# API RESTful de Gerenciamento de Eventos

Uma API RESTful desenvolvida em Go para gerenciamento de eventos, utilizando Gin como framework web, SQLite como banco de dados, JWT para autenticação e sistema de migrations.

## 🚀 Tecnologias Utilizadas

- **Go** - Linguagem de programação
- **Gin** - Framework web HTTP
- **SQLite** - Banco de dados
- **JWT** - Autenticação e autorização
- **Migrations** - Controle de versão do banco de dados

## 📋 Funcionalidades

- ✅ Cadastro e autenticação de usuários
- ✅ CRUD completo de eventos
- ✅ Autenticação JWT
- ✅ Autorização baseada em roles
- ✅ Migrations automáticas
- ✅ Validação de dados

## 📚 Endpoints da API

### Autenticação

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/api/v1/auth/register` | Cadastrar usuário |
| POST | `/api/v1/auth/login` | Login do usuário |

### Eventos

| Método | Endpoint | Descrição | Auth |
|--------|----------|-----------|------|
| GET | `/api/v1/events` | Listar eventos | ❌ |
| GET | `/api/v1/events/:id` | Obter evento por ID | ❌ |
| POST | `/api/v1/events` | Criar evento | ✅ |
| PUT | `/api/v1/events/:id` | Atualizar evento | ✅ |
| DELETE | `/api/v1/events/:id` | Deletar evento | ✅ |

## 📝 Exemplos de Uso

### Cadastro de Usuário

```bash
curl -X POST http://localhost:8080/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "João Silva",
    "email": "joao@email.com",
    "password": "senha123"
  }'
```

### Login

```bash
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "joao@email.com",
    "password": "senha123"
  }'
```

### Criar Evento

```bash
curl -X POST http://localhost:8080"/api/v1/events" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer SEU_JWT_TOKEN" \
  -d '{
    "name": "Go Conference",
    "description": "A conference about Go programming",
    "date": "2025-06-01",
    "location": "San Francisco"
  }'
```

### Listar Eventos

```bash
curl -X GET http://localhost:8080"/api/v1/events"
```

## 🗄️ Estrutura do Banco de Dados

### Tabela: users
```sql
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    email TEXT NOT NULL UNIQUE,
    name TEXT NOT NULL,
    password TEXT NOT NULL
);
```

### Tabela: events
```sql
CREATE TABLE IF NOT EXISTS events (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    owner_id INTEGER NOT NULL,
    name TEXT NOT NULL,
    description TEXT NOT NULL,
    date DATETIME NOT NULL,
    location TEXT NOT NULL,
    FOREIGN KEY (owner_id) REFERENCES users (id) ON DELETE CASCADE
);
```

### Tabela: attendees
```sql
CREATE TABLE IF NOT EXISTS attendees (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL,
    event_id INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users (id) ON DELETE CASCADE,
    FOREIGN KEY (event_id) REFERENCES events (id) ON DELETE CASCADE
);
```

## 🔧 Configuração

### Variáveis de Ambiente

```env
# Server
PORT=8080

# JWT
JWT_SECRET=seu-jwt-secret-super-seguro
```
