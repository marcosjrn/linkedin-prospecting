# Contratos

Consultar schema vigente pelo MCP. Exemplos são referência do teste de outubro/2026, não contrato/preço permanente.

## ICP

```json
{
  "requested_profiles": 10,
  "total_budget_usd": 1,
  "search_filters": {
    "current_job_titles": ["Founder", "Co-Founder", "Owner"],
    "person_locations": ["United States"],
    "industries": ["Advertising Services", "Marketing Services"],
    "company_size": {"min": 1, "max": 50}
  },
  "required_criteria": ["cargo atual de fundador/proprietário", "pessoa nos EUA", "serviços de marketing", "empresa de 1–50 funcionários"],
  "preferred_criteria": ["atende empresas cujo mercado é B2B"],
  "exclusion_criteria": [],
  "organization_scope": {
    "accepted": ["agências de marketing"],
    "excluded": [],
    "unresolved": ["agências exclusivamente de PR", "consultorias", "fornecedores promocionais"]
  }
}
```

Este ICP é exemplo histórico, não configuração padrão. Não exigir faixa, B2B, orçamento como campo do formulário ou decisão sobre subtipos de agência. Aceitar outros ICPs; julgar casos sem evidência por qualification.md (sem base razoável: NÃO QUALIFICADO), sem interrogatório de escopo.

## Profile Search

Tradução do pedido, filtros, IDs de setor e exemplos: [search-input.md](search-input.md).
Faixas fixas nem sempre representam intervalo exato: 5–50 com B/C inclui 1–4. Registrar busca ampla e validar; faixa 2–10 apenas sobrepõe 5–50.
Full contém `firstName`, `lastName`, `linkedinUrl`, `headline`, `about`, `location`, `industry`, `currentPosition` e `experience` (arrays). Schema inferido pode representar outro modo; usar retorno real.

## Company Details

Input: `{"companies":["https://www.linkedin.com/company/empresa-validada/"],"searches":["Nome sem URL válida"]}`.
Output: `id`, `linkedinUrl`, `name`, `originalQuery`, `website`, `description`, `tagline`, `specialities`, `industries`, `locations`, `employeeCount`, `employeeCountRange.start/end`, `foundedOn.year` (ajuda a comprovar fundador).
`originalQuery` ajuda mapear busca por nome, mas não comprova identidade. Ausente não equivale a zero.

## Execução e preço

`call-actor({actor,input,callOptions:{maxTotalChargeUsd:subteto},waitSecs:30})` retorna IDs/status, não linhas. Acompanhar com `get-actor-run` e ler com `get-dataset-items`. Seguir schema descoberto se mudar. Limite PPE não substitui limite de trabalho no input.

Preço consultado FREE/BRONZE: US$ 0,10/página de até 25 pessoas + US$ 0,004/perfil Full. Company Details US$ 0,004/empresa + início US$ 0,00005/GB, mínimo um evento. Consultar novamente antes de estimar.

## Saída JSON

Envelope de entrega: {"metadata":{...},"leads":[...]}. Um registro por pessoa única, incluindo todos os status. Vínculos adicionais devem ficar nas evidências, sem duplicar pessoa:

```json
{
  "person":{"name":"","linkedin_url":"","current_title":"","location":""},
  "company":{
    "name":"","linkedin_url":null,"id":null,
    "identity_status":"CONFIRMADA|NAO_RESOLVIDA|AMBIGUA",
    "employee_range":{"min":null,"max":null},
    "linkedin_employee_count":null,
    "size_status":"ATENDE|NAO_ATENDE|NAO_CONFIRMADO",
    "data_warnings":[]
  },
  "qualification":{
    "status":"QUALIFICADO|NAO_QUALIFICADO",
    "reason":"", "segment_evidence":"", "preference_evidence":"",
    "required_checks":[{"criterion":"","result":"ATENDE|NAO_ATENDE|NAO_CONFIRMADO","source_field":"","evidence":""}],
    "preferred_checks":[],"missing_information":[]
  },
  "provenance":{
    "profile_run_id":"","profile_dataset_id":"",
    "company_run_id":"","company_dataset_id":"","retrieved_at":""
  }
}
```

Acrescentar metadados gerais separados: ICP, inputs/filtros, orçamento/subtetos, custo real nullable e estimativa identificada. Não inventar data de scrape; retrieved_at é data de leitura.
