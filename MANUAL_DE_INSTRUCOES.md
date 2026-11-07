# MANUAL DE INSTRUÇÕES — PLATAFORMA OFICIAL JK (ANGOLA)

**JK — Tecnologia, confiança e inovação.**  
**WhatsApp Oficial:** +244 922 201 011  
**Link Oficial WhatsApp:** https://wa.me/244922201011  
**País de Operação:** Angola  
**Moeda Oficial:** Kwanza angolano (Kz)  
**Hospedagem Recomendada:** Cloudflare Pages  
**Backend:** Supabase (PostgreSQL + Auth + Storage)

---

## ÍNDICE

1. [Visão Geral da Plataforma](#1-visão-geral-da-plataforma)
2. [Estrutura de Ficheiros do Projeto](#2-estrutura-de-ficheiros-do-projeto)
3. [Requisitos e Instalação Local](#3-requisitos-e-instalação-local)
4. [Configuração de Variáveis de Ambiente (.env)](#4-configuração-de-variáveis-de-ambiente)
5. [Configuração do Banco de Dados Supabase](#5-configuração-do-banco-de-dados-supabase)
6. [Publicação no Cloudflare Pages (Passo a Passo)](#6-publicação-no-cloudflare-pages)
7. [Funcionamento do WhatsApp Commerce](#7-funcionamento-do-whatsapp-commerce)
8. [Programa de Afiliados e Atribuição de 30 Dias](#8-programa-de-afiliados)
9. [Painel Administrativo Completo](#9-painel-administrativo-completo)
10. [Módulo GladIA — Assistente Inteligente](#10-módulo-gladia)
11. [Exportação e Personalização do Projeto em ZIP](#11-exportação-do-projeto-em-zip)
12. [Perguntas Frequentes e Suporte](#12-perguntas-frequentes-e-suporte)

---

## 1. VISÃO GERAL DA PLATAFORMA

A **JK** é uma plataforma comercial de comércio eletrónico moderna e completa, desenvolvida exclusivamente para o mercado de tecnologia e eletrónicos em Angola.

### Principais Pilares:
- **Exclusividade da Marca:** Somente a marca **JK**, com logotipo tipográfico azul cobalto, fundo branco puro e textos em preto de alto contraste.
- **WhatsApp Commerce Nativo:** Encomendas, compras diretas, atendimento e suporte integrados ao número oficial **+244 922 201 011**.
- **Angola First:** Moeda oficial em Kwanza (Kz), cálculo de frete para Luanda e todas as 18 províncias, pagamentos manuais via Multicaixa Express e Transferência Bancária.
- **Ecossistema de Afiliados:** Links individuais com código de referência (`?ref=CODIGO_AFILIADO`), janela de atribuição de 30 dias gravada com consentimento, cálculo exato de comissões por produto e painel com levantamentos bancários (IBAN).
- **CRM e Gestão Comercial:** Gestão de oportunidades de vendas, tarefas e histórico de conversas.
- **GladIA:** Assistente inteligente para recomendar eletrónicos pelo orçamento em Kwanza, comparar fichas técnicas e orientar clientes.

---

## 2. ESTRUTURA DE FICHEIROS DO PROJETO

```
jk-platform/
├── public/
│   ├── _redirects                  # Regra SPA Cloudflare Pages (evita erro 404 em refresh)
│   ├── robots.txt                  # Regras de indexação SEO
│   └── sitemap.xml                 # Mapa do site para motores de busca
├── src/
│   ├── config/
│   │   └── constants.ts            # Identidade oficial JK, WhatsApp centralizado, províncias
│   ├── types/
│   │   └── index.ts                # Tipagens TypeScript completas de todo o sistema
│   ├── services/
│   │   ├── initialProducts.ts      # Catálogo com ~60 produtos de tecnologia em Kwanzas
│   │   ├── storage.ts              # Motor reativo de dados local + sincronização Supabase
│   │   └── zipExporter.ts          # Gerador em tempo real do arquivo ZIP do projeto
│   ├── modules/
│   │   ├── storefront/             # Header, Carrossel Hero, Categorias, Destaques, Footer
│   │   ├── products/               # Página de Detalhe com variantes e Catálogo com Filtros
│   │   ├── cart/                   # Gaveta e gestão do carrinho com cupões
│   │   ├── checkout/               # Checkout angolano com WhatsApp order formatter
│   │   ├── customer/               # Portal do Cliente (pedidos, dados, histórico)
│   │   ├── affiliates/             # Portal de Afiliados (links, cliques, comissões, levantamentos)
│   │   ├── crm/                    # Gestão de contactos, leads e pipeline
│   │   ├── gladia/                 # Modal interativo da assistente inteligente GladIA
│   │   ├── admin/                  # Painel de controlo completo com 12 módulos
│   │   └── zip/                    # Modal de download do código em ZIP personalizado
│   ├── App.tsx                     # Roteamento e orquestração da aplicação
│   ├── main.tsx                    # Ponto de entrada React 19
│   └── index.css                   # Tailwind CSS v4
├── supabase/
│   ├── migrations/
│   │   └── 01_initial_schema.sql   # 34+ tabelas PostgreSQL, RLS, índices e chaves
│   └── seed.sql                    # Configurações iniciais e cupões
├── .env.example                    # Modelo de variáveis de ambiente
├── package.json                    # Dependências e scripts
├── tsconfig.json                   # Configuração de TypeScript
├── vite.config.ts                  # Configuração Vite & Tailwind
├── MANUAL_DE_INSTRUCOES.md         # Este manual completo
└── README.md                       # Apresentação do repositório
```

---

## 3. REQUISITOS E INSTALAÇÃO LOCAL

### Pré-requisitos:
- **Node.js:** Versão 18.0.0 ou superior (recomendado Node 20 LTS).
- **NPM:** Versão 9 ou superior.

### Passo a passo para rodar localmente:
1. Extraia o ficheiro ZIP fornecido para uma pasta no seu computador.
2. Abra o terminal nessa pasta:
   ```bash
   cd jk-platform
   ```
3. Instale as dependências:
   ```bash
   npm install
   ```
4. Crie o ficheiro de variáveis locais:
   ```bash
   cp .env.example .env
   ```
5. Inicie o servidor de desenvolvimento:
   ```bash
   npm run dev
   ```
6. Aceda no seu navegador a: `http://localhost:3000`

---

## 4. CONFIGURAÇÃO DE VARIÁVEIS DE AMBIENTE (.env)

No ficheiro `.env`, configure:

```env
# GladIA Assistente Inteligente (Gemini API)
GEMINI_API_KEY="a-sua-chave-gemini"

# Configurações Oficiais JK
VITE_JK_WHATSAPP_NUMBER="244922201011"
VITE_JK_WHATSAPP_LINK="https://wa.me/244922201011"

# Supabase (Banco de Dados em Produção)
VITE_SUPABASE_URL="https://seu-projeto.supabase.co"
VITE_SUPABASE_ANON_KEY="sua-chave-anon-publica"
```

---

## 5. CONFIGURAÇÃO DO BANCO DE DADOS SUPABASE

A plataforma JK foi desenhada para funcionar imediatamente em modo Local/Demo no navegador e conectar-se perfeitamente ao Supabase em produção.

### Passo a passo no Supabase:
1. Aceda a [https://supabase.com](https://supabase.com) e crie uma conta gratuita.
2. Crie um novo projeto, selecionando a região mais próxima de África (ex: Frankfurt ou Londres).
3. No menu lateral do Supabase, aceda a **SQL Editor**.
4. Abra o ficheiro `supabase/migrations/01_initial_schema.sql` deste projeto, copie todo o seu conteúdo e cole no SQL Editor do Supabase.
5. Clique em **RUN** para criar todas as 34 tabelas relacionais, índices de alta performance e políticas de segurança RLS (Row Level Security).
6. Execute também o ficheiro `supabase/seed.sql` para carregar as configurações padrão e cupões.
7. Em **Project Settings > API**, copie a **Project URL** e a **anon public key** e cole no seu `.env` ou nas variáveis do Cloudflare Pages.

---

## 6. PUBLICAÇÃO NO CLOUDFLARE PAGES (PASSO A PASSO)

O Cloudflare Pages oferece carregamento ultrarrápido em Angola através dos seus servidores de borda globais.

1. Faça o envio (push) deste código para um repositório no **GitHub** ou **GitLab**.
2. Aceda ao painel do **Cloudflare** > **Workers & Pages** > **Create application** > **Pages** > **Connect to Git**.
3. Selecione o repositório da plataforma JK.
4. Defina as configurações de Build:
   - **Framework preset:** `Vite`
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
5. Em **Environment variables**, adicione:
   - `VITE_JK_WHATSAPP_NUMBER` = `244922201011`
   - `VITE_JK_WHATSAPP_LINK` = `https://wa.me/244922201011`
   - `VITE_SUPABASE_URL` = (a sua URL Supabase)
   - `VITE_SUPABASE_ANON_KEY` = (a sua chave anónima Supabase)
6. Clique em **Save and Deploy**.
7. O ficheiro `public/_redirects` já incluído garante que qualquer recarregamento de página em rotas internas funcione perfeitamente sem erros 404!

---

## 7. FUNCIONAMENTO DO WHATSAPP COMMERCE

A JK utiliza mensagens estruturadas com codificação URL para criar uma experiência de compra sem fricção:

### Mensagem de Compra Direta de Produto:
```
Olá JK! Tenho interesse em comprar este produto:

Produto: [NOME]
Referência: [SKU]
Preço: [PREÇO]
Variante: [VARIANTE]
Quantidade: [QUANTIDADE]

Gostaria de confirmar a disponibilidade e as condições de compra.
```

### Mensagem de Finalização de Encomenda no Checkout:
```
Olá JK! Quero finalizar a minha encomenda.

CLIENTE: [NOME]
CONTACTO: [TELEFONE]

PRODUTOS:
[LISTA DE PRODUTOS COM QUANTIDADES E VALORES]

SUBTOTAL: [VALOR EM KZ]
DESCONTO: [VALOR EM KZ]
ENTREGA: [VALOR EM KZ]
TOTAL: [VALOR EM KZ]

LOCAL DE ENTREGA: [PROVÍNCIA, MUNICÍPIO, BAIRRO, ENDEREÇO]
PAGAMENTO: [MÉTODO DE PAGAMENTO]

Referência da encomenda: [JK-2026-XXXX]

Aguardo confirmação. Obrigado!
```

---

## 8. PROGRAMA DE AFILIADOS

1. O interessado regista-se na página **Afiliados**.
2. Recebe o seu código único (ex: `AF-MATEUS`).
3. O link de partilha é gerado no formato:
   `https://loja.jk.co.ao/?ref=AF-MATEUS` ou `https://loja.jk.co.ao/produto/slug?ref=AF-MATEUS`
4. Quando um cliente visita através do link:
   - É gravada uma atribuição de **30 dias**.
   - Cada clique incrementa o contador no painel do afiliado.
5. Quando o cliente compra, a comissão (5% a 15% conforme o produto) entra como **Pendente**.
6. O administrador confirma a receção do pagamento no Painel Admin e aprova a comissão.
7. O afiliado solicita levantamento indicando o seu **IBAN** bancário angolano (BAI, BFA, BIC, etc.).

---

## 9. PAINEL ADMINISTRATIVO COMPLETO

O Painel de Controlo da JK inclui:
- **Dashboard:** Vendas do dia/semana/mês, receitas em Kwanzas, encomendas pendentes e alertas de stock.
- **Produtos:** Criação, edição, variantes, comissões de afiliado e gestão de fotos.
- **Categorias:** Ativação e ordenação das 23 categorias de eletrónica.
- **Encomendas:** Alteração de status (Nova -> Confirmada -> Em transporte -> Concluída) com atalho de WhatsApp direto para o cliente.
- **Inventário:** Ajustes de entrada, saída e histórico.
- **Afiliados & Levantamentos:** Aprovação de comissões e registo de transferências com número de comprovativo bancário.
- **CRM:** Gestão de oportunidades de vendas, follow-ups e notas.
- **Fornecedores & Finanças:** Registo de despesas, receitas e cálculo de lucro líquido real.
- **Configurações:** Atualização de telefone WhatsApp, moradas, fretes e parâmetros da loja.

---

## 10. MÓDULO GLADIA — ASSISTENTE INTELIGENTE

A **GladIA** auxilia os clientes a:
- Encontrar smartphones ou computadores de acordo com o limite de gastos em Kwanzas.
- Comparar modelos (ex: iPhone 15 Pro Max vs Samsung Galaxy S24 Ultra).
- Tirar dúvidas sobre garantia em Angola e prazos de entrega nas províncias.
- Transferir com um clique a conversa para o WhatsApp oficial com a dúvida já formatada.

---

## 11. EXPORTAÇÃO DO PROJETO EM ZIP

O utilizador pode a qualquer momento clicar no botão **"Baixar Projeto ZIP"** situado no menu ou no painel de controlo. A aplicação irá gerar na hora um ficheiro compactado contendo todo o código-fonte, componentes, migrações SQL e este manual, pronto para backup ou envio.

---

## 12. PERGUNTAS FREQUENTES E SUPORTE

**P: A loja funciona sem internet ou sem Supabase configurado?**  
R: Sim! A aplicação possui um banco de dados reativo local embutido que salva todas as encomendas, produtos e afiliados mesmo sem conexão ao Supabase externo. Quando você configurar o Supabase, os dados podem ser migrados.

**P: Como alterar o número do WhatsApp da loja?**  
R: Basta aceder a **Painel Admin > Configurações da Loja** e atualizar o número, ou editar a constante em `src/config/constants.ts`.

---
*Documento emitido para a plataforma oficial JK em Angola.*
