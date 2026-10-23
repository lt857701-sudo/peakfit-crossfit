# Auditoria Técnica — PEAKFIT CrossFit

Metodologia: `skill/reference/audit.md` (Impeccable). 5 dimensões, nota 0-4 cada.

## Resultado

| # | Dimensão | Nota | Principal achado |
|---|----------|------|------------------|
| 1 | Acessibilidade (A11y) | 3 | Semântica OK, headings corrigidos, foco visível adicionado; faltam labels visíveis em alguns links sociais (aria-label presente) |
| 2 | Performance | 2 | Lazy loading aplicado abaixo da dobra; fontes e imagens via CDN externas bloqueiam render inicial |
| 3 | Teming | 2 | Cores em tailwind config (tokens), mas valores hard-coded em classes utilitárias espalhadas |
| 4 | Responsividade | 3 | Grid responsivo Tailwind, sem rolagem horizontal; touch targets corrigidos a 44px |
| 5 | Integridade de implementação | 3 | Coerente com identidade PEAKFIT; detector limpo de skipped-heading e dark-glow |

**Total: 13/20 — Acceptable (significant work needed)**

---

### 1. Acessibilidade (A11y) — 3/4
- [x] HTML semântico: `<header>`, `<nav>`, `<section>`, `<article>`, `<footer>`
- [x] Hierarquia de headings: h1 → h2 → h3 → h4 sem skips (detector confirmou)
- [x] Alt text em todas as imagens (`alt` descritivo em pt-BR)
- [x] Foco visível para teclado (`focus-visible:ring`) em nav e CTAs
- [x] Contraste: texto branco #fff sobre #0b0d0e ≈ 15.6:1; text-gray-300 ≈ 11:1 (acima de 4.5:1)
- [ ] Links sociais no rodapé usam `aria-label` (OK) mas não têm texto visível — padrão aceitável para ícones
- [ ] Formulário da newsletter não exibe mensagem de sucesso/erro após submit (`onsubmit="event.preventDefault()"` sem feedback)

### 2. Performance — 2/4
- [x] `loading="lazy" decoding="async"` em imagens abaixo da dobra
- [x] Hero acima da dobra sem `loading="lazy"` (carrega com prioridade)
- [ ] Fontes via Google Fonts CDN (bloqueio de render; `preconnect` presente)
- [ ] Imagens de programas/testimonials/blog via Google Imagens (URLs externas, sem otimização de tamanho)
- [ ] Sem `srcset`/`sizes` para imagens responsivas
- [ ] Tailwind via CDN (compilação no cliente)

### 3. Teming — 2/4
- [x] Tokens definidos em `tailwind.config` (brand.lime, brand.dark, etc.)
- [ ] Valores hard-coded repetidos em classes utilitárias em todo o HTML
- [ ] Sem variáveis CSS / design system centralizado extraível

### 4. Responsividade — 3/4
- [x] Grid responsivo (`grid-cols-1 sm:grid-cols-2 lg:grid-cols-4`)
- [x] Sem rolagem horizontal (`overflow-x: hidden` no body)
- [x] Touch targets ≥ 44px (botões de depoimento corrigidos de 36px → 44px)
- [x] Textos escalam (`sm:text-lg`, `lg:text-[4.2rem]`)
- [ ] Não testado fisicamente em 360/390/430/768/1024/1280/1440px

### 5. Integridade de implementação — 3/4
- [x] Identidade visual preservada (cores lima, montanha, fonte Plus Jakarta Sans)
- [x] Detector Impeccable limpo: `skipped-heading` e `dark-glow` removidos
- [ ] Restantes do detector: `overused-font` (identidade), `flat-type-hierarchy` (falso positivo estático), `nested-cards` (escolha de design, baixo risco)

---

## Recomendações de comando (ordem de prioridade)

1. `impeccable adapt` — validar responsividade nos breakpoints de teste (360–1440px)
2. `impeccable optimize` — imagens locais otimizadas, `srcset`, fontes self-hosted
3. `impeccable polish` — revisão final antes do deploy

---

## Arquivos modificados nesta sessão

- `public/index.html`: remoção de eyebrows/kickers, remoção de glow zero-offset e `drop-shadow`, remoção de `backdrop-blur-sm` (glassmorphism), remoção de `.neon-glow` CSS, ids `#comece`/`#avaliacoes`/`#blog`, hierarquia de headings, touch targets 44px, `loading="lazy"`, meta SEO, focus-visible, links internos corrigidos
- `public/robots.txt`, `public/sitemap.xml`: criados (SEO técnico)
- `package.json`, `.gitignore`, `README.md`, `progress.md`: criados
