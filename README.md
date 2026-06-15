# Agenda Digital 

> Aplicação web de página única (SPA) para gerenciamento de contatos, integrada ao banco de dados relacional **Supabase (PostgreSQL)** na nuvem.

---

##  Alunas

| Nome                     |                              
|--------------------------|
| Júlia Monteiro Rodrigues | 
| Marielli Alves Macedo | 

---

## Informações da Atividade

| Campo              | Descrição                                    |
|--------------------|----------------------------------------------|
| **Disciplina**     | Desenvolvimento de Sistemas Web              |
| **Atividade**      | Prática — Integração Frontend + BaaS         |
| **Banco de dados** | Supabase (PostgreSQL)                        |
| **Tecnologias**    | HTML5, CSS3, JavaScript (Vanilla JS)         |

---

##  Objetivo

Construir um aplicativo web de **gerenciamento de contatos (Agenda Digital)**, integrando uma interface estática de cliente a um banco de dados hospedado na nuvem, exercitando o papel de desenvolvedor Full Stack iniciante com uso de BaaS (Backend as a Service).

---

##  Estrutura do Projeto

```
/
├── index.html       # Página principal da aplicação (SPA)
└── README.md        # Este arquivo
```

---

## Funcionalidades (CRUD)

| Operação   | Descrição |
|------------|-----------|
| **Create** | Cadastro de novo contato via formulário (Nome, Telefone, E-mail) |
| **Read**   | Listagem de todos os contatos salvos na nuvem |
| **Update** | Edição de contato existente — dados carregados no formulário ao clicar em ✏️ |
| **Delete** | Exclusão do contato com confirmação antes de apagar 🗑️ |
| **Search** | Busca por nome, filtrando a listagem dinamicamente |

---

## Banco de Dados: Supabase (PostgreSQL)

### Criação da Tabela e Configuração de Segurança

Script SQL completo utilizado no projeto:

```sql
CREATE TABLE contato (
  id        SERIAL PRIMARY KEY,
  email     VARCHAR(255),
  nome      VARCHAR(255),
  telefone  VARCHAR(25),
  obs       VARCHAR(255),
  dtcontato DATE
);

ALTER TABLE contato ENABLE ROW LEVEL SECURITY;

CREATE POLICY "acesso_publico" ON contato
  FOR ALL USING (true) WITH CHECK (true);
```

### Como funciona o RLS aqui

| Elemento | O que faz |
|----------|-----------|
| `ENABLE ROW LEVEL SECURITY` | Ativa o RLS na tabela — sem isso, as políticas são ignoradas |
| `FOR ALL` | Aplica a política para SELECT, INSERT, UPDATE e DELETE |
| `USING (true)` | Libera leitura e exclusão para qualquer usuário |
| `WITH CHECK (true)` | Libera escrita e atualização para qualquer usuário |

>  A chave utilizada no frontend é exclusivamente a `anon` (pública), com permissões controladas pelo RLS. A chave `service_role` (administrativa) **não está exposta** em nenhum arquivo do projeto.

---

##  Boas Práticas de Segurança

- Apenas a chave `anon` (pública) do Supabase é utilizada no frontend.
- O RLS está ativo na tabela `contato` com política de acesso controlado.
- A chave `service_role` (administrativa) **nunca** foi exposta no código-fonte ou no repositório.
- Nenhum arquivo `.env` com credenciais sensíveis foi versionado.

---

##  Como Executar Localmente

1. Clone o repositório:
   ```bash
   git clone https://github.com/Julia076/agenda-digital.git
   cd agenda-digital
   ```

2. Abra o arquivo `index.html` diretamente no navegador **ou** utilize a extensão **Live Server** no VS Code.

3. Confirme que as credenciais do Supabase em `app.js` estão preenchidas:
   ```js
    const URL  = 'https://wsdazbfihhrmkjprqnyf.supabase.co';
    const KEY  = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6IndzZGF6YmZpaGhybWtqcHJxbnlmIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODA5NzgzMTUsImV4cCI6MjA5NjU1NDMxNX0.o6ctzuYqg2zzFYYtu03Rp2dJL3V11POfQmbV9uITz_M';
   ```

>  Nenhuma dependência precisa ser instalada. A biblioteca do Supabase é carregada via CDN diretamente no HTML.

---

##  Deploy

A aplicação está publicada e acessível em:

**🔗 [https://julia076.github.io/agenda-digital/](https://julia076.github.io/agenda-digital/)**

---

## 📸 Interface da Aplicação

> *![Tela da aplicação](screenshot/screenshot.png)
![Tela da aplicação 2](screenshot/screenshot01.png)*

---
