# marcos.afns — portfolio

> Portfólio pessoal minimalista construído com Nuxt 4, Tailwind CSS e animações em canvas.

![Nuxt](https://img.shields.io/badge/Nuxt-4-00DC82?style=flat-square&logo=nuxt.js&logoColor=white)
![Vue](https://img.shields.io/badge/Vue-3-4FC08D?style=flat-square&logo=vue.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind-3-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)

---

## ✦ Sobre

Site pessoal com foco em simplicidade e experiência de usuário.
Duas páginas, zero componentes externos, animações feitas à mão.

---

## ✦ Stack

- **[Nuxt 4](https://nuxt.com)** — framework principal
- **[Vue 3](https://vuejs.org)** + Composition API + `<script setup>`
- **[TypeScript](https://www.typescriptlang.org)** — tipagem em todo o projeto
- **[Tailwind CSS](https://tailwindcss.com)** — estilização utilitária
- **[Nuxt Icon](https://github.com/nuxt/icon)** + **Lucide** — ícones
- **Canvas API** — rastro e explosão de partículas interativas

---

## ✦ Páginas
```
/          → Apresentação com animação de entrada e efeito de partículas no mouse
/contact   → Cards interativos com links para redes sociais
```

---

## ✦ Funcionalidades

- Animação de entrada em cascata com `animation-fill-mode: both`
- Rastro de partículas que segue o cursor via Canvas 2D
- Explosão de partículas ao clicar em qualquer lugar da tela
- Orbs de fundo que reagem ao movimento do mouse via paralaxe
- Design responsivo, dark por padrão

---

## ✦ Rodando localmente
```bash
# instalar dependências
pnpm install

# rodar em desenvolvimento
pnpm dev

# build para produção
pnpm build

# preview do build
pnpm preview
```

---

## ✦ Estrutura
```
├── pages/
│   ├── index.vue       # home com canvas interativo
│   └── contact.vue     # página de contato
├── layouts/
│   └── default.vue     # layout base com header e footer
├── components/
│   ├── AppHeader.vue
│   └── AppFooter.vue
├── app.vue
└── nuxt.config.ts
```

---

## ✦ Deploy

Hospedado na **[Vercel](https://vercel.com)** com deploy automático a cada push na `main`.

---

<p align="center">
  feito com <strong>obsessão por detalhes</strong> — marcos afns
</p>