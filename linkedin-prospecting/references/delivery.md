# Excel e dados de saída

Usar contrato em contracts.md com envelope `{"metadata":{...},"leads":[...]}`. Uma linha por pessoa; vínculos simultâneos em evidências. Deduplicar antes de exportar.

Lista: nome, URL LinkedIn, cargo, empresa/URL validada, localização pessoal, faixa de funcionários, contagem complementar LinkedIn, status (QUALIFICADO ou NÃO QUALIFICADO), justificativa, evidência no segmento (como agência quando pedido), preferência/B2B quando relevante, informações ausentes e alertas.

Preencher `qualification.segment_evidence` e `qualification.preference_evidence` com campos/trechos suficientes. Manter avaliações em required_checks/preferred_checks. Sem preferência, indicar “Não solicitado”, sem penalizar. Ausência não é zero.

Executar `<excel_python> <pasta-da-skill>/scripts/export_xlsx.py <qualified.json> <leads.xlsx>`, com o Python do ambiente preparado em setup.md (Ambiente do Excel). Se `excel_python` faltar ou falhar, preparar o ambiente nesse momento, conforme permissões, sem pedir ao usuário que programe e sem nova cobrança. Não renomear CSV para xlsx. Geração bloqueada: informar falha e entregar alternativa claramente identificada, preservando dados para gerar Excel depois.

Script gera Leads, Resumo, Evidências e Auditoria oculta (sem segredos). Conferir abertura, contagem, soma dos status, ordenação e URLs. Os dois status ficam no arquivo; o script rejeita qualquer outro status. Textos coletados devem ser literais, sem execução de fórmulas. Faixa/contagem são dados LinkedIn, não total auditado de funcionários.

Metadados: requested_profiles, found_profiles (brutos), duplicates_removed, companies_resolved, actual_cost_usd (null se qualquer etapa cobrada estiver indisponível), estimated_cost_usd, total_budget_usd, limitations, ICP/filtros/provenance. Não preencher custo desconhecido com zero nem chamar soma parcial de custo total. Valores monetários devem ser numéricos. Guardar JSON completo no registro.

Entregar arquivo e resumo curto de encontrados/únicos, quantidades por status, custo reportado/indisponível e limitação material. Sem resultados, gerar Excel com cabeçalhos. Salvar/apresentar conforme regras do ambiente. Não declarar pronto sem verificar arquivo.
