# Arraiá Digital

Versão real do app de Festa Junina, reconstruída a partir do protótipo antigo.

## Stack

- React + Vite
- Supabase Auth
- Supabase Postgres com Row Level Security
- Deploy preparado para Vercel ou Netlify

## Estrutura

- `legacy-prototype/` — protótipo visual original preservado
- `src/` — nova aplicação real
- `supabase/migrations/` — schema, políticas e funções do banco

## Como rodar localmente

1. Instale as dependências:

   ```bash
   npm install
   ```

2. Copie `.env.example` para `.env` e preencha:

   ```bash
   VITE_SUPABASE_URL=
   VITE_SUPABASE_ANON_KEY=
   ```

3. Rode a migration `supabase/migrations/202605150001_init.sql` no SQL Editor do Supabase.

4. Inicie o frontend:

   ```bash
   npm run dev
   ```

## Configuração do Auth no Supabase

No painel do Supabase, em **Authentication → URL Configuration**:

- `Site URL`: use a URL final do frontend hospedado
- `Redirect URLs`: adicione também `http://localhost:5173/**`

Se você mantiver confirmação de e-mail ligada, o cadastro cria a conta mas o login só acontece depois que o usuário confirma o e-mail.

## Primeiro administrador

Depois de criar sua conta no app, rode no SQL Editor do Supabase:

```sql
update public.profiles
set role = 'admin'
where nickname = 'SEU_APELIDO';
```

## Deploy

### Vercel

1. Suba o projeto para um repositório.
2. Importe o projeto na Vercel.
3. Cadastre as variáveis `VITE_SUPABASE_URL` e `VITE_SUPABASE_ANON_KEY`.
4. Faça o deploy.

### Netlify

1. Suba o projeto para um repositório.
2. Importe o projeto na Netlify.
3. Cadastre as variáveis `VITE_SUPABASE_URL` e `VITE_SUPABASE_ANON_KEY`.
4. Faça o deploy.

## Observações

- O app usa funções RPC para compras, jogos, correio e prisão, para manter a lógica sensível no banco.
- As páginas principais já estão prontas para operar com dados reais do Supabase.
- O protótipo antigo foi preservado apenas como referência visual.
