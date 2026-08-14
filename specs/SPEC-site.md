# SPEC — Site Lho Tech Solutions (site estático, GitHub Pages)

Documento de especificação para construir o site em VS Code (com ou sem assistente de IA).
Cole este arquivo inteiro no chat do assistente antes de pedir o código.

---

## 1. Objetivo

Site institucional/vitrine da desenvolvedora **Lho Tech Solutions** (apps Android no Google Play), com dois propósitos:

1. Portfólio profissional dos apps.
2. Cumprir as exigências do Google Play: **uma URL pública de política de privacidade por app**, e-mail de suporte visível.

Página do Play: `https://play.google.com/store/apps/dev?id=9127115335766256766&hl=pt_BR`
E-mail de contato: `lhotecsolutions@gmail.com`
Idioma: **bilíngue** — português como principal, inglês como bloco secundário em cada seção.

## 2. Stack e restrições

- HTML + CSS puros. **Sem framework, sem build, sem npm, sem JavaScript** exceto o mínimo (nenhum é obrigatório).
- Um único arquivo `styles.css` compartilhado por todas as páginas.
- Caminhos **relativos** (o site roda em subpasta no GitHub Pages: `usuario.github.io/repo/`).
- Cada página deve funcionar abrindo o arquivo direto no navegador (`file://`).
- Sem cookies, sem analytics, sem fontes bloqueantes além do Google Fonts.
- Responsivo mobile-first; nenhum texto abaixo de 14px; alvos de toque ≥ 44px.

## 3. Estrutura de arquivos

```
/
├── index.html                      Home: hero + grade de apps + suporte
├── privacidade/
│   ├── index.html                  Índice: lista de links para cada app
│   ├── app-1.html                  Política do App 1
│   ├── app-2.html
│   ├── app-3.html
│   └── app-4.html
├── styles.css
├── assets/
│   ├── icons/app-1.png             ícone 512x512 do Play
│   ├── icons/app-2.png
│   ├── og-image.png                1200x630 para compartilhamento
│   └── hero.jpg                    print ou capa (opcional)
└── README.md
```

Renomear `app-1` etc. para o slug real do app (ex.: `privacidade/cronometro-pro.html`). Uma página por app, sem exceção.

## 4. Design system (tokens obrigatórios)

Estilo: **wireframe técnico** — azul-aço sobre fundo claro, títulos condensados, molduras de 1px com marcas de registro "+" nos cantos. Nada de cantos arredondados, nada de gradientes, nada de sombra forte, nada de emoji.

```css
:root {
  --color-bg: #f2f2f3;
  --color-surface: #ffffff;
  --color-text: #1d1f20;
  --color-accent: #5980a6;
  --color-accent-700: #3f5f80;   /* texto de parágrafo em acento */
  --color-accent-900: #24384c;   /* campo cheio: fundo escuro, tipo em papel */
  --color-neutral-100: #f7f7f8;
  --color-divider: rgba(29,31,32,.18);

  --font-heading: "Barlow Condensed", system-ui, sans-serif;
  --font-body: "Barlow", system-ui, sans-serif;

  --space-1: 3.4px; --space-2: 6.8px;  --space-3: 10.2px;
  --space-4: 13.6px; --space-6: 20.4px; --space-8: 27.2px;

  --radius: 4px;   /* usar apenas em inputs; cards e botões são quadrados */
}
```

Fontes: `<link href="https://fonts.googleapis.com/css2?family=Barlow:wght@400;500;600&family=Barlow+Condensed:wght@500;600;700&display=swap" rel="stylesheet">`

### Regras de tipografia
- Todos os títulos (`h1`–`h4`): `--font-heading`, `text-transform: uppercase`, `line-height: 1.12`, `letter-spacing: -0.015em`.
- Corpo: `--font-body`, `line-height: 1.6`, largura máxima de leitura `62ch` (política: `78ch`).
- Escala: h1 54px (mobile 36px), h2 32px, h3 22px, h4 16px, corpo 15px, legenda 13px.
- `text-wrap: pretty` nos parágrafos.

### Componente `.blueprint` (a assinatura visual)
Moldura quadrada de 1px com um "+" em cada canto. Aplicar em: cards de app, figuras/imagens, botão primário, blocos da seção de privacidade.

```css
.blueprint { position: relative; border: 1px solid var(--color-divider); background: transparent; }
.blueprint .corner { position: absolute; width: 7px; height: 7px; opacity: .9; }
.blueprint .corner::before,
.blueprint .corner::after {
  content: ""; position: absolute; background: var(--color-accent);
}
.blueprint .corner::before { left: 50%; top: 0; width: 1px; height: 100%; transform: translateX(-50%); }
.blueprint .corner::after  { top: 50%; left: 0; height: 1px; width: 100%; transform: translateY(-50%); }
.blueprint .corner.tl { left: -4px; top: -4px; }
.blueprint .corner.tr { right: -4px; top: -4px; }
.blueprint .corner.bl { left: -4px; bottom: -4px; }
.blueprint .corner.br { right: -4px; bottom: -4px; }
```
Markup: `<article class="card blueprint"> … <i class="corner tl"></i><i class="corner tr"></i><i class="corner bl"></i><i class="corner br"></i></article>`

### Botões
```css
.btn { display:inline-flex; align-items:center; gap:8px; min-height:44px; padding:13.6px 27.2px;
       font-family:var(--font-heading); font-size:15px; letter-spacing:.08em; text-transform:uppercase;
       text-decoration:none; border:1px solid transparent; border-radius:0; cursor:pointer; }
.btn-primary   { background:var(--color-accent); color:#fff; }
.btn-primary:hover  { background:var(--color-accent-700); }
.btn-secondary { border-color:var(--color-divider); color:var(--color-text); background:transparent; }
.btn-secondary:hover { background:rgba(29,31,32,.07); }
:focus-visible { outline:2px solid var(--color-accent); outline-offset:2px; }
```

### Imagens
Quadradas, com moldura de 1px e marcas de canto. Fotografias/prints recebem duotone em acento:
`filter: grayscale(1) contrast(1.05);` sobre fundo de acento com `mix-blend-mode: multiply`.

### Grade
Container `max-width: 1120px; margin: 0 auto; padding: 0 27.2px`.
Grade de apps: `display:grid; grid-template-columns: repeat(auto-fill, minmax(300px,1fr)); gap:27.2px`.
Ritmo vertical entre seções: `54.4px` (mobile `40.8px`).

## 5. Páginas

### 5.1 `index.html`

**`<head>`** — `lang="pt-BR"`, viewport, title `Lho Tech Solutions — Jogos e ferramentas para o dia a dia`,
`meta description` = "Jogos incríveis e ferramentas úteis para o seu dia a dia. Diversão e praticidade em cada app.",
Open Graph (title, description, image `assets/og-image.png`, url), `theme-color: #5980a6`, favicon.

**Cabeçalho** — barra com marca "LHO TECH SOLUTIONS" (Barlow Condensed, uppercase, 20px) à esquerda e links `Início · Apps · Privacidade · Suporte` à direita (13px, uppercase, `letter-spacing: .06em`). Sem borda inferior; separação por espaço em branco. Em mobile, os links quebram em segunda linha (`flex-wrap`).

**Hero** — duas colunas (`minmax(320px,1fr)`), colapsa em uma no mobile.
- Kicker: `DESENVOLVEDORA INDEPENDENTE · ANDROID` em `--color-accent-700`.
- H1: "Jogos e ferramentas para o dia a dia".
- Parágrafo PT: "Criamos apps simples, leves e úteis: diversão e praticidade em cada lançamento. Todos os nossos títulos estão disponíveis gratuitamente no Google Play."
- Parágrafo EN (menor, 62% de opacidade): "We build simple, lightweight and useful Android apps — games and everyday tools, all free on Google Play."
- Botões: primário "VER NO GOOGLE PLAY" (link do Play, `target="_blank" rel="noopener"`) + secundário "POLÍTICAS DE PRIVACIDADE" (`privacidade/`).
- Coluna direita: figura `.blueprint` em `aspect-ratio: 4/3` com `assets/hero.jpg` em duotone.

**Seção Apps** — H2 "NOSSOS APPS" com "OUR APPS" ao lado em 13px cinza. Um card `.blueprint` por app:
```
[ícone 64x64 com moldura] KICKER "APLICATIVO 01"
                          H3 NOME DO APP
parágrafo PT (1 linha, 14px)
parágrafo EN (13px, opacidade 60%)
tags: "Grátis" (outline) + "Android" (acento claro)
links: "Google Play" (btn-secondary) · "Privacidade" (btn-ghost → privacidade/app-1.html)
```
Tags: `font-size:11px; padding:3px 10px; border-radius:3px`. Outline = borda 1px; acento = `background:#e6ecf3; color:#24384c`.

**Seção Suporte** — três células: texto explicativo (PT + EN), card com o e-mail `mailto:` (22px, Barlow Condensed), card com link para a página do Play.

**Rodapé** — `© 2026 Lho Tech Solutions` à esquerda, e-mail à direita, 12px uppercase, borda superior de 1px.

### 5.2 `privacidade/index.html`
Fundo `--color-accent-900` com tipo em `--color-neutral-100`. H1 "POLÍTICA DE PRIVACIDADE", parágrafo explicando que cada app tem sua própria página, e uma grade de cards `.blueprint` (borda em branco a 35%) linkando cada `app-N.html`. Rodapé igual ao da home.

### 5.3 `privacidade/app-N.html` (uma por app)
Documento de leitura: fundo claro, `max-width: 78ch`, `padding: 34px`, título + data + 8 seções numeradas em PT e um resumo em EN. Cada página deve trazer no `<head>` `<meta name="robots" content="index,follow">` e title `Política de Privacidade — [Nome do App] | Lho Tech Solutions`.

Conteúdo (substituir `[Nome do App]`; **revisar itens 1–3 conforme o app real**):

> **Política de Privacidade — [Nome do App]**
> Última atualização: [data] · Desenvolvedora: Lho Tech Solutions
>
> A Lho Tech Solutions desenvolveu o aplicativo **[Nome do App]** para Android, distribuído gratuitamente no Google Play. Esta política explica quais dados o app trata, para quê e quais são os seus direitos. Ao usar o app, você concorda com estes termos.
>
> **1. Dados que coletamos** — O aplicativo não solicita cadastro e não coleta dados que identifiquem você pessoalmente (nome, e-mail, telefone ou endereço). Preferências e progresso ficam salvos apenas no seu próprio dispositivo e são apagados ao desinstalar o app.
>
> **2. Serviços de terceiros** — O app pode usar serviços do Google que coletam dados técnicos anônimos (identificador de anúncios, modelo do dispositivo, versão do sistema, falhas) para exibir anúncios e medir estabilidade: Google Play Services, Google AdMob e Firebase. O tratamento desses dados segue as políticas de privacidade dos respectivos provedores.
>
> **3. Permissões** — Solicitamos apenas as permissões necessárias ao funcionamento do app, sempre com o seu consentimento — por exemplo, acesso à internet para carregar conteúdo e anúncios. Nenhuma permissão é usada para finalidades diferentes das informadas.
>
> **4. Crianças** — Não coletamos intencionalmente dados de menores de 13 anos. Se você é responsável e acredita que houve alguma coleta, entre em contato para que removamos as informações.
>
> **5. Segurança e retenção** — Não mantemos servidores próprios com dados de usuários. Os dados técnicos tratados pelos serviços de terceiros são retidos conforme as políticas desses provedores.
>
> **6. Seus direitos (LGPD/GDPR)** — Você pode solicitar confirmação, acesso, correção ou exclusão de dados a qualquer momento pelo e-mail abaixo. Responderemos em até 15 dias.
>
> **7. Alterações** — Podemos atualizar esta política. Publicaremos a nova versão nesta mesma página, com a data de atualização revisada.
>
> **8. Contato** — Dúvidas sobre privacidade: lhotecsolutions@gmail.com
>
> **Privacy Policy — [App Name]** (resumo em inglês)
> Lho Tech Solutions built **[App Name]** as a free Android app on Google Play. The app requires no sign-up and does not collect personally identifiable information; preferences and progress stay on your device and are removed when you uninstall. The app may use Google services (Google Play Services, AdMob, Firebase) that collect anonymous technical data — advertising identifier, device model, OS version and crash reports — to serve ads and measure stability, handled under those providers' own privacy policies. We request only the permissions the app needs to work. We do not knowingly collect data from children under 13. You may request confirmation, access, correction or deletion of data at any time; we reply within 15 days. This policy may be updated on this page with a revised date. Contact: lhotecsolutions@gmail.com

⚠️ **Atenção legal:** se um app **não** exibe anúncios ou **não** usa Firebase, remova essas menções do item 2. O texto precisa bater com o formulário de *Segurança dos Dados* do Play Console.

## 6. Acessibilidade

- Um único `h1` por página; hierarquia de headings sem pular níveis.
- Contraste: acento (#5980a6) só em textos grandes/chrome; parágrafos em acento usam `--color-accent-700`.
- `alt` descritivo em todo ícone e imagem (`alt="Ícone do app [Nome]"`); decorativas com `alt=""`.
- `:focus-visible` com anel de 2px em acento — nunca remover outline.
- Navegação por teclado funcional; links de âncora com `scroll-behavior: smooth`.

## 7. Deploy — GitHub Pages

1. Criar repositório público `lho-tech-solutions`.
2. Commitar tudo na raiz do branch `main`.
3. Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)` → Save.
4. Adicionar arquivo vazio `.nojekyll` na raiz (evita o Jekyll ignorar pastas).
5. URL final: `https://<usuario>.github.io/lho-tech-solutions/` — política do App 1 em `.../privacidade/app-1.html`.
6. No Play Console → Política → Conteúdo do app → *Política de Privacidade*: colar a URL **daquele** app.

## 8. Checklist de entrega

- [ ] `index.html` com hero, grade de apps e suporte, responsivo em 360px e 1440px
- [ ] Uma página de privacidade por app, com URL própria e indexável
- [ ] `privacidade/index.html` listando todas
- [ ] Nomes, descrições e ícones reais de cada app substituídos
- [ ] Itens 1–3 da política revisados app por app
- [ ] E-mail de suporte visível na home e em toda política
- [ ] `.nojekyll` presente; nenhum caminho absoluto (`/assets/...`)
- [ ] OG image e meta description em todas as páginas
- [ ] Zero erros no console; HTML válido (validator.w3.org)

## 9. Prompt inicial sugerido para o assistente

> Leia o SPEC.md do projeto. Gere `styles.css` e `index.html` seguindo exatamente os tokens, o componente `.blueprint` e o conteúdo da seção 5.1. HTML e CSS puros, sem frameworks, sem JavaScript, caminhos relativos, mobile-first. Depois gere `privacidade/index.html` e um `privacidade/app-N.html` para cada app da lista que eu vou passar. Não invente seções que não estão no spec.
