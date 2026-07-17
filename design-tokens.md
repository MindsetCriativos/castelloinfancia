# Design Tokens & Diretrizes Visuais — Site Infância/Maternidade

> Documento de referência para o Claude Code construir a página estática.
> Extraído da análise de 4 referências visuais (Blippi Kindergarten, Rainbow Play School,
> Artistry Kids Academy, Ruang Edit) + moodboard base (Castello Infância).
> Estética-alvo: **soft, colorida, acolhedora, lúdica, mas com acabamento editorial/premium** —
> não "infantil demais", e sim "para a mãe que quer o melhor pro filho".

---

## 1. Padrões observados nas referências

| Elemento | O que se repete nas 4 referências |
|---|---|
| Cantos | Border-radius generoso em TUDO — cards 20–32px, botões/pills totalmente arredondados (999px) |
| Fotos | Molduras orgânicas (blob/torn-paper mask), nunca retângulo puro; círculos coloridos decorativos atrás/ao lado |
| Cor | Blocos de seção em pastel (não a página toda), alternando fundo branco/creme com blocos coloridos |
| Badges | Pills coloridas para categorização (faixa etária, tags, valores) — texto curto, fundo sólido saturado, texto branco/escuro |
| Decoração | Elementos soltos espalhados: estrelinhas, círculos, rabiscos/squiggles, pequenos ícones — nunca centralizados, sempre "jogados" no espaço negativo |
| Tipografia | Mistura de 2 famílias: uma expressiva (arredondada/serifa itálica) para headlines + uma neutra/limpa para corpo |
| Divisores | Seções raramente se separam com linha reta — ondas, nuvens, blobs cortando a transição |
| CTA | Botão pill, cor de alto contraste com o fundo, geralmente com micro-ícone ou seta |
| Cards numerados | Grids de features com números grandes coloridos (01, 02, 03...) ou ícones ilustrativos em blocos coloridos |
| Prova social | Avatares circulares pequenos sobrepostos ao texto, contador com "+" (ex: "345+ estudando") |

---

## 2. Paleta de cores

Paleta soft-colorida, pensada para transmitir acolhimento + confiança (não é "parquinho", é "storybook editorial").

```css
:root {
  /* Base neutra quente */
  --color-bg-base: #FFFBF5;        /* creme, fundo padrão da página */
  --color-bg-alt: #FFFFFF;         /* branco puro para seções de respiro */
  --color-text-primary: #3A2E2A;   /* marrom escuro suave, não preto puro */
  --color-text-secondary: #7A6A63; /* texto de apoio */

  /* Cores de seção (usar 1 por bloco, nunca misturar 3+ na mesma seção) */
  --color-pink-soft: #FFE1E9;      /* fundo de seção rosa */
  --color-pink-accent: #FF7FA3;    /* CTA/destaque rosa */
  --color-pink-quote-text: #BA4B6D; /* texto corrido em --font-accent sobre fundo claro — contraste AA (4.87:1) */

  --color-lilac-soft: #EDE4FF;     /* fundo de seção lilás */
  --color-lilac-accent: #9B7FE0;   /* destaque lilás */

  --color-yellow-soft: #FFF3D6;    /* fundo de seção amarelo */
  --color-yellow-accent: #FFC94A;  /* destaque amarelo/dourado */

  --color-mint-soft: #DFF6EC;      /* fundo de seção verde-água */
  --color-mint-accent: #5BC9A0;    /* destaque verde */

  --color-blue-soft: #E1F0FF;      /* fundo de seção azul */
  --color-blue-accent: #6FAEE0;    /* destaque azul */

  /* Semânticas */
  --color-cta-primary: #FF7FA3;    /* botão principal — rosa vibrante */
  --color-cta-text: #FFFFFF;
  --color-success: #5BC9A0;
  --color-warning: #FFC94A;

  /* Sombra */
  --shadow-soft: 0 8px 24px rgba(58, 46, 42, 0.08);
  --shadow-card-hover: 0 14px 32px rgba(58, 46, 42, 0.14);
}
```

Regra de uso: **cada seção usa 1 cor-base + neutros**. Nunca todas as cores na mesma dobra da tela — isso é o que dá o efeito "clean apesar de colorido" visto nas referências 3 e 4.

---

## 3. Tipografia

```css
:root {
  --font-display: "Fredoka", "Baloo 2", sans-serif;   /* títulos — arredondada, amigável, mas não infantilizada */
  --font-accent: "Kalam", cursive;                     /* toques manuscritos pontuais, tipo ref. 3 — traço mais grosso que Caveat, sem itálico sintético */
  --font-body: "Nunito", sans-serif;                   /* corpo de texto — arredondada, amigável, combina com --font-display */

  --fs-hero: clamp(2.2rem, 5vw, 3.5rem);
  --fs-h2: clamp(1.6rem, 3vw, 2.4rem);
  --fs-h3: 1.3rem;
  --fs-body: 1.15rem;
  --fs-small: 0.9rem;

  --fw-bold: 700;
  --fw-semibold: 600;
  --fw-regular: 400;
}
```

- Palavras-chave dentro de headlines recebem destaque de cor (ex: "melhor **infância**" com a palavra em `--color-pink-accent`), como visto na ref. 1 e 4.
- Uso pontual da fonte manuscrita (`--font-accent`) em 1–2 palavras por seção, nunca em blocos de texto inteiros — efeito "nota escrita à mão" (ref. 3).
- Em texto corrido (frases inteiras, não só 1–2 palavras) usar `--color-pink-quote-text` (`#BA4B6D`) em vez de `--color-pink-accent-dark` — cor vibrante + traço fino de fonte manuscrita prejudica leitura; títulos/badges curtos podem seguir com a cor normal.

---

## 4. Raio, espaçamento e sombra

```css
:root {
  --radius-sm: 12px;    /* badges pequenas, inputs */
  --radius-md: 20px;    /* cards padrão */
  --radius-lg: 32px;    /* blocos grandes, hero image */
  --radius-pill: 999px; /* botões, tags, badges */

  --space-section: clamp(64px, 10vw, 120px); /* respiro vertical entre seções */
  --space-card-gap: 24px;
  --container-max: 1140px;
}
```

---

## 5. Molduras orgânicas de imagem (assinatura visual das referências)

Fotos nunca aparecem como retângulo puro. Usar `clip-path` com blob orgânico ou máscara SVG, variando por seção para não repetir a mesma forma:

```css
.img-blob-1 { clip-path: polygon(8% 0%, 92% 4%, 100% 88%, 76% 100%, 4% 96%); }
.img-blob-2 { border-radius: 42% 58% 60% 40% / 45% 40% 60% 55%; } /* blob orgânico */
```

Adicionar círculo decorativo sólido/outline atrás ou tangenciando a foto (visto em todas as 4 refs):

```html
<div class="photo-wrap">
  <div class="deco-circle deco-circle--pink"></div>
  <img class="img-blob-2" src="..." alt="..." />
</div>
```

---

## 6. Componentes-chave

**Badge/Pill** (faixa etária, tag, categoria)
- fundo sólido de cor de acento, texto branco ou escuro conforme contraste, `--radius-pill`, padding `6px 16px`, `--fs-small`, `font-weight: 600`

**Card de feature/benefício**
- fundo branco ou pastel, `--radius-md`, `--shadow-soft`, ícone ou número grande no topo, hover = leve `translateY(-4px)` + `--shadow-card-hover`

**Botão CTA**
- `--radius-pill`, padding generoso (`16px 32px`), cor de alto contraste, ícone seta opcional, hover = leve scale (1.03) + sombra

**Divisor de seção (wave/blob)**
- SVG de onda ou nuvem entre blocos de cor diferente, no lugar de linha reta — usar `<svg>` posicionado absoluto na borda da seção

**Elementos decorativos soltos**
- estrelinhas, círculos, rabiscos SVG posicionados `absolute`, `opacity: 0.6–0.9`, tamanhos pequenos (16–40px), nunca centralizados no conteúdo — sempre nas margens/cantos

---

## 7. Microinterações e animação (para o Claude Code implementar)

```css
/* Respeitar sempre */
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}
```

- **Entrada de seção ao rolar**: fade + translateY(24px→0), `IntersectionObserver`, stagger de 80–120ms entre elementos filhos de uma mesma seção.
- **Hover em card**: translateY(-4px) + sombra mais forte, 200ms ease-out.
- **Hover em botão CTA**: scale(1.03), 150ms.
- **Ícones/decorações soltas**: animação de flutuação sutil contínua (translateY ±6px, 4–6s ease-in-out infinite) — dá vida sem ser irritante.
- **Gradiente de fundo entre seções**: transição suave de cor usando pseudo-elemento com gradient blend na borda de duas seções adjacentes, em vez de corte seco.
- Nunca mais de 2 animações continuas simultâneas na viewport (evitar poluição visual).

---

## 8. Acessibilidade (não negociável)

- Contraste mínimo AA (4.5:1) em todo texto sobre fundo colorido — testar cada `--color-*-soft` com `--color-text-primary`.
- Todo `<img>` com `alt` descritivo.
- Foco visível customizado (outline colorido, não removido): `:focus-visible { outline: 3px solid var(--color-lilac-accent); outline-offset: 2px; }`
- Navegação por teclado testável em todos os CTAs e no FAQ (accordion com `aria-expanded`).
- `prefers-reduced-motion` respeitado (ver seção 7).
- Tamanho de toque mínimo 44x44px em botões/links no mobile.

---

## 9. O que NÃO fazer

- Não usar as 5 cores de acento na mesma seção — 1 cor dominante por bloco.
- Não usar imagens em retângulo puro sem tratamento (perde a identidade visual da referência).
- Não exagerar em animação de entrada — 1 efeito consistente (fade+slide) em toda a página, não um efeito diferente por seção.
- Não usar preto puro (`#000`) — sempre o marrom escuro suave definido em `--color-text-primary`.
