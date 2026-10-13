# Do pedido ao input dos Actors

Traduzir internamente; nunca mostrar JSON ao usuário. Conferir o schema vigente pelo MCP antes de chamar; se divergir deste guia, seguir o schema.

## Profile Search: base fixa

```json
{"profileScraperMode":"Full","maxItems":N,"startPage":1,"takePages":ceil(N/25),"autoQuerySegmentation":false}
```

Nunca usar `Full + email search`, campos de MongoDB nem deduplicação externa. `autoQuerySegmentation` só quando o usuário pedir mais perfis do que a busca entrega e aceitar nova estimativa.

## Mapeamento

Filtros de tipos diferentes se somam (E); valores dentro de um mesmo filtro se alternam (OU). Usar o mínimo de filtros que traduz o pedido; critério subjetivo (B2B, aderência ao ICP) fica para a qualificação.

| Pedido no chat | Campo | Regra |
|---|---|---|
| Cargo específico | `currentJobTitles` | 2 a 6 variantes do mesmo cargo, em PT e EN, masculino/feminino quando mudar a grafia. Ex.: Founder, Co-Founder, Fundador, Cofundador. Não misturar níveis diferentes sem pedido. |
| "Donos", "sócios", "decisores", "C-level" | `seniorityLevelIds` | Usar em vez de títulos: 320 Owner/Partner, 310 CXO, 300 VP, 220 Director. "Donos" = 320; "decisores" = 320, 310, 300 e 220. |
| Área sem cargo ("pessoas de marketing") | `functionIds` + `seniorityLevelIds` | 15 Marketing, 25 Sales, 4 Business Development, 13 Information Technology, 12 Human Resources, 10 Finance, 18 Operations, 9 Entrepreneurship. |
| Segmento que é setor do LinkedIn | `industryIds` | Tabela abaixo, 1 a 5 IDs como texto, incluindo pai e filhos relevantes. |
| Nicho que não é setor (SaaS, e-commerce, franquias, clínicas odontológicas) | `searchQuery` | 1 a 3 termos, com `OR` e aspas quando útil: `"e-commerce" OR "loja virtual"`. Combinar com `industryIds` só se ambos forem claros. |
| B2B, porte de cliente, "empresas que vendem para empresas" | nenhum | Não existe filtro; buscar sem ele e qualificar depois. |
| Onde a pessoa está | `locations` | Formato do LinkedIn, país em inglês: `Ribeirão Preto, São Paulo, Brazil`; estado: `São Paulo, Brazil`; país: `Brazil`. Várias cidades no mesmo array. Nunca siglas soltas (“UK” vira Ukraine; “SP” é ambíguo). |
| "Interior de SP" e similares | `locations` + `excludeLocations` | Estado em `locations` e capital em `excludeLocations`. |
| Onde fica a empresa ("empresas de Curitiba") | `companyHeadquarterLocations` | Mesmo formato; não confundir com `locations`. |
| Tamanho da empresa | `companyHeadcount` | A Self-employed, B 1–10, C 11–50, D 51–200, E 201–500, F 501–1.000, G 1.001–5.000, H 5.001–10.000, I 10.001+. Cobrir a faixa pedida; fronteira fora da letra é validada na qualificação (“mais de 30” = C a I). Pedido de empresa com equipe exclui A. |
| Empresas específicas | `currentCompanies` | URLs `https://www.linkedin.com/company/...`. |
| Exclusão explícita | `excludeCurrentJobTitles`, `excludeIndustryIds`, `excludeLocations` | Só o que o usuário excluiu. |
| "Ativos no LinkedIn" / "trocaram de emprego" | `recentlyPostedOnLinkedIn` / `recentlyChangedJobs` | `true` só quando pedido. |
| Idioma do perfil | `profileLanguages` | Só quando pedido. |

`industryIds` filtra o setor declarado no perfil da pessoa, que pode diferir do setor da empresa; por isso a qualificação sempre confere a empresa. `currentJobTitles` também é aproximado (o LinkedIn padroniza cargos) e pode trazer títulos vizinhos, como "Sócio proprietário".

## Setores (IDs conferidos em 2026-10-13)

| Segmento | IDs |
|---|---|
| Software, SaaS, startups de tecnologia | 4 Software Development; 6 Technology, Information and Internet; 2458 Data Infrastructure and Analytics; 1285 Internet Marketplace Platforms |
| TI, consultoria de TI, cibersegurança | 96 IT Services and IT Consulting; 118 Computer and Network Security |
| Agências de marketing e publicidade | 80 Advertising Services; 1862 Marketing Services; 98 Public Relations and Communications Services; 97 Market Research |
| Design | 99 Design Services; 140 Graphic Design |
| Consultoria empresarial | 11 Business Consulting and Services; 102 Strategic Management Services |
| RH e recrutamento | 137 Human Resources Services; 104 Staffing and Recruiting; 1923 Executive Search Services |
| Contabilidade | 47 Accounting |
| Advocacia e jurídico | 9 Law Practice; 10 Legal Services |
| Engenharia e arquitetura | 3242 Engineering Services; 50 Architecture and Planning; 51 Civil Engineering |
| Construção | 48 Construction; 51 Civil Engineering |
| Imobiliárias | 44 Real Estate |
| Serviços financeiros e fintechs | 43 Financial Services; 1673 Credit Intermediation; 41 Banking; 46 Investment Management |
| Seguros e corretoras | 42 Insurance; 1737 Insurance Agencies and Brokerages |
| Fundos e investidores | 106 Venture Capital and Private Equity Principals |
| Saúde, hospitais e clínicas | 14 Hospitals and Health Care; 13 Medical Practices; 2045 Dentists; 139 Mental Health Care |
| Academias e bem-estar | 124 Wellness and Fitness Services |
| Veterinária | 16 Veterinary Services |
| Farmacêutica e equipamentos médicos | 15 Pharmaceutical Manufacturing; 17 Medical Equipment Manufacturing |
| Indústria em geral | 25 Manufacturing; 55 Machinery Manufacturing; 135 Industrial Machinery Manufacturing; 3216 Industrial Automation; 24 Computers and Electronics Manufacturing |
| Indústria de alimentos e bebidas | 23 Food and Beverage Manufacturing |
| Química, plásticos, têxtil, automotiva | 54 Chemical Manufacturing; 117 Plastics Manufacturing; 60 Textile Manufacturing; 53 Motor Vehicle Manufacturing |
| Agronegócio | 63 Farming; 23 Food and Beverage Manufacturing (agroindústria) |
| Logística e transporte | 116 Transportation, Logistics, Supply Chain and Storage; 92 Truck Transportation; 87 Freight and Package Transportation; 93 Warehousing and Storage |
| Distribuição, atacado, importação | 133 Wholesale; 134 Wholesale Import and Export |
| Varejo | 27 Retail; 19 Retail Apparel and Fashion |
| Restaurantes e food service | 34 Food and Beverage Services; 32 Restaurants |
| Hotelaria, turismo e eventos | 31 Hospitality; 30 Travel Arrangements; 110 Events Services |
| Educação, cursos e treinamentos | 1999 Education; 68 Higher Education; 67 Primary and Secondary Education; 132 E-Learning Providers; 105 Professional Training and Coaching |
| Energia | 59 Utilities; 3240 Renewable Energy Power Generation; 387 Solar Electric Power Generation; 57 Oil and Gas |
| Telecom | 8 Telecommunications |
| Meio ambiente | 86 Environmental Services |
| Terceiro setor | 100 Non-profit Organizations |
| Governo | 75 Government Administration |
| Serviços ao consumidor | 91 Consumer Services |

Segmento fora da tabela: consultar o CSV oficial (https://github.com/HarvestAPI/linkedin-industry-codes-v2) por rótulo exato; sem ID confirmado, usar `searchQuery` ou buscar sem filtro de setor. Nunca inventar ID.

## Exemplos

“Founders de empresas B2B com mais de 10 funcionários em Ribeirão Preto, 20 leads”:
```json
{"profileScraperMode":"Full","maxItems":20,"startPage":1,"takePages":1,"autoQuerySegmentation":false,
 "currentJobTitles":["Founder","Co-Founder","Fundador","Cofundador"],
 "locations":["Ribeirão Preto, São Paulo, Brazil"],"companyHeadcount":["C","D","E","F","G","H","I"]}
```
B2B fica para a qualificação. Resultado real: 574 perfis disponíveis; 12 de 20 qualificados.

“Diretores comerciais de indústrias de 50 a 500 funcionários no interior de SP, 100 leads”:
```json
{"profileScraperMode":"Full","maxItems":100,"startPage":1,"takePages":4,"autoQuerySegmentation":false,
 "currentJobTitles":["Diretor Comercial","Diretora Comercial","Commercial Director","Sales Director","Head de Vendas"],
 "industryIds":["25","55","135","23","54"],"companyHeadcount":["D","E"],
 "locations":["São Paulo, Brazil"],"excludeLocations":["São Paulo, São Paulo, Brazil"]}
```

“Donos de agências de marketing em Curitiba, 50 leads”:
```json
{"profileScraperMode":"Full","maxItems":50,"startPage":1,"takePages":2,"autoQuerySegmentation":false,
 "seniorityLevelIds":["320"],"industryIds":["80","1862"],"locations":["Curitiba, Paraná, Brazil"]}
```

## Company Details: input enxuto

`{"companies":[URLs deduplicadas]}`, em uma única execução por etapa. Antes de enriquecer, aplicar os requisitos que dependem só da pessoa (cargo, localização, evidência explícita contra o ICP, como negócio claramente B2C); quem já falhou fica NÃO QUALIFICADO com motivo e sua empresa não é enriquecida. Usar `searches` só para nome distintivo sem URL; nome genérico (“Smart Consultoria”) traz homônimo e desperdiça cobrança.

## Leitura econômica dos datasets

Cada perfil traz imagens e logos que consomem contexto. Ler em lotes de 10 e projetar campos pais:
- Perfis: `id,firstName,lastName,linkedinUrl,headline,about,location,industry,currentPosition,websites,_meta`. `_meta.pagination.totalElements` informa quantos perfis a busca encontrou; citar ao usuário.
- `experience` só para quem tem outro vínculo atual capaz de mudar a decisão (headline cita outra empresa, cargo atual não é o pedido, empresa B2C com indício de outro negócio).
- Empresas: `id,universalName,linkedinUrl,name,website,tagline,description,employeeCount,employeeCountRange,foundedOn,industries,specialities,originalQuery`; `locations` só se houver requisito de sede.
`omit` não remove subcampos dentro de arrays; não contar com ele para cortar logos.
