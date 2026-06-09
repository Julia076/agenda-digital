#  Agenda Digital 

Aplicação web de página única (SPA) para gerenciamento de contatos, desenvolvida com **HTML5, CSS3 e JavaScript Vanilla**, integrada ao banco de dados **Supabase (PostgreSQL)**.

---
## Alunas

| Nome    | 
|------------|
| Júlia Monteiro Rodrigues  | 
| Marielli Alves Macedo | 

---

## Tecnologias Utilizadas

| Camada     | Tecnologia                |
|------------|---------------------------|
| Frontend   | HTML5 + CSS3 + JS Vanilla |
| Backend/DB | Supabase (PostgreSQL)     |
| Hospedagem | GitHub Pages              |

---

## Configuração do Banco de Dados 

### 1. Criar a tabela

```sql
CREATE TABLE contato (
  id        SERIAL PRIMARY KEY,
  email     VARCHAR(255),
  nome      VARCHAR(255),
  telefone  VARCHAR(25),
  obs       VARCHAR(255),
  dtcontato DATE
);
```

### 2. Ativar RLS e criar política de acesso

```sql
ALTER TABLE contato ENABLE ROW LEVEL SECURITY;

CREATE POLICY "acesso_publico" ON contato
  FOR ALL USING (true) WITH CHECK (true);
```

### 3. Verificar tabelas criadas

```sql
SELECT table_name FROM information_schema.tables
WHERE table_schema = 'public';
```

---

## Funcionalidades (CRUD Completo)

-  **Criar** novo contato (nome, telefone, e-mail)
-  **Listar** todos os contatos em ordem alfabética
-  **Buscar** contato pelo nome
-  **Editar** contato existente (formulário pré-preenchido)
-  **Excluir** contato com confirmação

---

## Segurança

- RLS (Row Level Security) ativado na tabela `contato`
- Apenas a `anon_key` pública é usada no frontend (nunca a `service_role`)
- Política de acesso controlado via Supabase Policy

---

##  Estrutura do Projeto

```
agenda-digital/
├── index.html   # Aplicação completa (HTML + CSS + JS)
```

---

*Atividade Prática — Desenvolvimento de Aplicação em Nuvem*
