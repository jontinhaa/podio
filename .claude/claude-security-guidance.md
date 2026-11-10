# Regras de segurança do projeto

Contexto: sites e sistemas web de pequenos negócios no Brasil (Astro, TypeScript), feitos por um desenvolvedor solo. Além do que você já procura, trate como achado:

Segredos
- Chave, token ou senha em código, teste, comentário ou arquivo versionado. Só `.env.example`, sem valores reais, é versionado.
- Segredo em variável com prefixo público (`PUBLIC_`, `NEXT_PUBLIC_`, `VITE_`, `EXPO_PUBLIC_`): ela vai parar no navegador ou no app.

Navegador
- HTML vindo de usuário, URL ou API em `innerHTML`, `outerHTML`, `set:html`, `dangerouslySetInnerHTML` ou `v-html` sem sanitização.
- Script de terceiro sem necessidade clara, ou carregado de CDN sem `integrity`.
- Dado pessoal (nome, telefone, e-mail, CPF, endereço) em URL, query string, analytics, `console.log` ou guardado no `localStorage` sem prazo.

Servidor e rotas
- Rota ou função de servidor sem validação de entrada por schema, sem limite de tamanho do corpo ou sem rate limit quando cria, envia ou cobra algo.
- CORS `*` em rota com efeito; erro que devolve stack, token ou resposta crua de provedor.
- Redirecionamento para URL vinda do usuário sem lista de destinos permitidos.

Configuração e cadeia de suprimentos
- Deploy sem os cabeçalhos Content-Security-Policy, Strict-Transport-Security, X-Content-Type-Options, Referrer-Policy, Permissions-Policy e frame-ancestors.
- Dependência nova desconhecida, com nome parecido com o de pacote famoso, ou com script de instalação estranho.
- Workflow do GitHub com `pull_request_target`, permissões amplas ou segredo impresso em log.

# Sala mobile

- Segredo dentro do app: `EXPO_PUBLIC_*`, `extra` do app.config, constante no código ou arquivo empacotado. Tudo que vai no app pode ser extraído.
- Token ou sessão em AsyncStorage, SharedPreferences ou arquivo comum, em vez de `expo-secure-store`, Keychain, Keystore ou `flutter_secure_storage`.
- Tráfego sem HTTPS (`usesCleartextTraffic`, `NSAllowsArbitraryLoads`) sem justificativa documentada.
- Regra de negócio sensível (preço, saldo, permissão) decidida no app em vez da API.
- Deep link que executa ação sensível sem confirmação ou sem validar os parâmetros.
- WebView com `originWhitelist` aberta, JavaScript injetado com dado externo ou sessão carregada em URL arbitrária.
- Permissão pedida sem uso ou sem texto explicando o motivo.
- Build de produção com logs verbosos, menu de debug ou endpoints de teste.
- Atualização OTA fora do canal oficial, ou código baixado e executado em tempo real.
- App com cadastro sem exclusão de conta dentro do app; declarações de privacidade das lojas diferentes do que o código faz.

# Sala do cofre: dinheiro, login e dados pessoais

Pagamentos
- Preço, frete, desconto ou total aceitos do navegador. O servidor recalcula tudo a partir do catálogo; quantidade é inteiro positivo com limite; dinheiro em centavos inteiros, nunca float.
- Pedido marcado como pago pela página de retorno ou por webhook sem assinatura validada. Exija assinatura e consulta à API do provedor antes de liberar o pedido.
- Mercado Pago: header `x-signature` validado com HMAC-SHA256 sobre `id:<data.id>;request-id:<x-request-id>;ts:<ts>;` e comparação em tempo constante; `X-Idempotency-Key` ao criar pagamento.
- Stripe: `stripe.webhooks.constructEvent` com o corpo bruto da requisição.
- Webhook sem idempotência (o mesmo evento duplica pedido, estoque ou mensagem); valor ou moeda pagos sem conferência com o pedido.
- Número de cartão ou CVV passando pelo servidor do projeto; use o checkout ou a tokenização do provedor.
- Access token de provedor fora do servidor ou em variável pública.

Login e permissões
- Senha sem argon2id ou bcrypt; login caseiro quando um provedor pronto resolveria.
- Cookie de sessão sem `HttpOnly`, `Secure` e `SameSite`; sessão sem expiração; logout que não invalida no servidor.
- Login, cadastro e recuperação de senha sem rate limit, ou com mensagem que revela se o e-mail existe.
- Rota ou ação de admin que confere permissão só no front-end.
- Registro buscado pelo id sem conferir se pertence ao usuário logado (IDOR).
- Supabase: tabela exposta sem RLS, política sem `auth.uid()`, `service_role` fora do servidor. Firebase: regra com `if true`.
- Sistema com vários clientes: consulta sem filtro pelo cliente do usuário logado.

Dados pessoais (LGPD)
- Coleta além do necessário para a finalidade; consentimento não registrado quando ele for a base legal.
- Dados ou imagens de menores de 18 anos sem consentimento específico de pai, mãe ou responsável, ou públicos por padrão.
- Upload sem validar tipo e tamanho no servidor, em bucket público, ou foto de pessoa sem remover EXIF e GPS.
- Nenhum caminho para a pessoa pedir acesso, correção ou exclusão dos próprios dados.

Este projeto trata dados de menores: qualquer dado ou imagem de menor exige consentimento específico de pai, mãe ou responsável e fica fora do público por padrão.
