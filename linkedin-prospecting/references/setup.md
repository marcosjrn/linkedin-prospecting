# Configuração inicial

Instruções internas: orientar uma ação por vez, não todo o procedimento. Detectar conexão antes de perguntar se usuário tem conta. Não executar Actor para testar.

## Claude Code

1. Descobrir ferramentas Apify. Se acessíveis, ler detalhes do Actor e pular configuração. Em conexão existente com erro, reparar apenas causa observada (autenticação, desabilitada, versão, indisponibilidade). Não remover servidor/credenciais por rotina.
2. Sem conexão, perguntar: “Você já tem uma conta na Apify?” Se não, orientar: “Abra [Criar conta na Apify](https://console.apify.com/sign-up), crie sua conta e volte aqui quando terminar.” Esperar ação antes da próxima. Login existente: https://console.apify.com/ . Não pedir senha ou garantir créditos gratuitos.
3. A IA verificar CLI/comandos disponíveis e configurar por conta própria, preservando outros servidores. Preferir escopo de usuário:
   `claude mcp add --transport http --scope user apify https://mcp.apify.com`
   Não repetir add se servidor existir; verificar endpoint e conflito de escopo. Se ambiente não permitir configuração, fornecer só ação/comando necessário, adequado ao sistema.
4. Iniciar OAuth com `claude mcp login apify`, se suportado. Orientar: “Na página que abrir, entre na sua conta Apify e autorize a conexão com o Claude.” Usuário autentica no navegador. Não pedir tokens, cookies do LinkedIn ou senha no chat. Se login não suportado, orientar `/mcp`, escolher Apify e autenticar. Usar URL gerada pelo fluxo; não inventar link OAuth.
5. Se ferramentas não atualizarem na sessão após configuração, orientar nova sessão no mesmo projeto, sem reinstalar. Verificar detalhes de Actor, chamada com limite de cobrança, acompanhamento de execução e leitura de dataset. Alguns clientes expõem ferramentas dinâmicas; consultar descoberta antes de concluir que faltam. Validar leitura de detalhes, sem executar Actor pago.
6. Só depois informar: “Apify conectada. Agora podemos preparar sua busca.” Retomar dados já fornecidos. Se saldo impedir operação, indicar conta para resolver; não adicionar créditos/contratar plano automaticamente.

## Codex (terminal, extensão de IDE ou app do ChatGPT para computador)

Não mandar comandos `claude` para usuário Codex.

1. Descobrir ferramentas Apify, como no passo 1 do Claude Code. Se o Codex oferecer instalar a dependência `apify` declarada em `agents/openai.yaml`, aceitar e ir ao passo 4.
2. Conta Apify: igual ao passo 2 do Claude Code.
3. A IA configurar por conta própria, preservando outros servidores em `~/.codex/config.toml`:
   `codex mcp add apify --url https://mcp.apify.com`
   Não repetir se `codex mcp list` já mostrar `apify`. Se o sandbox bloquear, pedir aprovação ao usuário. Sem CLI disponível (app para computador), usar o passo 6.
4. Iniciar OAuth com `codex mcp login apify`. Orientar: “Na página que abrir, entre na sua conta Apify e clique em Allow access.” Conferir autenticação em `codex mcp list`. Não pedir token no chat.
5. Ferramentas novas só aparecem em nova conversa: orientar abrir uma conversa nova no Codex e chamar `$linkedin-prospecting`. Validar leitura de detalhes do Actor, sem executar Actor pago.
6. Alternativa oficial da Apify, se o comando falhar ou no app: Plugins › menu ao lado de **+** › Add marketplace › `apify/apify-codex-plugin` › aba Personal › Add em Apify › Add to Codex › Install Apify › autorizar no navegador (no terminal: `/plugins` › Add Marketplace). O plugin traz Skills próprias de geração de leads; orientar chamar esta Skill sempre com `$linkedin-prospecting`.
7. Se OAuth falhar em ambiente sem navegador, o usuário pode definir `APIFY_TOKEN` antes de abrir o Codex, conforme a documentação da Apify; a IA nunca recebe o token pelo chat.
8. Só depois informar: “Apify conectada. Agora podemos preparar sua busca.”

ChatGPT na web e no celular não carrega Skills avulsas; orientar o usuário a usar o Codex.

## Fontes oficiais

Conferidas em 2026-10-13; consultar novamente se interface/comando divergir:
- https://docs.apify.com/mcp
- https://code.claude.com/docs/en/mcp
- https://learn.chatgpt.com/docs/build-skills
- https://developers.openai.com/codex/mcp
- https://docs.apify.com/integrations/codex-cli
- https://docs.apify.com/integrations/codex-app
- https://apify.com/harvestapi/linkedin-profile-search
- https://apify.com/harvestapi/linkedin-company
- https://apify.com/pricing

Instalação da Skill não concede acesso à conta Apify. Configuração salva não comprova autenticação.
