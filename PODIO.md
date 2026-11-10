# Pódio — briefing do projeto

> Documento-guia para o próximo chat. Leia inteiro antes de agir.
> Origem: conversa de descoberta com o Jhonatan em 10/11/2026 (ideia, pesquisa de mercado e escolha do nome).
> Status: **ideia validada no papel, nada de código ainda.** A pasta do projeto ainda não é um repositório git.

---

## 1. Seu papel neste projeto

Você é **sócio de produto e engenheiro** do Pódio, não só executor.

- **Opine deliberadamente.** Discorde quando algo não fizer sentido, proponha caminhos melhores e diga quando uma ideia não compensa. O Jhonatan pediu isso explicitamente.
- **Traga uma ideia fora da caixa** (seção 7) que torne o app muito viral **e** viável de construir.
- Siga as instruções globais do Jhonatan: responder em **português do Brasil**, explicar o motivo das decisões em poucas linhas, **não fazer commit nem push sem ele pedir**, imagens via Gemini/agy conforme o CLAUDE.md global.
- O Jhonatan ainda está entendendo o produto. Explique conceitos novos (ex.: "loop viral", "segmento", "cold start") com um exemplo concreto antes de usá-los.

---

## 2. A ideia (nas palavras do produto)

**Pódio** é um app de corrida que transforma as ruas da cidade numa disputa por ranking.

| Mecânica | Como funciona |
|---|---|
| **Dono do trecho** | O app grava o trajeto. Quem faz o melhor pace num trecho vira o nº 1 dali. Outros corredores podem ir lá e tomar o posto. |
| **Rankings por período** | Disputa de colocação **semanal, mensal e anual**, mais o **recorde histórico** de cada trecho. |
| **Grupos (clãs)** | Grupos de corrida com membros, histórico das corridas do grupo e perfil do grupo. |
| **Guerra de grupos** | Competição entre grupos, no estilo "guerra de clãs do Clash of Clans" adaptada para corrida. O objetivo é manter as pessoas correndo. Os confrontos são equilibrados pela quantidade de membros e pela patente de cada um. Cada membro corre o máximo que consegue dentro da própria patente. |
| **Patente** | Cerca de 5 corridas de classificação calculam as médias do corredor (pace, tempo, distância, etc.) e definem a patente (ex.: Bronze, Prata, Ouro, Platina, Diamante). A pessoa sobe conforme evolui. |
| **Compartilhamento** | Ao subir de patente ou conquistar um trecho, o app gera um card para postar nas redes. **Esse é o principal motor de crescimento** planejado para o lançamento. |
| **Perfil personalizável** | Fotos das corridas, melhor pace, locais que domina (trechos com recorde), patente atual. |
| **Mascote** | Mascote favorito do usuário, que será criado com o tempo. Versão paga: mascote personalizado do grupo. |

---

## 3. Mercado: o que já existe (pesquisado em 10/11/2026)

**Conclusão:** cada peça já existe em algum app, mas **nenhum junta tudo**. O valor está na combinação e, principalmente, na patente usada como **equalizador** (seção 4).

| Peça | Quem já faz | Observação |
|---|---|---|
| Dono do trecho por tempo | **Strava**: segmentos com a coroa de mais rápido (KOM/QOM) e o **Local Legend**, para quem mais correu no trecho em 90 dias | O 1º lugar costuma ser de atleta de elite ou de quem gravou de bike. O corredor comum desiste de competir. |
| Conquista de território | **INTVL, Konquo, KYRO, Turf, Run An Empire, Motera, Running Empire** | Correr em circuito fechado "pinta" uma área no mapa. O Konquo tem clubes e o plano Konquo+ (4,99 €/mês). |
| Guerra de clãs de corrida | **ClashRun** (Brasil) | Liga de equipes, raids 5x5, arena 1x1, Season Pass. **Ainda não lançou** ("app em desenvolvimento"). É o concorrente mais direto. |
| Patente / tiers | **KYRO** (13 níveis, de Iron a Legend), **PaceOff** (Brasil, duelos 1x1 por GPS, de Iniciante a Lendário, Premium R$19,90/mês) | Os tiers são de XP ou progressão, não de capacidade real. |
| Ranking por bairro | **Run Rank**: vaga de freelancer no Workana para desenvolver um app de "social racing" com ranking por bairro e cidade | Sinal de que tem gente construindo algo parecido agora. **Velocidade importa.** |

---

## 4. Diferenciais do Pódio

1. **Patente como equalizador.** Cada trecho tem o **rei geral** e também o **rei de cada patente** (rei Bronze, rei Prata...). O iniciante consegue ganhar alguma coisa perto de casa e tem motivo para postar.
2. **Guerra de clãs justa.** No confronto entre grupos, cada membro pontua pela **melhora em relação à própria patente**, não pelo pace bruto. Um grupo de iniciantes esforçados pode vencer um grupo de corredores rápidos e acomodados. O pareamento dos grupos leva em conta o número de membros e a soma das patentes, como no Clash.
3. **Feito para o Brasil.** Corrida de rua em alta, grupos e assessorias de corrida respondendo por boa parte dos inscritos em provas, linguagem e cards pensados para o Instagram brasileiro.
4. **Compartilhamento como produto, não como botão.** O card de "subi de patente" e o de "novo rei do trecho" são features centrais, com o capricho visual de um Spotify Wrapped.

---

## 5. Pontos que podem não compensar: ataque e resolva

Para cada ponto, entregue: **(a)** a solução proposta, **(b)** o custo e a complexidade de implementar, **(c)** o que entra no MVP e o que fica para depois.

1. **Fraude.** Quando o ranking vale status, aparece gente gravando de bike, de carro ou com GPS falso, e um ranking contaminado perde a credibilidade.
   - Pistas: limite de velocidade e aceleração plausíveis, variação de pace, cadência ou passos pelo acelerômetro/HealthKit, detecção de GPS simulado (mock location no Android), saltos de posição, botão "denunciar corrida", revisão do top 3 de cada trecho.
2. **Começo vazio (cold start).** Ranking sem gente não tem graça.
   - Pistas: lançar **numa cidade só**, entrar pelos **grupos e assessorias de corrida** (também clientes pagantes em potencial), pré-popular trechos famosos (parques, orlas), ranking que já faz sentido com poucos corredores.
3. **"O mesmo trajeto" é tecnicamente difícil.** Comparar trajetos livres é complexo.
   - Pistas: começar com **trechos fixos** (segmentos com início, fim e tolerância), criados a partir das ruas e parques mais corridos ou pelos próprios usuários com regras mínimas. Matching com PostGIS. Deixar a conquista de área livre para depois.
4. **O corredor já usa Garmin, Apple Watch ou Strava.** Exigir gravação no Pódio é atrito.
   - Pistas: importar de Apple Health, Health Connect e Garmin. **Atenção:** a API do Strava mudou em 2024 e, até onde sabemos, proíbe mostrar dados de um usuário para outros, o que inviabiliza ranking com dados do Strava. **Confirme os termos atuais antes de contar com isso.** Defina se corrida importada vale para o ranking ou só a gravada no app (antifraude).
5. **Patente justa.** Pace puro engana: 5 km e 21 km não se comparam, subida pesa, calor pesa.
   - Pistas: desempenho equivalente (VDOT de Daniels ou fórmula de Riegel, T2 = T1 × (D2/D1)^1,06), correção por altimetria, 5 corridas de classificação com distância mínima, recalibração periódica e regra para não "afundar" a patente de propósito (smurf).
6. **Privacidade e LGPD.** Trajetos revelam onde a pessoa mora. Localização é dado pessoal e menores de idade exigem cuidado.
   - Pistas: zonas privadas que escondem início e fim, perfil privado, consentimento claro, idade mínima, direito de apagar os dados.
7. **Segurança física.** Incentivar pace máximo em rua aberta tem risco (trânsito, horário, assédio).
   - Pistas: trechos preferencialmente em parques e ciclovias, avisos, não mostrar em tempo real onde a pessoa está.
8. **Bateria e GPS em segundo plano.** O app precisa gravar com a tela apagada sem drenar a bateria, e as lojas exigem justificativa para localização em background.

---

## 6. MVP (primeira versão)

**Objetivo:** provar que as pessoas **disputam trechos e compartilham as conquistas** numa cidade.

**Entra:**
- Cadastro, login e perfil básico (foto, patente, melhor pace, trechos dominados).
- Gravação de corrida por GPS, funcionando em segundo plano.
- Trechos fixos numa cidade piloto.
- Ranking por trecho: rei geral e rei por patente, com filtros de **semana, mês, ano e recorde histórico**.
- 5 corridas de classificação e cálculo da patente.
- Grupos com membros e **uma guerra semanal entre grupos**.
- Cards compartilháveis: "subi de patente", "sou o novo rei do trecho" e "meu grupo venceu a guerra".
- Notificação "você perdeu o 1º lugar no trecho X".
- Antifraude básico e zonas privadas.

**Fica para depois:** mascote, mascote pago do grupo, plano pago, fotos de corridas no perfil, conquista de área livre, integrações com relógios, rede social completa.

**Stack sugerida (opine):** Expo / React Native, para iOS e Android num só código, com `expo-location` e `TaskManager` para GPS em background. Supabase (Postgres + **PostGIS** para geometria dos trechos, Auth, Storage, RLS). Geração do card como imagem no app ou numa edge function. Se discordar, justifique.

---

## 7. Desafio aberto: a ideia fora da caixa

O Jhonatan pensou numa **mini rede social dentro do app**. Ele gostou da ideia, mas ainda não sabe bem o que seria. Sua tarefa:

1. **Avalie com honestidade** se uma mini rede social faz sentido, e em que formato. Feed genérico de fotos compete com o Instagram e costuma morrer vazio. Um feed **só de acontecimentos da disputa** pode ser outra história: "Fulano tomou seu trecho", "Seu grupo está perdendo a guerra por 3 pontos", "Novo recorde na orla".
2. **Proponha pelo menos 3 ideias ousadas** que torne o Pódio muito viral, explicando:
   - por que as pessoas compartilhariam (o loop viral: ação → card ou convite → novo usuário),
   - por que é **viável** para uma equipe pequena no MVP ou logo depois,
   - como ela se conecta com trecho, patente e grupo, sem virar um app diferente.
3. Pense também em **monetização** que não estrague a competição. Nada de pagar para ganhar ranking. Algumas pistas: plano para assessorias, Season Pass, mascote do grupo, visual do card.

Pode ser criativo de verdade. O critério é: **viral, viável e alinhado com o objetivo do app (fazer as pessoas continuarem correndo).**

---

## 8. Decisões em aberto

- Nomes das patentes: metais (Bronze → Diamante → Lenda?) ou outro tema próprio do Pódio.
- Quantas patentes e quantos trechos na cidade piloto.
- Qual cidade piloto.
- Regras exatas da guerra entre grupos (duração, pareamento, pontuação, tamanho mínimo de grupo).
- Slogan. Candidato: "Seja o dono da rua."
- Registro da marca: "Pódio" é palavra comum. Provavelmente será marca mista (nome + logo) ou uma variação. Verificar no INPI (classes 9 e 41), no registro.br e nos @ das redes.

---

## 9. Como trabalhar: loop do agente e economia de tokens

### Loop de trabalho
1. **Entender:** leia este arquivo. Pergunte só o que for decisão do Jhonatan (use AskUserQuestion com opções, não perguntas abertas).
2. **Planejar:** antes de escrever código, use **EnterPlanMode** para apresentar o plano e só siga após a aprovação.
3. **Executar:** em fatias pequenas e testáveis (ex.: gravar GPS → salvar corrida → casar com o trecho → ranking).
4. **Verificar:** rode o app, os testes e o lint. Use a skill **run** para ver funcionando. Não declare pronto sem verificar.
5. **Registrar:** atualize **este arquivo** (decisões da seção 8, status) e use **escritorio:passagem** ao encerrar a sessão, para o próximo chat continuar sem reler a conversa.

### Ferramentas do harness e quando usar
| Ferramenta | Use para |
|---|---|
| **WebSearch** | Modo `standard` por padrão. `extended` só para dado recente ou difícil (termos de API, preços, concorrentes novos). Faça as buscas em paralelo numa única resposta. |
| **Agent → web-fetch** | Ler páginas específicas (termos da API do Strava, Health Connect, regras das lojas). Peça o **resumo da resposta**, não a página. |
| **Agent → Explore / Plan** | Explorar várias partes do código ou desenhar a arquitetura quando o projeto crescer. |
| **Agent → ajudante-rapido** | Tarefas mecânicas em muitos arquivos (renomear, trocar import, padronizar). |
| **Artifact** | Protótipo visual das telas e dos **cards compartilháveis** para o Jhonatan ver e opinar antes do código. Carregue a skill `artifact-design` antes. |
| **agy (Gemini)** | Mascote, ícones e imagens, conforme o fluxo do CLAUDE.md global. **Exige repositório git:** peça ao Jhonatan para rodar `git init` antes. |
| **escritorio:pente-fino** | Revisão antes de cada entrega. Os auditores relevantes aqui são **auditor-mobile** (app), **auditor-dados** (localização, LGPD, RLS) e, quando houver plano pago, **auditor-pagamentos**. |
| **escritorio:passagem** | Salvar onde parou ao fim de cada sessão. |
| **Workflow** (multiagente) | **Só se o Jhonatan pedir explicitamente.** É caro. |

### Economia de tokens sem perder criatividade
- **Este arquivo é a memória do projeto.** Atualize-o em vez de reexplicar ou rederivar decisões.
- Use Grep e Glob antes de Read. Leia trechos com `offset` e `limit`, não arquivos inteiros sem necessidade. Não releia arquivo que acabou de editar.
- Faça chamadas independentes **em paralelo** numa única resposta.
- Subagente só para trabalho paralelo de verdade ou pesquisa ampla. Uma busca que você mesmo resolve em 2 ou 3 chamadas não precisa de subagente.
- Gaste tokens onde importa: **pensar o produto, as regras do jogo e a ideia viral**. Economize no mecânico: boilerplate, leituras repetidas, dumps de página.
- Respostas ao Jhonatan: diretas, com recomendação clara em vez de uma lista enorme de opções.

---

## 10. Primeira resposta esperada no próximo chat

1. Sua **opinião sincera** sobre o Pódio como está.
2. **Solução proposta para cada ponto da seção 5**, de forma resumida.
3. **A ideia fora da caixa** (seção 7) e sua avaliação da mini rede social.
4. **Sistema de patente e pontuação da guerra de grupos** em rascunho.
5. **Proposta de próximos passos** (ex.: protótipo das telas e dos cards como Artifact → `git init` → setup do projeto Expo + Supabase).

---

## Fontes da pesquisa
- ClashRun: https://clashrun.com.br/
- PaceOff: https://paceoff.app/
- Konquo (comparação de apps de território 2026): https://konquo.com/en/territory-capture-apps
- Motera (apps de corrida gamificados): https://www.motera.app/best-gamified-running-app
- Running Empire: https://running-empire.com/en/
- Strava Local Legend: https://www.bikeradar.com/news/strava-local-legend-worldwide-release/
- Vaga Run Rank (Workana): https://www.workana.com/job/desenvolvedor-react-native-expo-para-aplicativo-mobile-de-social-racing-run-rank
- RunLab: https://runlab.com.br/
