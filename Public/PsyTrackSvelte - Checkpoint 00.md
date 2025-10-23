🧭 PSYTRACKSVELTE
CHECKPOINT #00 – Setup Inicial

(versão oficial Codex)

🧠 1. Visão Geral

PsyTrackSvelte é uma plataforma web para avaliações psicológicas corporativas, desenvolvida em SvelteKit 2 + TypeScript, com TailwindCSS + Shadcn-svelte no front e Supabase no backend (Auth + DB + Storage + Edge Functions).
O sistema será multi-tenant lógico, isolando dados por psicólogo, e permitirá que psicólogos, empresas e funcionários participem de processos avaliativos seguros e personalizados.

O objetivo principal é unir simplicidade de uso, velocidade e precisão em uma ferramenta completa para diagnósticos psicológicos corporativos.

⚙️ 2. Stack Técnica
Camada	Tecnologia
Framework	SvelteKit 2
Linguagem	TypeScript
Estilização	Tailwind CSS + Shadcn-svelte
Backend	Supabase (PostgreSQL + Auth + Storage + Edge Functions)
Segurança	RLS (Row-Level Security)
Deploy	Vercel (Frontend)
Banco de Dados	Supabase (novo projeto)
Estado	Svelte Stores + Supabase Realtime
Internacionalização	svelte-i18n (pt-BR, es, en)
🧩 3. Estrutura Inicial de Pastas
psytracksvelte/
└─ src/
   ├─ lib/
   │  ├─ supabaseClient.ts
   │  ├─ auth.ts
   │  ├─ db.ts
   │  └─ utils.ts
   ├─ routes/
   │  ├─ +layout.svelte
   │  ├─ +layout.ts
   │  ├─ +page.svelte
   │  ├─ login/
   │  │   ├─ +page.svelte
   │  ├─ admin/
   │  │   ├─ +layout.svelte
   │  │   ├─ +layout.ts
   │  │   ├─ traits/+page.svelte
   │  │   ├─ quizzes/+page.svelte
   │  │   ├─ assessments/+page.svelte
   │  │   └─ companies/+page.svelte
   ├─ components/
   │  ├─ ui/
   │  ├─ forms/
   │  └─ charts/
   ├─ styles/
   │  └─ globals.css
   ├─ hooks/
   │  └─ session.ts
   └─ app.d.ts

🔐 4. Etapas do Setup (execução prática)
1️⃣ – Criar o projeto base
npm create svelte@latest psytracksvelte
cd psytracksvelte
npm install


Selecione as opções:

✔ TypeScript

✔ ESLint + Prettier

✔ Tailwind

✔ Playwright (opcional para testes end-to-end)

2️⃣ – Instalar dependências adicionais
npm install @supabase/supabase-js @supabase/auth-helpers-sveltekit
npm install -D @tailwindcss/forms clsx lucide-svelte
npm install shadcn-svelte

3️⃣ – Configurar Shadcn-svelte
npx shadcn-svelte init


Adicionar os primeiros componentes:

npx shadcn-svelte add button input card label

4️⃣ – Criar o projeto Supabase (novo)

No painel https://supabase.com/dashboard
:

Crie um novo projeto chamado psytracksvelte.

Copie as chaves anon e url para o arquivo .env local:

PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
PUBLIC_SUPABASE_ANON_KEY=eyxxxxxx

5️⃣ – Inicializar o cliente Supabase

src/lib/supabaseClient.ts

import { createClient } from '@supabase/supabase-js'
import { PUBLIC_SUPABASE_URL, PUBLIC_SUPABASE_ANON_KEY } from '$env/static/public'

export const supabase = createClient(PUBLIC_SUPABASE_URL, PUBLIC_SUPABASE_ANON_KEY)

6️⃣ – Configurar autenticação global

src/hooks.server.ts

import { handleSupabaseAuth } from '@supabase/auth-helpers-sveltekit'

export const handle = handleSupabaseAuth()


Esse handle unifica sessão e autenticação em todas as rotas (sem precisar de contextos React).

7️⃣ – Layout base

src/routes/+layout.svelte

<script lang="ts">
  import { supabase } from '$lib/supabaseClient'
  let session = $state(null)
  supabase.auth.onAuthStateChange((_, _session) => session = _session)
</script>

<main class="min-h-screen bg-gray-50 text-gray-900">
  <slot />
</main>

8️⃣ – Configurar Tailwind global

src/app.css

@tailwind base;
@tailwind components;
@tailwind utilities;

9️⃣ – Setup inicial do banco (Supabase SQL)

Após criar o projeto no painel, o próximo passo será o
Checkpoint #01 – Modelagem e RLS, que trará o script SQL completo com as tabelas:

psychologists

companies

employees

traits

quizzes

questions

alternatives

assessments

assessment_quizzes

applications

responses

results

v_results_full

Cada uma com RLS configurado e políticas por role (psychologist, company, employee).

🚀 5. Checkpoints Planejados
Etapa	Descrição	Status
0️⃣	Setup base do projeto (SvelteKit + Supabase)	🔜
1️⃣	Modelagem completa do banco + RLS	🔜
2️⃣	Autenticação e controle de sessão	🔜
3️⃣	CRUD do Psicólogo (Traits, Quizzes, Assessments)	🔜
4️⃣	CRUD da Empresa e Funcionários	🔜
5️⃣	Aplicação e Respostas das Avaliações	🔜
6️⃣	Dashboards e Relatórios	🔜
7️⃣	Internacionalização (pt-BR, es, en)	🔜
8️⃣	Deploy final (Vercel + domínio customizado)	🔜
🎨 6. Diretrizes de UI

Tipografia: Inter / sans-serif

Paleta base: cinzas neutros com toques de azul e violeta (profissional, mas moderno)

Componentes: baseados em Shadcn-svelte, com responsividade mobile-first

Layout padrão: sidebar fixa (admin), header minimalista (login e público)

Tema: claro (modo escuro planejado no futuro)

🧠 7. Diferenciais Técnicos

SSR e SPA no mesmo ambiente (SvelteKit)

Reatividade nativa (sem hooks ou useEffect)

RLS robusto e isolado por psicólogo (Supabase)

Componentes UI reutilizáveis (Shadcn-svelte)

Código expressivo e de fácil manutenção

Infraestrutura escalável e deploy instantâneo na Vercel

🧩 8. Resultados Esperados do Checkpoint #00

Ao final deste checkpoint, o projeto PsyTrackSvelte deverá estar:

Criado e funcional localmente (npm run dev rodando sem erros).

Conectado ao novo Supabase com autenticação integrada.

Com Tailwind e Shadcn-svelte operando normalmente.

Pronto para receber o Checkpoint #01 – Modelagem e RLS.