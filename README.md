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
| **Disciplina**     | APLICAÇÃO DE BANCO DE DADOS             |
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
| **Update** | Edição de contato existente — dados carregados no formulário ao clicar em editar |
| **Delete** | Exclusão do contato com confirmação antes de apagar |
| **Search** | Busca por nome, filtrando a listagem dinamicamente |
 
---
 
## Banco de Dados: Supabase (PostgreSQL)
 
### Criação da Tabela (via SQL Editor)
 
Script SQL utilizado para criar a tabela e ativar o RLS:
 
```sql
CREATE TABLE contato (
  id        SERIAL PRIMARY KEY,
  email     VARCHAR(255),
  nome      VARCHAR(255) NOT NULL,
  telefone  VARCHAR(25),
  obs       VARCHAR(255),
  dtcontato DATE
);
 
ALTER TABLE contato ENABLE ROW LEVEL SECURITY;
```
 
### Políticas de Segurança (via interface gráfica — Authentication → Policies)
 
Após ativar o RLS, foram criadas 4 políticas manualmente pela interface do Supabase, todas restritas ao role `anon`:
 
| Policy | Comando | Regra | Efeito |
|--------|---------|-------|--------|
| Permitir SELECT publico | SELECT | `using (true)` | Permite leitura dos contatos |
| Permitir INSERT publico | INSERT | `with check (true)` | Permite cadastro de novos contatos |
| Permitir UPDATE publico | UPDATE | `using (true)` / `with check (true)` | Permite edição dos contatos |
| Permitir DELETE publico | DELETE | `using (true)` | Permite exclusão dos contatos |
 
### Como funciona o RLS aqui
 
| Elemento | O que faz |
|----------|-----------|
| `ENABLE ROW LEVEL SECURITY` | Ativa o RLS na tabela — sem isso, as políticas seriam ignoradas |
| 4 políticas separadas | Uma para cada operação (SELECT, INSERT, UPDATE, DELETE), aplicadas explicitamente ao role `anon` |
| `using (true)` | Libera leitura/atualização/exclusão para o role `anon` |
| `with check (true)` | Libera escrita/atualização para o role `anon` |
 
>  A chave utilizada no frontend é a **publishable key** (equivalente atual da antiga chave `anon`), com permissões controladas pelo RLS. A **secret key** (equivalente à antiga `service_role`, administrativa) **não está exposta** em nenhum arquivo do projeto.
 
---
 
##  Boas Práticas de Segurança
 
- Apenas a **publishable key** do Supabase é utilizada no frontend.
- O RLS está ativo na tabela `contato`, com 4 políticas explícitas (uma por operação), restritas ao role `anon`.
- A **secret key** (administrativa) **nunca** foi exposta no código-fonte ou no repositório.
- Nenhum arquivo `.env` com credenciais sensíveis foi versionado.
---
 
##  Como Executar Localmente
 
1. Clone o repositório:
```bash
   git clone https://github.com/Julia076/agenda-digital.git
   cd agenda-digital
```
 
2. Abra o arquivo `index.html` diretamente no navegador **ou** utilize a extensão **Live Server** no VS Code.
3. Confirme que as credenciais do Supabase em `index.html` estão preenchidas:
```js
    const URL  = 'https://wsdazbfihhrmkjprqnyf.supabase.co';
    const KEY  = 'sb_publishable_xrJw_waDaUOfOLIFj49JIA__lUUI6yI';
```
 
>   Nenhuma dependência precisa ser instalada. A integração com o Supabase é feita diretamente via API REST usando fetch nativo do JavaScript.
 
---

##  Deploy

A aplicação está publicada e acessível em:

**🔗 [https://julia076.github.io/agenda-digital/](https://julia076.github.io/agenda-digital/)**

---

## Interface da Aplicação

> *![Tela da aplicação](screenshot/screenshot.png)
![Tela da aplicação 2](screenshot/screenshot01.png)*

---
