# 💰 Controle Financeiro

App de controle financeiro mensal com sincronização em nuvem via Supabase. Funciona em qualquer dispositivo — celular, tablet ou computador.

---

## 🔐 Acesso

| Usuário | Senha |
|---------|-------|
| higoro  | Porto123@ |

---

## 🚀 Como configurar do zero

### 1. Supabase — banco de dados

1. Acesse [supabase.com](https://supabase.com) e crie uma conta (gratuito)
2. Clique em **New project** e dê um nome (ex: `controle-financeiro`)
3. Defina uma senha para o banco e clique em **Create new project**
4. No menu lateral, clique em **SQL Editor**
5. Cole o SQL abaixo e clique em **Run**:

```sql
create table lancamentos (
  id uuid default gen_random_uuid() primary key,
  ano integer not null,
  mes integer not null,
  desc text not null,
  valor numeric not null,
  cat text not null,
  tipo text not null,
  dia integer not null,
  created_at timestamp with time zone default now()
);

-- Permitir acesso público (sem autenticação do Supabase)
alter table lancamentos enable row level security;

create policy "Acesso público" on lancamentos
  for all using (true) with check (true);
```

6. Vá em **Project Settings → API**
7. Copie:
   - **Project URL** → ex: `https://xyzxyz.supabase.co`
   - **anon public key** → chave longa começando com `eyJ...`

8. Abra o arquivo `controle-financeiro.html` e substitua nas linhas 165-166:
```js
const SUPABASE_URL = 'COLE_SUA_PROJECT_URL_AQUI';
const SUPABASE_ANON_KEY = 'COLE_SUA_ANON_KEY_AQUI';
```

---

### 2. GitHub — repositório do código

1. Acesse [github.com](https://github.com) e crie um novo repositório
2. Nome sugerido: `controle-financeiro`
3. Pode deixar **Público** (necessário para o Vercel gratuito) ou Privado
4. Após criar, faça upload do arquivo `controle-financeiro.html` (arrastar e soltar funciona)
5. Também faça upload deste `README.md`
6. Commit com a mensagem: `primeiro commit`

---

### 3. Vercel — hospedagem

1. Acesse [vercel.com](https://vercel.com) e entre com sua conta GitHub
2. Clique em **Add New Project**
3. Escolha o repositório `controle-financeiro`
4. Clique em **Deploy** (sem alterar nada)
5. Após o deploy, você receberá um link tipo `controle-financeiro.vercel.app`

✅ Pronto! Abra esse link em qualquer dispositivo e os dados ficam sincronizados via Supabase.

---

## 📱 Funcionalidades

- **Resumo** — métricas do mês: entradas, saídas, saldo e investido + gráfico por categoria
- **Lançamentos** — adicionar e remover gastos e receitas com categoria e dia
- **Comparativo** — comparar dois meses lado a lado com variação percentual
- **Insights** — análise automática detectando padrões, gastos altos, meses sem investimento, tendências

## 🔄 Sincronização

- Todos os dados ficam salvos no Supabase
- Funciona offline (usa cache local) e sincroniza quando voltar a conexão
- O ponto verde (●) na barra superior indica status da conexão

## 🛠️ Atualizar o app

Quando quiser mudar algo no app:
1. Edite o arquivo `controle-financeiro.html` no GitHub
2. Commit a mudança
3. O Vercel faz o deploy automático em ~30 segundos

---

## 📊 Dados de março/2026 (pré-carregados)

| Descrição | Valor | Tipo |
|-----------|-------|------|
| IR - Higor | R$ 500,00 | Entrada |
| Salário IW | R$ 2.000,00 | Entrada |
| Vale IW | R$ 2.000,00 | Entrada |
| Água | R$ 163,73 | Saída |
| Internet | R$ 99,90 | Saída |
| Celular | R$ 99,60 | Saída |
| Energia | R$ 191,30 | Saída |
| Academia | R$ 110,00 | Saída |
| Aluguel | R$ 1.400,00 | Saída |
| Financiamento Carro (14/48) | R$ 961,57 | Saída |
| Financiamento Moto (24/48) | R$ 967,00 | Saída |
| IPVA HB20 | R$ 382,11 | Saída |
| IPVA FZ25 | R$ 94,74 | Saída |
| Licenciamento FZ25 | R$ 174,08 | Saída |
| Sem Parar | R$ 59,82 | Saída |
| Fatura Nubank | R$ 9.480,00 | Saída |
| Fatura Inter | R$ 7.121,48 | Saída |
