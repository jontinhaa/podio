# AGENTS.md — Pódio

Regras deste projeto para qualquer agente (Claude Code, Codex, Antigravity). O `CLAUDE.md` importa este arquivo; mantenha as regras gerais aqui.

## Projeto

- O que é: app de corrida que transforma as ruas da cidade numa disputa por ranking (dono do trecho, patentes, grupos e guerra de grupos). Briefing completo em `PODIO.md`.
- Cliente: produto próprio do Jhonatan <!-- completar: confirme -->
- Tipo: mobile — risco alto (o app vai para a mão de qualquer pessoa), com login, pagamento e dados de menores de 18 anos
- Público e tom dos textos: corredores brasileiros, de iniciantes a assessorias de corrida <!-- completar: tom dos textos -->

## Stack

- Sugerida no briefing, ainda não decidida: Expo / React Native (`expo-location` e TaskManager para GPS em segundo plano) e Supabase (Postgres com PostGIS, Auth, Storage, RLS) <!-- completar: confirmar a stack e o provedor de pagamento -->
- App em: `.` (raiz do repositório; ajuste se o app ficar numa subpasta)
- Hospedagem: <!-- completar: API/backend e lojas (App Store, Google Play) -->

## Comandos

- Desenvolvimento: <!-- completar quando o app existir -->
- Build: <!-- completar quando o app existir -->

## Comandos de verificação

O pente-fino roda estes comandos, nesta ordem, antes de entregar. Todos precisam passar.

<!-- completar: liste só comandos que existem de verdade no package.json (ou pubspec.yaml), por exemplo `npm run lint`, `npx tsc --noEmit`, `npm test`. Use `cd <pasta> &&` se o app ficar numa subpasta. -->

## Estrutura

<!-- completar quando o app existir -->

## Convenções

- Dependência nova só com justificativa no pedido e aprovação do usuário.
- Textos visíveis em português do Brasil, no tom definido acima.
- <!-- completar: regras do projeto -->

## Design system

- Fonte da verdade: <!-- completar: arquivo de tokens / tema do app -->
- Use os tokens e os componentes do design system; nada de cor, espaçamento, raio, sombra ou fonte fixos no código.
- Breakpoints: <!-- completar -->

## Crédito Koraki

- O rodapé de todas as páginas termina com "Feito por" seguido do logo horizontal da Koraki, os dois dentro de um só link para `https://korakitech.com` (`target="_blank" rel="noopener"`). A imagem leva `alt="Koraki"`, para o link ser lido como "Feito por Koraki". No app (mobile), o crédito vai na tela "Sobre".
- Arquivos em `koraki-marca-final/` (não edite; regras em `koraki-marca-final/GUIA.md`). Use `svg/koraki-horizontal-fundo-escuro.svg` em rodapé escuro e `svg/koraki-horizontal-fundo-claro.svg` em rodapé claro. Em fundo de cor média, use a versão de uma cor que der mais contraste (`*-1cor-noite` ou `*-1cor-creme`).
- O logo tem no mínimo 96 px de largura, sem esticar, girar, sombra ou contorno. Deixe um respiro de pelo menos metade da altura do símbolo entre o texto e o logo.
- O texto "Feito por" segue a fonte, o tamanho e a cor dos outros textos do rodapé, sem sublinhado. O hover fica discreto (opacidade) e só em `(hover:hover) and (pointer:fine)`.

## Segurança e dados

- Nunca ler nem editar `.env`; os nomes das variáveis ficam em `.env.example`, sem valores reais.
- Segredo nunca vai para variável com prefixo público (`PUBLIC_`, `NEXT_PUBLIC_`, `VITE_`, `EXPO_PUBLIC_`).
- Nada de dado pessoal em log, URL, analytics ou commit.
- Nada secreto dentro do app: tudo que é empacotado pode ser extraído.
- Token e sessão só em armazenamento seguro (`expo-secure-store`, Keychain, Keystore).
- Regra de negócio sensível (preço, saldo, permissão) é decidida na API, nunca no app.
- Só HTTPS; deep links validam parâmetros e não executam ação sensível sem confirmação.
- Se há cadastro, existe exclusão de conta dentro do app; declarações de privacidade das lojas batem com o código.
- Preço, frete, desconto e total são calculados no servidor a partir do catálogo; valor vindo do app é só sugestão.
- Pedido só vira "pago" por webhook com assinatura validada mais consulta à API do provedor; a tela de retorno nunca confirma pagamento.
- Webhooks são idempotentes: o mesmo evento não duplica pedido, estoque nem mensagem.
- Cartão nunca passa pelo servidor do projeto (checkout ou tokenização do provedor).
- Toda leitura e escrita confere se o usuário logado pode acessar aquele registro; admin é conferido no servidor.
- Banco com RLS (ou regras equivalentes) em toda tabela exposta; chave de serviço só no servidor.
- Login, cadastro, recuperação de senha e criação de pagamento têm rate limit.
- LGPD: coleta mínima, finalidade clara, consentimento registrado quando for a base legal, canal para a pessoa pedir acesso, correção e exclusão.
- Menores de 18 anos: dados e imagens só com consentimento específico de pai, mãe ou responsável, registrado; nada público por padrão; coleta ainda menor.
- Páginas e telas com dados de menores ficam com `noindex` e prévia de link genérica (sem foto).
- Fotos sem EXIF e GPS; pedido de remoção atendido rápido.
- Localização: trajeto revela onde a pessoa mora. Zonas privadas escondem início e fim da corrida; perfil privado disponível; nunca mostrar a posição de alguém em tempo real; localização em segundo plano só com justificativa clara nas lojas.
- Ranking: antifraude (velocidade e aceleração plausíveis, GPS simulado, denúncia de corrida) fica no servidor; o app nunca decide posição, patente nem pontuação.

## Git

- Commits em Conventional Commits, em português (por exemplo `feat(pedido): adiciona resumo da sacola`).
- Não fazer commit nem push sem o usuário pedir.

## Escritório

- Ao fim de cada entrega, o pente-fino automático revisa as mudanças com os revisores e pede aprovação; correções só depois do "aplica".
- Só ajustes mecânicos (formatação, typo, import sem uso) são corrigidos sem perguntar.
- Achados que se repetem viram regra neste arquivo pela `/escritorio:retro`.
