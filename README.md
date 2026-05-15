# Arraiá Digital

Aplicação de Festa Junina concentrada em um único `index.html`, com dados reais no Supabase.

## Stack

- `index.html` como interface principal
- Tailwind via CDN
- Supabase Auth
- Supabase Postgres com Row Level Security
- Vite apenas para rodar localmente e injetar variáveis de ambiente no HTML

## Estrutura

- `index.html` — interface única do app
- `supabase/migrations/` — schema, políticas e funções do banco
- `src/` — implementação React anterior, preservada por enquanto como referência de código

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

Se a confirmação de e-mail estiver ligada, o cadastro cria a conta e o login só funciona depois da confirmação.

## Primeiro administrador

Depois de criar sua conta no app, rode no SQL Editor do Supabase:

```sql
update public.profiles
set role = 'admin'
where nickname = 'SEU_APELIDO';
```

## O que já usa banco de dados

- cadastro e login
- perfil e saldo de fichas
- cardápio e compras
- correio do amor
- jogos
- programação de shows
- prisão, fiança e quiz
- histórico recente de movimentações de fichas

## Observações

- Compras, jogos, correio e prisão continuam usando funções RPC do banco para manter a lógica sensível protegida.
- Os HTMLs antigos do protótipo foram removidos para evitar duas interfaces competindo entre si.
- O login agora usa e-mail, porque o Supabase Auth não faz login seguro por apelido direto no navegador sem uma camada extra no backend.
