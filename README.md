

<h1 align="center">🚗 Klyven Auto</h1>

<p align="center">
  <strong>Gestão Completa e Inteligente para o seu Negócio Automotivo.</strong><br/>
  Um SaaS desenvolvido pela <a href="https://www.instagram.com/klyvensolutions/">Klyven Solutions</a>.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=white" />
  <img src="https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?logo=tailwindcss&logoColor=white" />
  <img src="https://img.shields.io/badge/Supabase-Backend-3FCF8E?logo=supabase&logoColor=white" />
  <img src="https://img.shields.io/badge/PWA-Instalável-FF6F00?logo=pwa&logoColor=white" />
</p>

---

## 📋 Sobre o Projeto

O **Klyven Auto** é um sistema SaaS definitivo para donos de **oficinas mecânicas**, **lava-rápidos** e **centros de estética automotiva**. Ele centraliza toda a operação, do controle de pátio em tempo real ao fluxo de caixa automático, proporcionando uma gestão completa e inteligente.

> 🧪 **Teste grátis por 30 dias** — sem cartão de crédito.

---

## 🚀 Funcionalidades Principais

| Módulo | Descrição |
|--------|-----------|
| 📊 **Painel de Controle 360º** | Dashboard com KPIs, radar de saúde financeira, ranking de dias lucrativos e calendário de agendamentos |
| 🅿️ **Controle de Pátio** | Status em tempo real de cada veículo (aguardando, preparação, execução, finalizado, entregue) |
| 📅 **Agendamentos** | Organização completa da agenda com vinculação a clientes e serviços |
| 👥 **Gestão de Clientes (CRM)** | Cadastro completo, histórico de visitas, radar de clientes inativos e envio de mensagem via WhatsApp |
| 🔧 **Catálogo de Serviços** | Cadastro de serviços com categorias, preços, tempo estimado e ranking dos mais lucrativos (Top 10) |
| 🛒 **Vendas** | Vendas rápidas de produtos com controle de estoque automático e ranking de produtos mais lucrativos |
| 💰 **Financeiro** | Fluxo de caixa integrado, controle de despesas, pagamentos pendentes e exportação de relatórios em PDF |
| 📦 **Controle de Estoque** | Gestão precisa de insumos, peças e materiais com alertas de estoque mínimo |
| 📄 **Notas e Orçamentos** | Emissão de notas de serviço, notas de venda, notas combinadas e orçamentos em PDF personalizado |
| ⚙️ **Configurações** | Dados da empresa, logo, gestão de equipe, níveis de acesso e vencimento de mensalidade |

---

## 🏗️ Arquitetura & Stack Tecnológica

```
┌─────────────────────────────────────────────┐
│                  Frontend                    │
│  React 18 · TypeScript 5 · Vite 5 · PWA     │
│  Tailwind CSS 3 · Shadcn/UI · Framer Motion │
├─────────────────────────────────────────────┤
│               State & Data                   │
│  TanStack React Query · React Router DOM     │
├─────────────────────────────────────────────┤
│                 Backend                      │
│  Supabase (Auth · Database · Storage · RLS)  │
│  Edge Functions (Deno)                       │
└─────────────────────────────────────────────┘
```

### Principais Tecnologias

- **React 18** — Biblioteca UI com hooks e componentes funcionais
- **TypeScript 5** — Tipagem estática para código robusto
- **Vite 5** — Build tool ultrarrápido com HMR
- **Tailwind CSS 3** — Framework CSS utility-first
- **Shadcn/UI** — Componentes acessíveis e customizáveis
- **Supabase** — Backend-as-a-Service (Auth, PostgreSQL, RLS, Edge Functions)
- **TanStack React Query** — Gerenciamento de estado assíncrono e cache
- **Framer Motion** — Animações declarativas
- **jsPDF** — Geração de PDFs no client-side
- **PWA** — Aplicação instalável com suporte offline

---

## 🔐 Segurança & Níveis de Acesso

O sistema implementa controle de acesso baseado em roles (RBAC) com **Row Level Security (RLS)** no Supabase:

| Role | Permissões |
|------|------------|
| 🔴 **Admin** | Acesso total a todos os módulos, configurações e gestão de equipe |
| 🟡 **Operador** | Acesso total exceto Configurações e Financeiro |
| 🟢 **Visualizador** | Acesso somente ao Pátio e Agendamentos |

- Roles armazenadas em tabela separada (`user_roles`) para evitar escalação de privilégios
- Função `has_role()` com `SECURITY DEFINER` para verificação segura
- Políticas RLS aplicadas em todas as tabelas

---

## 🏢 Multi-Tenant

Cada empresa (organização) possui seus dados completamente isolados:

- Todas as tabelas possuem `organization_id` com RLS
- Configurações personalizadas por organização (logo, endereço, telefone)
- Gestão independente de equipe, clientes, serviços e estoque

---

## 📱 PWA — Progressive Web App

O Klyven Auto é uma PWA completa, podendo ser instalada em:

- 📱 Smartphones (Android e iOS)
- 💻 Desktops (Chrome, Edge, etc.)
- 📲 Funciona offline com cache inteligente via Workbox

---

## 📂 Estrutura do Projeto

```
src/
├── components/
│   ├── dashboard/          # Componentes do painel (KPIs, radar, ranking, etc.)
│   ├── ui/                 # Componentes Shadcn/UI customizados
│   ├── AppLayout.tsx       # Layout principal com sidebar
│   ├── AppSidebar.tsx      # Sidebar com navegação por role
│   ├── ProtectedRoute.tsx  # Rotas protegidas por autenticação e role
│   └── SessionGate.tsx     # Gate de sessão do Supabase
├── hooks/
│   ├── useAuth.tsx         # Context de autenticação
│   ├── useOrganization.ts  # Hook para organization_id
│   └── useUserRole.ts      # Hook para role do usuário
├── integrations/
│   └── supabase/           # Client e tipos gerados do Supabase
├── pages/
│   ├── Dashboard.tsx       # Painel de controle 360º
│   ├── Patio.tsx           # Controle de pátio (kanban)
│   ├── Agendamentos.tsx    # Gestão de agendamentos
│   ├── Clientes.tsx        # CRM e radar de inativos
│   ├── Servicos.tsx        # Catálogo de serviços
│   ├── Vendas.tsx          # Vendas de produtos
│   ├── Financeiro.tsx      # Fluxo de caixa e relatórios
│   ├── Estoque.tsx         # Controle de estoque
│   ├── Configuracoes.tsx   # Configurações da organização
│   ├── NotaServico.tsx     # Emissão de notas e orçamentos (PDF)
│   ├── LandingPage.tsx     # Página de apresentação
│   └── Auth.tsx            # Login e cadastro
├── App.tsx                 # Rotas e providers
├── main.tsx                # Entry point
└── index.css               # Design tokens e tema global

supabase/
├── config.toml             # Configuração do Supabase
├── migrations/             # Migrações do banco de dados
└── functions/
    ├── create-user/        # Edge Function: criar usuário
    └── delete-user/        # Edge Function: deletar usuário
```

---

## 💰 Planos de Assinatura

| Plano | Valor | Custo/dia | Economia |
|-------|-------|-----------|----------|
| Mensal | R$ 97/mês | R$ 3,23 | — |
| Semestral | R$ 540/6 meses | R$ 3,00 | R$ 42 |
| Anual ⭐ | R$ 960/ano | R$ 2,66 | R$ 204 |

> 💡 *Organize seu negócio automotivo por menos de R$ 3 por dia.*

---

## 🛠️ Como Rodar Localmente

### Pré-requisitos

- [Node.js 18+](https://nodejs.org/) ou [Bun](https://bun.sh/)
- Conta no [Supabase](https://supabase.com/) 

### Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/klyven-auto.git
cd klyven-auto

# Instale as dependências
npm install
# ou
bun install

# Configure as variáveis de ambiente
cp .env.example .env
# Preencha VITE_SUPABASE_URL e VITE_SUPABASE_ANON_KEY

# Rode o projeto
npm run dev
# ou
bun dev
```

O app estará disponível em `http://localhost:8080`.

### Variáveis de Ambiente

| Variável | Descrição |
|----------|-----------|
| `VITE_SUPABASE_URL` | URL do projeto Supabase |
| `VITE_SUPABASE_ANON_KEY` | Chave pública (anon) do Supabase |

---

## 📜 Scripts Disponíveis

| Comando | Descrição |
|---------|-----------|
| `npm run dev` | Inicia o servidor de desenvolvimento |
| `npm run build` | Build de produção |
| `npm run preview` | Preview do build de produção |
| `npm run lint` | Lint do código com ESLint |
| `npm run test` | Executa testes com Vitest |

---

## ⚖️ Documentação Legal

- [📄 Política de Privacidade](https://klyven-auto-flow.lovable.app/politica-de-privacidade)
- [📄 Termos de Uso](https://klyven-auto-flow.lovable.app/termos-de-uso)

Redigidos com base nas diretrizes da **LGPD** (Lei Geral de Proteção de Dados).

---

## 📞 Contato & Redes Sociais

| Canal | Link |
|-------|------|
| 📸 Instagram | [@klyvenauto](https://www.instagram.com/klyvenauto/) |
| 📧 Suporte | suporte@klyvenauto.com.br |
| 📧 Financeiro | financeiro@klyvenauto.com.br |
| 📧 Contato | contato@klyvenauto.com.br |

---

## 📄 Licença

Este projeto é propriedade exclusiva da **Klyven Solutions**. Todos os direitos reservados.

O uso, cópia, modificação ou distribuição deste software sem autorização expressa é estritamente proibido.

---

<p align="center">
  <strong>Klyven Auto © 2026 — Todos os direitos reservados.</strong><br/>
  
