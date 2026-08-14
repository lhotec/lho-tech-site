# Lho Tech Solutions — Website

Website institucional estático para a desenvolvedora Lho Tech Solutions. Site responsivo, bilíngue (PT/EN), com políticas de privacidade individuais para cada app.

## 📂 Estrutura de arquivos

```
/
├── index.html                      Home: hero + grade de apps + suporte
├── privacidade/
│   ├── fio-certo.html              Política do app Fio Certo
│   ├── blocup.html                 Política do app BlocUp
│   ├── calculadora-trabalhista.html Política do app Calculadora Trabalhista
│   └── pipe-water.html             Política do app Pipe Water
├── styles.css                      Estilos compartilhados (mobile-first)
├── assets/
│   ├── icons/                      Ícones dos apps (512x512)
│   ├── og-image.png                Imagem para compartilhamento (1200x630)
│   └── hero.jpg                    Imagem hero da homepage
├── .nojekyll                       Arquivo vazio para GitHub Pages
└── README.md                       Este arquivo
```

## 🎨 Design System

- **Cores**: Azul-aço (#5980a6) sobre fundo claro
- **Tipografia**: Barlow (corpo) + Barlow Condensed (títulos)
- **Componentes**: Molduras 1px com marcas de canto "+" (`.blueprint`)
- **Responsividade**: Mobile-first, sem cantos arredondados, sem gradientes

## 🚀 Deploy no GitHub Pages

1. Criar repositório público `lho-tech-solutions`
2. Commitar todos os arquivos na raiz do branch `main`
3. Acessar **Settings → Pages**
4. Configurar: **Deploy from a branch** → `main` / `/ (root)` → Save
5. URL final: `https://<usuario>.github.io/lho-tech-solutions/`

### ⚠️ Importante para Google Play

No Play Console, registre a URL da política de privacidade de cada app:
- Fio Certo: `.../privacidade/fio-certo.html`
- BlocUp: `.../privacidade/blocup.html`
- Calculadora Trabalhista: `.../privacidade/calculadora-trabalhista.html`
- Pipe Water: `.../privacidade/pipe-water.html`

## 📋 Checklist de entrega

- ✅ `index.html` com hero, grade de apps e suporte, responsivo
- ✅ Uma página de privacidade por app com URL indexável, linkada diretamente no card do app na home
- ✅ E-mail de suporte visível na home e políticas
- ✅ `.nojekyll` presente
- ✅ Caminhos relativos (sem `/assets/...`)
- ✅ OG image e meta description em todas as páginas
- ✅ HTML válido, sem erros no console

## 🛠️ Personalização

### Adicionar novos apps

1. Criar nova linha no grid de apps em `index.html`, com o link `privacidade/novo-app.html` no botão "Privacidade" do card
2. Criar novo arquivo `privacidade/novo-app.html` com a política

### Atualizar assets

Substituir arquivos em `assets/`:
- `icons/`: ícones 512x512 dos apps (PNG)
- `og-image.png`: imagem 1200x630 para compartilhamento
- `hero.jpg`: imagem da seção hero (aspect-ratio 4:3)

## 📞 Contato

E-mail de suporte: **lhotecsolutions@gmail.com**

---

© 2026 Lho Tech Solutions
