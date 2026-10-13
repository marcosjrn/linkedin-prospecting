# Google Sheets opcional

Só iniciar após escolha do usuário. Reutilizar qualified.json/Excel; falha de exportação não exige nova busca. Não exigir Sheets na configuração inicial.

## Escolher conexão

1. Descobrir ferramentas Sheets/Drive existentes e schemas. Usar conexão autenticada se permitir escrita e leitura de confirmação. Nome Google Drive não comprova escrita; upload/conversão de Excel serve se realmente suportado e confirmar planilha Sheets.
2. Sem conexão, em Claude com conectores disponíveis, orientar uma ação por vez em https://claude.ai/customize/connectors: conectar Google Sheets/Drive compatível, entrar e autorizar no navegador. Verificar ferramentas de escrita **neste Claude Code**; presença no Claude web não garante Code. Não declarar pronto só por login.
3. No Code sem escritor nativo, oferecer: “Podemos conectar o Google Sheets pelo Zapier. Ele usa sua conta Google e pode consumir a franquia do seu plano Zapier. Se preferir, o Excel já está disponível.” Só instalar serviço adicional se usuário escolher; consultar limites/preços vigentes se custo relevante.
4. No Codex, conectores do claude.ai não se aplicam: trocar `claude mcp add`/`claude mcp login` por `codex mcp add <nome> --url <url>` e `codex mcp login <nome>`, e abrir conversa nova para carregar as ferramentas.

## Zapier com OAuth

Guiar só ações necessárias, uma por vez; reutilizar conexão existente:
- Conta: https://zapier.com/ . Usuário criar/entrar no navegador se necessário.
- IA verificar CLI e configurar HTTP de usuário, preservando servidores:
  `claude mcp add --transport http --scope user zapier https://mcp.zapier.com/api/v1/connect`
- Iniciar `claude mcp login zapier` se suportado; alternativa `/mcp`, Zapier, autenticar. Usuário autoriza no navegador. Não pedir URL contendo token no chat.
- Descobrir ferramentas do servidor para habilitar/conectar Google Sheets usando schema real. Selecionar apenas ações Sheets necessárias e fornecer link Google gerado pelo serviço. Usuário só entra/autoriza. Não executar onboarding genérico que consulte e-mails ou demonstre outros apps.
- Sem configuração dinâmica, orientar https://mcp.zapier.com/ , selecionar servidor Claude, ferramentas Google Sheets e habilitar escrita/criação de planilha e leitura necessárias, conforme interface vigente. Conferir documentação antes de cliques se rótulos divergirem.
- Validar ferramentas lendo metadados da planilha de destino. Informar antes do primeiro uso que chamadas podem consumir franquia: documentação de 2026-10-09 indica duas tarefas por chamada bem-sucedida, sujeito ao plano. Não prometer gratuito/uma chamada.

Não exigir projeto Google Cloud, service account, credenciais OAuth manuais ou e-mail técnico no fluxo padrão.

## Exportar

Usar destino fornecido; sem destino, criar nova planilha se suportado. Se só adicionar linhas for possível, pedir apenas link da planilha. Conexão não autoriza alterar outras planilhas.

Mapear colunas humanas iguais ao Excel e conferir schema. Preferir escrita em lote. Planilha existente: ler cabeçalhos/URLs antes e adicionar apenas URLs ausentes, sem sobrescrever. Usar texto literal/RAW ou escape suportado; preservar todos os status.

Salvar ID, aba/range e progresso. Escrita incerta/timeout: ler linhas e reconciliar antes de repetir; não criar outra planilha por demora. Ler intervalo após escrita e conferir quantidade/URLs/status. Só afirmar concluída com evidência. Não publicar/alterar compartilhamento sem pedido.

Falha: manter Excel, explicar etapa pendente/escrita parcial e permitir retomar exportação. Não apresentar conexão documentada como integração testada.

## Fontes oficiais

Conferidas em 2026-10-09; consultar novamente se divergirem:
- https://support.claude.com/en/articles/10166901-use-google-workspace-connectors
- https://code.claude.com/docs/en/mcp
- https://github.com/zapier/zapier-mcp/blob/main/AGENTS.md
- https://docs.zapier.com/mcp/get-started/quickstart
- https://zapier.com/mcp/google-sheets
