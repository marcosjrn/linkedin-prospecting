# Prospecção LinkedIn com IA

Skill para **Claude Code** e **Codex** que encontra e qualifica leads do LinkedIn conversando com a IA, sem planilhas manuais e sem programar.

## O que a Skill faz

- Busca pessoas no LinkedIn por cargo, segmento e localização.
- Coleta os dados das empresas dessas pessoas (tamanho, descrição, site).
- Qualifica cada lead com base no seu cliente ideal: **Qualificado** ou **Não qualificado**, sempre com o motivo.
- Entrega tudo em uma planilha Excel (e, se você quiser, no Google Sheets).

A Skill **não envia mensagens** e não faz nenhum contato por você.

## O que você precisa

1. **Uma destas ferramentas** (planos pagos):
   - **Claude Code**: no app do Claude para computador (aba "Code") ou no terminal.
   - **Codex**: no app do ChatGPT para computador (opção "Codex"), no terminal ou na extensão do seu editor. O ChatGPT no navegador não carrega Skills.
2. **Conta na Apify** ([apify.com](https://apify.com)): é a plataforma que coleta os dados do LinkedIn. A própria Skill te guia na conexão, passo a passo.

## Quanto custa

A Skill é gratuita. As buscas são cobradas pela Apify, na sua conta. Valores aproximados no plano gratuito da Apify, com perfil completo e dados da empresa (consultados em outubro de 2026; podem mudar):

| Leads | Custo aproximado |
|---|---|
| 10 | US$ 0,18 |
| 100 | US$ 1,20 |

Antes de cada busca, a Skill mostra a estimativa e um limite máximo, e só começa depois da sua confirmação.

## Como instalar

Abra o Claude Code ou o Codex, cole este pedido e envie:

```
Instale ou atualize a Skill linkedin-prospecting a partir de https://github.com/marcosjrn/linkedin-prospecting. Baixe o repositório e copie a pasta linkedin-prospecting para a sua pasta de Skills pessoais (Claude Code: ~/.claude/skills/linkedin-prospecting; Codex: ~/.agents/skills/linkedin-prospecting), preservando a estrutura. Se houver versão anterior, faça backup. Preserve conexões, ICPs salvos e resultados existentes. Valide a instalação sem executar buscas pagas. Depois, inicie a Skill linkedin-prospecting e siga o fluxo de configuração apenas se necessário, com orientações simples e uma etapa por vez.
```

Aprove as permissões que aparecerem: a IA baixa os arquivos e os copia para a sua pasta de Skills.

Só na primeira vez, a IA vai:
- conectar sua conta Apify (no Codex, depois disso, abra uma conversa nova);
- preparar o que gera as planilhas Excel (se aparecer um pedido de permissão, é só aprovar);
- fazer 3 perguntas rápidas sobre o seu negócio e o seu cliente ideal.

<details>
<summary>Prefere baixar o arquivo?</summary>

Nesta página, clique em **Code › Download ZIP**. Depois, cole no Claude Code ou no Codex:

```
Instale ou atualize a Skill linkedin-prospecting a partir do arquivo linkedin-prospecting-main.zip que está na minha pasta Downloads. Descompacte e copie a pasta linkedin-prospecting para a sua pasta de Skills pessoais (Claude Code: ~/.claude/skills/linkedin-prospecting; Codex: ~/.agents/skills/linkedin-prospecting), preservando a estrutura. Se houver versão anterior, faça backup. Preserve conexões, ICPs salvos e resultados existentes. Valide a instalação sem executar buscas pagas. Depois, inicie a Skill linkedin-prospecting e siga o fluxo de configuração apenas se necessário, com orientações simples e uma etapa por vez.
```

</details>

## Como usar

- **Claude Code:** digite `/linkedin-prospecting`.
- **Codex:** digite `$linkedin-prospecting`. Se você instalou o plugin da Apify no Codex, chame a Skill sempre assim, para o Codex não usar outra.

Ou peça do seu jeito, por exemplo:

> Busque 20 CEOs de indústrias em Campinas.

A IA vai pedir o que faltar (cargo, segmento, localização e quantidade), mostrar o custo e aguardar sua confirmação.

## Dicas

- Comece com 10 a 20 leads para testar.
- Envie convites aos poucos e personalizados; mensagens em massa prejudicam sua conta.
- Para mudar seu cliente ideal, é só pedir: "quero atualizar meu ICP".
- Seus resultados ficam na pasta `prospeccao/` do projeto. Não compartilhe essa pasta: ela contém dados de pessoas. Use os dados com responsabilidade e respeite a LGPD.

## Para atualizar

Cole o mesmo pedido de instalação. Seu cliente ideal e sua conexão com a Apify são mantidos.

---

Criado por [Marcos Júnior](https://www.linkedin.com/in/marcos-j%C3%BAnior-537bba282/) · Licença [MIT](LICENSE)
