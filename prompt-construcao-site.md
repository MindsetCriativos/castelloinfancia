# Prompt de Construção — Site "30 Dias Sem Tela" (Fase 1: Estático)

> Cole este prompt inteiro no Claude Code / Cowork para iniciar a construção.
> Este é um projeto em 2 fases: **agora construímos a página estática, completa e responsiva**.
> Microinterações, animações de entrada e efeitos de scroll ficam para uma fase 2, depois de aprovado o estático.

---

## 0. Instrução de abertura para o Claude Code

Antes de escrever qualquer código, leia e siga os padrões da skill de frontend design do usuário em `claude\skills\frontend-design`. Aplique especialmente:
- Não cair nos 3 "defaults" de IA (fundo creme + serifa + terracota / fundo preto + verde-ácido / editorial jornalístico sem radius). Este projeto já tem uma direção própria definida abaixo — siga-a.
- Trabalhe em duas passadas: primeiro um plano compacto de tokens (cor, tipografia, layout, elemento-assinatura), critique esse plano contra o brief, só then construa.
- Gaste a "ousadia" em UM elemento de assinatura visual: sugestão — as molduras orgânicas de foto (blob shapes) combinadas com os círculos decorativos, que são o elemento mais distintivo das referências coletadas. O resto da página deve ser disciplinado ao redor desse elemento.
- Copy é material de design, não decoração: respeite a copy fornecida na seção 4 deste documento, mas ajuste microcopy (labels de botão, eyebrows, alt text) com a mesma intencionalidade.
- Antes de fechar cada seção, faça uma autocrítica rápida: "isso parece genérico ou foi uma escolha para ESTE projeto?"

Também leia o arquivo `design-tokens.md` (anexo/já enviado nesta conversa) — ele contém a paleta, tipografia, componentes e princípios de raio/sombra extraídos das referências visuais aprovadas pelo cliente. Use-o como ponto de partida, não como camisa de força: se algo ali conflitar com um julgamento melhor de design para este brief específico, sinalize a mudança e justifique.

---

## 1. Contexto do projeto

- **Cliente**: Daniela Castello Nuovo — especialista em desenvolvimento infantil.
- **Produto**: "30 Dias Sem Tela" — kit digital em PDF com 10 jogos de alfabetização lúdica + 3 bônus, pagamento único, R$29,90.
- **Página**: landing page de vendas (1 página, scroll único), objetivo = conversão para o checkout (link externo Kiwify).
- **Público**: mães que trabalham fora, sentem culpa pelo tempo de tela dos filhos, buscam alternativas educativas e querem se sentir presentes mesmo sem ter tempo de sobra. Tom: acolhedor, empático, nunca culpabilizante.
- **Fase atual**: reestruturação visual e de UX de uma página já existente (a copy e a oferta permanecem as mesmas, com retoques de clareza). Ver `design-tokens.md` para o sistema visual.

---

## 2. Requisitos técnicos (Fase 1 — Estático)

- HTML semântico + CSS (pode ser um único arquivo ou HTML/CSS/JS separados — decisão do Claude Code).
- **Sem animações de entrada, sem scroll-reveal, sem microinterações nesta fase.** Estado final visual = como se a página já tivesse "aterrissado" (opacidade 1, posição final), só sem transições. O objetivo agora é validar layout, hierarquia, copy e sistema visual.
- Totalmente responsivo (mobile-first), com breakpoints para tablet e desktop.
- Imagens: usar placeholders com proporção e legenda indicando o que deve entrar ali (ex: `[FOTO: mãe sorrindo com criança, tom caloroso]`), já que os assets reais serão inseridos depois.
- Acessibilidade: seguir a seção 8 do `design-tokens.md` (contraste AA, alt text, foco visível, tamanho de toque mínimo).
- Botões de CTA devem ser `<a>` com `href="#"` por enquanto (placeholder do link de checkout real).

---

## 3. Estrutura de seções (wireframe)

```
┌─────────────────────────────────────────┐
│ [1] HERO                                 │
│  Headline + subheadline + CTA            │
│  Foto/mockup do produto (blob frame)     │
├─────────────────────────────────────────┤
│ [2] IDENTIFICAÇÃO (dor da mãe)           │
│  Texto empático em 1ª pessoa + foto      │
├─────────────────────────────────────────┤
│ [3] VIRADA DE CHAVE                      │
│  "Você não precisa escolher entre..."    │
│  Autoridade da especialista              │
├─────────────────────────────────────────┤
│ [4] APRESENTAÇÃO DO DESAFIO              │
│  "30 dias sem tela" + checklist rápido   │
│  + CTA intermediário                     │
├─────────────────────────────────────────┤
│ [5] OS 10 JOGOS                          │
│  Grid de 10 cards (imagem+título+desc)   │
├─────────────────────────────────────────┤
│ [6] POR QUE FUNCIONA                     │
│  4 cards: Neurociência / Solução /       │
│  Tranquilidade / Economia                │
├─────────────────────────────────────────┤
│ [7] BÔNUS                                │
│  3 cards de bônus com valor "de/por"     │
├─────────────────────────────────────────┤
│ [8] OFERTA (tudo que você leva)          │
│  Lista com valores riscados + preço final│
│  + CTA principal                         │
├─────────────────────────────────────────┤
│ [9] GARANTIA 7 DIAS                      │
│  Selo + texto de segurança               │
├─────────────────────────────────────────┤
│ [10] PARA QUEM É / NÃO É                 │
│  2 colunas (✅ perfeito para / ❌ não é)  │
├─────────────────────────────────────────┤
│ [11] FAQ                                 │
│  Acordeão, 4 perguntas                   │
├─────────────────────────────────────────┤
│ [12] CTA FINAL                           │
│  "Última chance" + duas opções + CTA     │
└─────────────────────────────────────────┘
```

---

## 4. Copy revisada (seguir esta redação — retoques de UX Writing já aplicados)

> Mantém a mesma informação e oferta do site original, com frases mais diretas, menos repetição e CTAs mais específicos.

### [1] Hero

- **Eyebrow**: Desafio para famílias reais
- **Headline**: Ajude seu filho a largar a tela — sem culpa, sem brigas.
- **Subheadline**: Um método simples para transformar o tempo livre em memórias de infância, mesmo com a rotina corrida de quem trabalha fora.
- **CTA primário**: Quero uma infância mais saudável
- **Legenda sob o CTA**: Acesso imediato · Pagamento único · R$29,90

### [2] Identificação (dor)

- **Título**: Você chega em casa, e a cena se repete.
- **Corpo**: Você acorda cedo, trabalha o dia inteiro e faz o melhor que pode pela sua família. Mas quando chega em casa, encontra seu filho na frente de uma tela — de novo. E vem a pergunta que dói: *"será que ele vai lembrar da infância só pelo tablet ligado?"*
- **Reforço**: A culpa não aparece porque você ama menos. Aparece porque você quer mais para ele: descoberta, criatividade, momentos que ficam.

### [3] Virada de chave (autoridade)

- **Título**: Trabalhar e estar presente não são opostos.
- **Corpo**: Como especialista em desenvolvimento infantil, sei que o aprendizado acontece de forma mais profunda quando a criança participa ativamente da brincadeira. Desafios, movimento, linguagem e criatividade desenvolvem habilidades essenciais — e tornam esse tempo livre prazeroso para todo mundo, inclusive para você.

### [4] Apresentação do desafio

- **Eyebrow**: O desafio
- **Título**: 30 dias sem tela
- **Corpo**: Uma jornada de aventura e diversão para manter as crianças longe das telas e motivadas todos os dias — com uma surpresa reservada para o último módulo.
- **Checklist**:
  - Método testado por mais de 3.000 mães e professoras
  - Para crianças de 4 a 10 anos (funciona até com as "difíceis")
  - PDF pronto para imprimir e começar hoje
  - Passo a passo simples para cada jogo
  - Funciona em casa e na escola
- **CTA**: Começar os 30 dias sem tela

### [5] Os 10 jogos

- **Eyebrow**: Kit completo
- **Título**: 10 jogos, cada um trabalhando uma habilidade diferente
- **Subtítulo**: Juntos, formam o material completo para tornar a infância dos pequenos mais leve e saudável.

Cards (título + objetivo + descrição curta + selo):
1. **Baralho das Sílabas** — Formar palavras juntando sílabas nas cartas. Desenvolve consciência fonológica brincando. *Ideal para quem está começando a juntar sílabas.*
2. **Baralho do Alfabeto** — Associar cada letra a uma figura. Fixação do alfabeto de forma natural. *Perfeito para crianças de 4–5 anos.*
3. **Baralho Palavra Secreta** — Desembaralhar letras para descobrir a palavra. Desenvolve raciocínio e ortografia. *Desafia e diverte ao mesmo tempo.*
4. **Baralho Forme Frases** — Organizar cartas de palavras em frases com sentido. Primeiros passos da estrutura gramatical. *Prepara para a escrita de textos.*
5. **Baralho Quem Sou Eu** — Adivinhar a palavra a partir de pistas. Desenvolve interpretação e vocabulário. *Trabalha raciocínio lógico.*
6. **Baralho Forme Palavras** — Escrever o nome certo a partir de uma figura sorteada. Treino de ortografia disfarçado de jogo.
7. **Baralho Descubra a Palavra** — Unir figuras para formar palavras compostas. Expande o vocabulário brincando.
8. **Baralho Responda Aí** — Responder perguntas sobre as cartas. Estimula expressão oral e escrita.
9. **Baralho das Rimas** — Encontrar palavras que rimam. Consciência fonológica avançada, base para a musicalidade da língua.
10. **Bingo das Sílabas** — Marcar as sílabas certas ao ouvir a palavra. Diversão garantida em grupo — ótimo para sala de aula ou família toda.

### [6] Por que funciona

- **Eyebrow**: A ciência por trás do método
- **Card 1 — Baseado em neurociência**: Crianças aprendem até 300% mais rápido quando estão se divertindo. O cérebro infantil foi feito para aprender brincando.
- **Card 2 — Resolve o problema real**: Transforma o "tempo passando" em experiências ricas de aprendizagem, diversão e conexão.
- **Card 3 — Tranquilidade**: Menos culpa, mais presença. Você continua fazendo parte das melhores lembranças da infância do seu filho — mesmo trabalhando.
- **Card 4 — Economia**: Menos de R$3,00 por dia. Material para anos de uso, imprima quantas vezes quiser.

### [7] Bônus

- **Eyebrow**: Incluso no seu kit
- **Bônus 1 — Lancheira Inteligente**: Guia prático com opções nutritivas e atrativas para facilitar a rotina da família. *De R$37 — hoje incluso.*
- **Bônus 2 — Mestre das Formas**: Atividades lúdicas para reconhecimento de formas geométricas, percepção visual e raciocínio lógico. *De R$47 — hoje incluso.*
- **Bônus 3 — Teddy Bear Edition**: Momentos de relaxamento criativo que estimulam imaginação, concentração e coordenação motora fina. *De R$107 — hoje grátis.*

### [8] Oferta (tudo que você leva)

- **Título**: Tudo que você leva hoje
- Lista com valor riscado:
  - 10 baralhos completos de alfabetização — ~~R$197~~
  - Lancheira Inteligente — ~~R$37~~
  - Mestre das Formas — ~~R$47~~
  - Teddy Bear Edition — ~~R$107~~
- **Valor total**: R$388
- **Por**: R$29,90 — pagamento único, acesso vitalício, sem mensalidades
- **CTA principal**: Garantir meu kit agora
- **Microcopy de confiança abaixo do botão**: Compra segura · Acesso imediato · Garantia de satisfação

### [9] Garantia

- **Título**: Garantia de 7 dias, sem letra miúda
- **Corpo**: Baixe, imprima, jogue com seu filho. Se em 7 dias você não perceber menos tempo de tela, mais momentos de aprendizado e interação, e evolução visível nas habilidades — devolvemos 100% do seu dinheiro. Sem perguntas, sem burocracia. O risco é nosso; a transformação é sua.

### [10] Para quem é / não é

**✅ Perfeito para você que:**
- Trabalha fora e sente que não consegue dar toda a atenção que gostaria
- Se preocupa com o tempo de tela do seu filho e busca alternativas educativas
- Quer uma infância com propósito, onde brincar também é aprender
- Conta com avós, tias ou babás e precisa de atividades fáceis de aplicar
- Valoriza mais brincadeiras e descobertas, e menos tempo ocioso diante das telas
- Quer criar memórias afetivas que seu filho leve para a vida toda

**❌ Não é para você que:**
- Acredita que a criança deve passar o dia todo em frente a telas
- Não valoriza o brincar como parte do desenvolvimento infantil
- Acredita que aprender só acontece dentro da sala de aula

### [11] FAQ

- **Funciona para qual idade?** De 4 a 10 anos. Os baralhos têm níveis diferentes de dificuldade, da fase pré-silábica até a alfabetização completa.
- **Serve para sala de aula?** Sim! Professoras podem imprimir para toda a turma — o Bingo das Sílabas, inclusive, é perfeito para grupos.
- **Posso imprimir quantas vezes quiser?** Sim. Uma vez baixado, é seu para sempre — imprima para todos os filhos, sobrinhos ou alunos.
- **E se meu filho não gostar de um jogo?** Por isso são 10 baralhos diferentes — cada criança se identifica com alguns mais que outros. E se ainda assim não funcionar, você tem a garantia de 7 dias.

### [12] CTA final

- **Título**: A infância passa rápido — e não volta
- **Corpo**: Você tem duas escolhas agora.
- **Opção 1 (❌)**: Correr o risco de seu filho passar a melhor parte da infância nas telas.
- **Opção 2 (✅)**: Investir R$29,90 — menos que uma pizza — e começar hoje a transformar essa rotina.
- **CTA**: Garantir o kit agora

---

## 5. Entregável esperado desta fase

1. Página HTML/CSS estática completa, todas as 12 seções, responsiva.
2. Sistema de cores/tipografia aplicado conforme `design-tokens.md`.
3. Um breve resumo do "plano de design" (tokens + elemento-assinatura escolhido) antes do código, como pede a skill de frontend-design.
4. Nenhuma animação/transição ainda — isso entra na Fase 2, depois da aprovação do layout.
