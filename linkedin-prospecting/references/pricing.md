# Estimativa e autorização

Consultar preços/modelo vigente dos dois Actors e plano aplicável antes de calcular. Considerar páginas, perfis Full, empresas, início/mínimos e demais eventos relevantes. Exemplos históricos não são preços atuais. Sem preço confiável ou teto aplicável, parar antes de cobrança; não inventar valores.

Estimar N = 10, 100 e quantidade pedida, até uma empresa por pessoa no caso padrão; deduplicação pode reduzir custo. Vários vínculos: estimar todos ou limitar enriquecimento explicitamente. São perfis coletados, não aprovados. Quantidade de páginas pode variar com busca restritiva.

Quando confirmado preço por página + perfil + empresa, referência: `ceil(N/pessoas_por_pagina)*preco_pagina + N*preco_full + N*preco_empresa + eventos_fixos`. Não garantir páginas mínimas. Reservar páginas/eventos extras dentro de limites de trabalho escolhidos e subtetos; não ligar segmentação ilimitada.

Se usuário já informou teto, respeitar e avaliar viabilidade. Sem teto, propor na mesma confirmação máximo calculado do cenário planejado com margem de 25%, arredondado para cima ao centavo, respeitando mínimos. Não impor mínimo arbitrário de US$ 1. Margem insuficiente para eventos planejados: calcular teto maior e mostrar claramente. Teto proposto só é autorizado após confirmação; não criar quinta pergunta obrigatória de orçamento.

Mensagem curta com valores atuais:

> Vou buscar até [N] perfis de [cargos], em [segmento], na localização [local].
>
> Estimativa com dados das empresas: 10 leads ≈ US$ [A]; 100 leads ≈ US$ [B]. Para sua busca: ≈ US$ [C], com limite máximo de US$ [D].
>
> A quantidade é de perfis coletados; nem todos vão atender aos critérios. [Qualificação pelo seu ICP; limitação material, se houver.]
>
> Posso iniciar essa busca com esse limite?

Se N = 10/100, evitar repetir preço. Não expor fórmula/eventos salvo pedido técnico. Custos opcionais de serviço de exportação precisam ser informados ao escolher essa opção; não incluí-los silenciosamente no orçamento Apify.

Confirmado: registrar escopo/teto/autorização, aplicar `callOptions.maxTotalChargeUsd`. Soma dos subtetos não pode exceder autorização; se gasto de etapa anterior desconhecido, reservar subteto inteiro. Se limite impedir enriquecimento, entregar dados existentes, marcando NÃO QUALIFICADO com motivo quando requisito não puder ser confirmado, sem aumentar teto/reiniciar busca automaticamente. Mudança material de escopo/custo exige nova estimativa e confirmação.

Entrega: separar custo reportado, estimativa e limite. Somar custo total apenas se todas as etapas cobradas tiverem custo reportado; preservar informação parcial identificada, sem chamá-la de total. Indisponível: “A Apify não disponibilizou o custo final nesta consulta.” Nunca chamar estimativa de valor debitado.
