#  Agenda Digital 

Aplicação web de página única (SPA) para gerenciamento de contatos, desenvolvida com **HTML5, CSS3 e JavaScript Vanilla**, integrada ao banco de dados **Supabase (PostgreSQL)**.

---

## Tecnologias Utilizadas

| Camada     | Tecnologia              |
|------------|-------------------------|
| Frontend   | HTML5 + CSS3 + JS Vanilla |
| Backend/DB | Supabase (PostgreSQL)   |
| Hospedagem | GitHub Pages / Vercel   |

---

##  Como Configurar

### 1. Criar o projeto no Supabase
1. Acesse [supabase.com](https://supabase.com) e crie uma conta
2. Crie um novo projeto
3. No **SQL Editor**, execute o script abaixo:

```sql
CREATE TABLE CONTATO (
  ID        SERIAL PRIMARY KEY,
  EMAIL     VARCHAR(255),
  NOME      VARCHAR(255),
  TELEFONE  VARCHAR(25),
  OBS       VARCHAR(255),
  DTCONTATO DATE
);
```

### 2. Ativar RLS e criar política pública

```sql
-- Ativar Row Level Security
ALTER TABLE contato ENABLE ROW LEVEL SECURITY;

-- Permitir SELECT e INSERT públicos (via anon key)
CREATE POLICY "acesso_publico" ON contato
  FOR ALL
  USING (true)
  WITH CHECK (true);
```

### 3. Obter as credenciais
- Vá em **Settings → API**
- Copie a **Project URL** e a **anon public key**

### 4. Inserir no index.html
Abra o `index.html` e substitua:

```js
const SUPABASE_URL  = 'https://SEU_PROJECT_ID.supabase.co';
const SUPABASE_ANON = 'SUA_ANON_KEY_AQUI';
```

---

##  Funcionalidades (CRUD Completo)

-  **Criar** novo contato (nome, telefone, e-mail)
-  **Listar** todos os contatos em ordem alfabética
-  **Buscar** contato pelo nome em tempo real
-  **Editar** contato existente (formulário pré-preenchido)
-  **Excluir** contato com confirmação

---

##  Segurança

- RLS (Row Level Security) ativado no Supabase
- Apenas a `anon_key` pública é usada no frontend (nunca a `service_role`)
- Domínio restrito nas configurações do projeto Supabase

---

##  Estrutura do Projeto

```
AgendaContatos/
└── index.html   # Aplicação completa (HTML + CSS + JS)
```

---

*Atividade Prática — Desenvolvimento de Aplicação em Nuvem*
