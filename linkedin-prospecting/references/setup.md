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

## Ambiente do Excel (Claude Code e Codex)

Preparar na instalação ou no primeiro uso, antes da primeira busca paga. O usuário não precisa saber o que é Python: não pedir que instale, configure ou programe.

1. Se `excel_python` do state.json existir e `<excel_python> -c "import openpyxl"` funcionar, pular o resto.
2. Procurar Python 3.9+ que realmente execute: `python3`, `python` ou `py -3` com `-c "import sys; print(sys.executable)"`. No Windows, `python` pode ser atalho da Microsoft Store que não executa; só vale se imprimir o caminho. No macOS, `/usr/bin/python3` sem as ferramentas da Apple abre janela de instalação; tratar como ausente.
3. Sem Python, avisar em uma linha e instalar pelo canal oficial do sistema, no escopo do usuário:
   > Vou instalar o Python (gratuito), que gera suas planilhas Excel. Se aparecer um pedido de permissão, é só aprovar.
   - Windows: `winget install -e --id Python.Python.3.14 --scope user --silent --accept-package-agreements --accept-source-agreements` (ou versão 3 estável mais recente do winget; se o escopo não for aceito, repetir sem `--scope`).
   - macOS: com Homebrew, `brew install python`; sem Homebrew, `xcode-select --install` e orientar: "Na janela da Apple, clique em Instalar e me avise quando terminar. Pode levar alguns minutos."
   - Linux: usar python3 do sistema; se faltar, mostrar só o comando do gerenciador de pacotes, pois exige senha.
   A sessão pode não enxergar o PATH novo: localizar o executável instalado (Windows: `py -3` ou `%LOCALAPPDATA%\Programs\Python\Python3*\python.exe`) em vez de pedir reinício.
4. Criar ambiente isolado `venv/` na mesma pasta do state.json (conversation.md), nunca na pasta da Skill, e instalar só `openpyxl`. Reutilizar se já existir. Executável: `venv/Scripts/python.exe` (Windows) ou `venv/bin/python` (macOS/Linux).
5. Validar `import openpyxl` e salvar o caminho em `excel_python` no state.json, preservando as outras chaves.
6. Se falhar (sem winget, permissão negada, rede bloqueada), não travar: seguir com configuração e busca, avisar em uma frase que a planilha será gerada depois e preservar os dados. Nunca pedir que o usuário edite PATH ou rode comandos técnicos.

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
