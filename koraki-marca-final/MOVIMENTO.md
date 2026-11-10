# Koraki — guia de movimento

Complementa o `GUIA.md` (cor, tipografia, logo). Aqui está **como a marca se move** em vídeo. Aprovado em 26/10/2026.
Tokens prontos para usar em composições: `tokens.css` (cores, fonte, eases, durações).

## A assinatura: o corte

O símbolo é um bloco partido por um corte só, em pé-de-galinha. Em movimento, **o corte é o gesto da marca**: uma linha âmbar atravessa e parte o quadro, e a cena seguinte nasce pela fresta.

- **Ângulo do corte:** o mesmo do símbolo, cerca de 24° de inclinação (de (42.9, 45) a (92, 23.1) no viewBox 100×100). Nunca horizontal reto, nunca vertical.
- **Linha:** âmbar `#F0A23B`, 3 px em 1080p (4 px em 9:16), sem brilho, sem sombra.
- **Tempo:** a linha cruza em 0,35 s (`power4.inOut`). Na hora em que termina, as duas metades se separam em 0,30 s (`power4.in` espelhado: a de cima sai para cima, a de baixo para baixo) e revelam a próxima cena.
- **Racionamento:** no máximo **2 vezes por filme**: na abertura e no momento de virada (payoff) ou no encerramento. Não é a transição padrão entre cenas.

## Abertura de marca (1,5 a 2,5 s)

Sub-composição `koraki-abertura.html` (ver `projetos/teste-marca/compositions/`).
1. As duas metades do símbolo entram uma contra a outra (de cima e de baixo), 0,55 s `power4.out`, e fecham o bloco.
2. Pausa de 6 quadros (0,2 s): o bloco parado, o corte aparente.
3. O corte se abre: as metades se afastam ~9% da altura do símbolo, 0,4 s `expo.out`, e o título nasce pela fresta.

Regra do HyperFrames: o quadro 0 é a miniatura (thumbnail) e nunca pode ser só o logo. Em vídeo de rede social, **a abertura de marca não abre o vídeo**. O gancho vem primeiro, e a marca aparece no fim ou no payoff.

## Encerramento (2,5 a 3,5 s)

Sub-composição `koraki-encerramento.html`.
1. O corte âmbar cruza o quadro e as metades da última cena saem.
2. O símbolo se fecha (metades entram) ao lado do nome; assinatura horizontal (`svg/koraki-horizontal-fundo-escuro.svg`).
3. CTA em uma linha (ex.: "koraki.com.br" ou "Chama no direct"), 400, creme.
4. Segura **2 a 3 s** parado. O logo aparece uma vez no filme, com peso.

## Movimento em geral

| Papel | Ease | Duração (30 fps) |
|---|---|---|
| Entrada de título/objeto | `power4.out` ou `expo.out` | 0,45–0,6 s |
| Saída | `power3.in` | ~60% da entrada (0,27–0,36 s) |
| Câmera (push, pan, zoom) | `power2.inOut` | 0,8–1,6 s |
| Marca (uma vez por filme) | `back.out(1.4)` permitido | 0,5 s |
| Defasagem entre palavras | — | 3–4 quadros (normal), 6 quadros (frase de impacto) |
| Defasagem entre itens | — | 2 quadros |

- **Um movimento herói por plano.** O resto acompanha com 50–70% do deslocamento e começa 100–200 ms depois.
- **Título que pousou fica parado.** Nada de "respirar", flutuar ou encolher enquanto é lido.
- **Sem crossfade entre mundos.** Transição tem causa na tela: o objeto clicado vira o próximo plano, o corte parte a cena, a câmera mergulha num detalhe.
- **Elástico e bounce:** proibidos, exceto o `back.out` da marca, uma vez.

## Cor em movimento

- **Proporção:** Noite ~70% · Igarapé ~15% (superfícies, mundos secundários) · Creme ~10% (texto) · Âmbar ≤5%.
- **Âmbar é racionado:** uma palavra destacada, o payoff e o encerramento. Se tudo é âmbar, nada é.
- **Verde-água:** dados, gráficos, estados ("ok", "enviado", "agendado").
- **Sem gradiente** de fundo (dá faixas no H.264 e é proibido no guia), sem glow, sem partículas decorativas.

## Tipografia em movimento

- **Familjen Grotesk:** 600 nos títulos (`letter-spacing: -0.03em`), 400 no texto e no CTA. Arquivos em `fontes/`.
- **Tamanhos em 1080p:** título 84–140 px, apoio 36–48 px, nada lido abaixo de 28 px. Em 9:16, títulos ×1,35.
- **Por tela:** no máximo 6 palavras por linha e uma linha de título de cada vez.
- **Apoio monoespaçado:** **JetBrains Mono** (já vem no HyperFrames), só em cenas de terminal, código ou automação.

## Som da marca

- **No corte:** um impacto seco e curto (madeira, clique grave ou "tick"), com o pico 1 quadro depois da imagem. Sem sino, sem "plim" sintético.
- **Trilha:** eletrônica orgânica ou minimalista, 95–120 BPM. Nada épico ou "inspiracional" genérico.

## Não faça

Logo no quadro 0 · corte âmbar em toda transição · âmbar como cor de fundo · tudo entrando com fade-and-slide-up · texto se mexendo enquanto é lido · três cards em fila · gradiente azul/roxo · brilho, sombra ou contorno no símbolo.
