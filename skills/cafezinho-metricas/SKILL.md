---
name: cafezinho-metricas
description: "Atualiza semanalmente as métricas do Cafezinho Semanal de Liderança de Clientes no Notion e envia aviso no Slack. Use esta skill SEMPRE que o usuário pedir para \"atualizar o cafezinho\", \"atualizar as métricas do cafezinho\", \"rodar a atualização semanal de clientes\", ou qualquer variante de atualização das tabelas de KPIs/KRs do time de clientes no Notion. A skill busca dados do HubSpot e Snowflake, atualiza a coluna \"QTD Atual\" e \"Data Atualização\" na tabela do trimestre vigente, e envia mensagem no canal #area-clientes-líderes no Slack."
---

# Cafezinho Métricas — Atualização Semanal

## O que esta skill faz

1. Busca todos os indicadores do trimestre vigente (HubSpot + Snowflake)
2. Atualiza `QTD Atual` e `Data Atualização` na tabela do trimestre vigente no Notion
3. Para os indicadores de cavaleiro (`[GD - SAOs]`), atualiza também a coluna `Comentários` com um resumo analítico automático
4. Envia mensagem no canal `#area-clientes-líderes` no Slack avisando que a tabela foi atualizada

> **Nota:** Atualiza apenas o trimestre **vigente** (não o encerrado).
> Data de atualização = data de hoje.
> Comentários de cavaleiro são **substituídos** a cada execução.

---

## Notion — Configuração

### Página principal
URL: `https://www.notion.so/piposaude/Caf-Semanal-Lideran-a-de-Clientes-1664744bd803808b8364ebaa295c1ff4`

### Tabelas por trimestre (atualizar apenas a vigente)

| Trimestre | Collection ID |
|---|---|
| 1Q26 | `collection://33b4744b-d803-81ac-a143-000b38d1750a` |
| 2Q26 | `collection://2ea4744b-d803-8112-aa0d-000bec58fbfa` |

**Para descobrir o trimestre vigente:** `DATE_TRUNC('quarter', CURRENT_DATE)` — se retornar `2026-01-01`, usar 1Q26; se `2026-04-01`, usar 2Q26.

### Mapeamento de Page IDs — 2Q26
*(Atualizar este bloco a cada trimestre com os IDs corretos)*

| Indicador | Page ID |
|---|---|
| Clientes Ganhos G+ | `2ea4744bd803818985dbd8c7a933e537` |
| Clientes Ganhos P&M | `2ea4744bd80381dfab77cac6ac123155` |
| Clientes Ganhos Total | `2ea4744bd8038150b0dfca304cc2abc3` |
| MRR Ganhos G+ | `2ea4744bd80381daaf6ff29f056b0d38` |
| MRR Ganhos P&M | `2ea4744bd8038194bbe8eed316324db9` |
| MRR Ganhos Total | `2ea4744bd8038105886adf63afef82c3` |
| Leads Conectados G+ | `2ea4744bd80381ce9328ef12a4863431` |
| Leads Conectados P&M | `2ea4744bd8038171af95fa0ffb6a7e32` |
| Leads Conectados Total | `2ea4744bd803819f9bd2d88aa16610f8` |
| Qualificações G+ | `2ea4744bd80381cf9b83c2c0ce3b388a` |
| Qualificações P&M | `2ea4744bd80381d3880dd3d9cb6c7b0f` |
| Qualificações Total | `2ea4744bd80381ee98b3f709b01e1391` |
| SAOs G+ | `2ea4744bd80381df8ba7c1d355da262a` |
| SAOs P&M | `2ea4744bd803818b9011d7445b26a9dd` |
| SAOs Total | `2ea4744bd80381afa241e196217b2c24` |
| [GD - SAOs] Inbound | `3454744bd80380d38d7bc65be789c95f` |
| [GD - SAOs] SDR Outbound | `3454744bd8038014bf41f3b53d6e9f22` |
| [GD - SAOs] EV Outbound | `3454744bd80380cdb0f9c6c6bdb98a50` |
| [GD - SAOs] Parcerias | `3454744bd803804bbc45fedbe2f04b07` |
| Reuniões de Resultado | `2ea4744bd80381919ca6cf865f93dc38` |
| Comitês de Saúde | `2ea4744bd803818f8f6bec9ac7f80f70` |
| Ações de Alto Valor | `2ea4744bd80381e69598e9134e43922d` |
| Reuniões Estratégicas | `2ea4744bd80381279bf5cb5b1c1c6735` |
| % Implantações no Prazo | `2ea4744bd80381e384a1e36b991ae91e` |
| CSAT Implantação | `2ea4744bd803816ea2d0cdad03014d5a` |
| Churn Realizado | `2ea4744bd80381cfa395ddd884bcd70e` |
| [G+] Cotações no Prazo | `2ea4744bd8038116a3cdd7a9dad7d337` |
| [P/M] Cotações no Prazo | `2ea4744bd8038191844addc5b5e00256` |
| % Cotações Aceitas PLC | `2ea4744bd803811d8693ebe8f6b0430e` |
| [G+] Conversão de Estudos | `2ea4744bd80381d29606cc0c566f63fb` |
| [P/M] Conversão de Estudos | `2ea4744bd80381198844d19ad341b11f` |
| Receita com Operadoras | `2ea4744bd80381d590ece0efde73320e` |
| % Retenção de Receita | `2ea4744bd803817c8451c61c9715fc22` |

---

## Regras de Formatação dos Valores no Notion

| Indicador | Regra |
|---|---|
| Churn Realizado | Valor bruto (não dividir) |
| MRR Ganhos | Dividir por 1000 (ex: 134789 → 134.79) |
| Receita com Operadoras | Valor bruto completo (não dividir) |
| % Implantações no Prazo | Só o número sem % (ex: 61.7% → 61.7) |
| CSAT Implantação | Valor com decimal (ex: 4.55) |
| % Cotações G+/P&M | Só o número sem % (ex: 78% → 78) |
| % Cotações PLC | Só o número sem % (ex: 94% → 94) |
| [G+/P&M] Conversão Estudos | Só o número sem % (ex: 26.1% → 26.1) |
| % Retenção de Receita (NRR) | Só o número sem % (ex: 100.54% → 100.54) |

---

## Fontes de Dados

### 1. HubSpot — Clientes e MRR Ganhos

**G+** — filtro: `hs_v2_date_entered_26183057 >= início do trimestre`, `hubspot_team_id IN ('4587700', '42072907')`
**P&M** — filtro: `hubspot_team_id IN ('4587706', '4587701')`
**Total** — sem filtro de team, apenas `hs_v2_date_entered_26183057 >= início do trimestre`

> Importante: data no formato ISO string `"2026-04-01T00:00:00.000Z"` (não milissegundos)

**MRR:** somar campo `amount` dos deals filtrados acima. Dividir por 1000 no Notion.

### 2. HubSpot — Leads Conectados (SQLs)

Filtro base (aplicar nos 3 grupos: G+, P&M, Total):
- Stage: `hs_v2_date_entered_24595562 >= início do trimestre`
- `origem_micro_ NOT IN ('M&A - Convenia | Parcerias', 'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias', 'Não se aplica | Oportunidade de FC', 'PipoPartners')` + segundo filterGroup com `NOT_HAS_PROPERTY`
- `origem NEQ 'Não se aplica | Oportunidade de FC'`
- `classificacao_tamanho_da_empresa___pipo IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')`

CNs G+: `493569292` (Erika), `149768337` (Marianne)
CNs P&M: `331668616` (Breno), `1134248428` (Larissa), `84342335` (Letícia), `465298555` (Marcelo), `51778761` (Bruno), `175077773` (Luciano), `91493869` (Barbara Costa Borges)

### 3. HubSpot — Qualificações (SQLs stage)

Mesmo filtro base, mas usando `hs_v2_date_entered_24595561` como stage de entrada.

### 4. HubSpot — SAOs

Mesmo filtro base, mas usando `hs_v2_date_entered_9102669` como stage de entrada.

### 5. Snowflake — SAOs por Cavaleiro (GD)

Usar as queries abaixo para buscar o realizado de cada cavaleiro no trimestre vigente.
Filtros padrão aplicados em todas: `CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')`, exclusões de `ORIGEM_MICRO` e `ARCHIVED = false`.

**[GD - SAOs] Inbound**
```sql
SELECT COUNT(*) AS realizado
FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
WHERE d.hs_v2_date_entered_9102669 >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND d.hs_v2_date_entered_9102669 < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND d.ORIGEM IN ('Levantada', 'Materiais', 'Eventos', 'Indicação')
  AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
  AND (d.ORIGEM_MICRO NOT IN (
      'M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC',
      'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias'
  ) OR d.ORIGEM_MICRO IS NULL)
  AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
```

**[GD - SAOs] SDR Outbound**
```sql
SELECT COUNT(*) AS realizado
FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
WHERE d.hs_v2_date_entered_9102669 >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND d.hs_v2_date_entered_9102669 < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND d.ORIGEM = 'Prospecção'
  AND d.CN IN ('1134248428', '84342335', '493569292')
  AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
  AND (d.ORIGEM_MICRO NOT IN (
      'M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC',
      'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias'
  ) OR d.ORIGEM_MICRO IS NULL)
  AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
```

**[GD - SAOs] EV Outbound**
```sql
SELECT COUNT(*) AS realizado
FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
WHERE d.hs_v2_date_entered_9102669 >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND d.hs_v2_date_entered_9102669 < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND d.ORIGEM = 'Prospecção'
  AND d.CN IN ('331668616', '465298555', '175077773', '149768337')
  AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
  AND (d.ORIGEM_MICRO NOT IN (
      'M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC',
      'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias'
  ) OR d.ORIGEM_MICRO IS NULL)
  AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
```

**[GD - SAOs] Parcerias**
```sql
SELECT COUNT(*) AS realizado
FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
WHERE d.hs_v2_date_entered_9102669 >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND d.hs_v2_date_entered_9102669 < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND d.ORIGEM = 'Parcerias'
  AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
  AND (d.ORIGEM_MICRO NOT IN (
      'M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC',
      'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias'
  ) OR d.ORIGEM_MICRO IS NULL)
  AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
```

---

## Queries Snowflake

### Fix crítico de DAYOFWEEK
O Metabase usa `DAYOFWEEK NOT IN (1, 7)` com seu próprio parser. Para replicar corretamente no Snowflake:
- **Holidays:** manter `DAYOFWEEK NOT IN (1, 7)` — preserva comportamento do Metabase (feriados em segunda não são excluídos)
- **Business_Days e Calendar:** usar `DAYOFWEEKISO NOT IN (6, 7)` — exclui sábado (6) e domingo (7) corretamente

### CTE de Feriados e Dias Úteis (reutilizar em todas as queries de cotações)

```sql
WITH Holidays AS (
  SELECT holiday_date FROM (
    SELECT DATE_FROM_PARTS(yr, 1,  1) AS holiday_date FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 4, 21) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 5,  1) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 9,  7) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 10, 12) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 11,  2) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 11, 15) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 11, 20) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
    UNION ALL SELECT DATE_FROM_PARTS(yr, 12, 25) FROM (VALUES (2023),(2024),(2025),(2026)) AS years(yr)
  ) AS fixed_holidays WHERE DAYOFWEEK(holiday_date) NOT IN (1, 7)
  UNION ALL
  SELECT holiday_date FROM (VALUES
    ('2023-02-20'::DATE),('2023-02-21'::DATE),('2023-04-07'::DATE),('2023-06-08'::DATE),
    ('2024-02-12'::DATE),('2024-02-13'::DATE),('2024-03-29'::DATE),('2024-05-30'::DATE),
    ('2025-03-03'::DATE),('2025-03-04'::DATE),('2025-04-18'::DATE),('2025-06-19'::DATE),
    ('2026-02-16'::DATE),('2026-02-17'::DATE),('2026-04-03'::DATE),('2026-06-04'::DATE)
  ) AS t(holiday_date) WHERE DAYOFWEEK(holiday_date) NOT IN (1, 7)
),
Calendar AS (
  SELECT DATEADD(day, SEQ4(), '2023-01-01'::DATE) AS cal_date FROM TABLE(GENERATOR(ROWCOUNT => 1461))
),
Business_Days AS (
  SELECT cal_date FROM Calendar
  WHERE DAYOFWEEKISO(cal_date) NOT IN (6, 7)
    AND cal_date NOT IN (SELECT holiday_date FROM Holidays)
)
```

### Reuniões de Resultado
```sql
SELECT
  COUNT(*) AS "count"
FROM
  "PROSPECTION"."GOLD"."HUBSPOT_MEETINGS"
WHERE
  "HS_ACTIVITY_TYPE" = 'GC | Reunião Resultados'
  AND "HS_MEETING_OUTCOME" IN ('COMPLETED', 'CONCLUÍDO [PRESENCIAL]')
  AND "HS_TIMESTAMP" >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND "HS_TIMESTAMP" < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE));
```

### Comitês de Saúde
```sql
SELECT
  COUNT(DISTINCT "HUBSPOT_COMPANY_ID") AS "count"
FROM
  "PROSPECTION"."GOLD"."HUBSPOT_MEETINGS"
WHERE
  "HS_ACTIVITY_TYPE" = 'Saúde | Comitê de Saúde'
  AND "HS_MEETING_OUTCOME" IN ('COMPLETED', 'CONCLUÍDO [PRESENCIAL]')
  AND "HS_TIMESTAMP" >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND "HS_TIMESTAMP" < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE));
```

### Ações de Alto Valor
```sql
SELECT
  COUNT(DISTINCT "HUBSPOT_COMPANY_ID") AS "count"
FROM
  "PROSPECTION"."GOLD"."HUBSPOT_MEETINGS"
WHERE
  (
    "HS_ACTIVITY_TYPE" NOT IN (
        'Follow up | Pré-Vendas e Vendas',
        'GC | Alinhamento com o cliente',
        'GC | Interna com Placement',
        'GC | Interna com Saúde',
        'GC | Onboarding - Alinhamento com cliente',
        'GC | Onboarding - Kickoff',
        'GC | Onboarding - Pré-KickOff',
        'GC | Outras',
        'GC | Passagem de bastão externa',
        'GC | Passagem de bastão interna',
        'GC | Racional cotação',
        'GC | Renovação - Prévia',
        'GC | Renovação - Recomendação',
        'GC | Reunião com Parceiro',
        'GC | Reunião Interna',
        'GC | Reunião Resultados',
        'IMP | Reunião de mapeamento operacional',
        'Primeira Abordagem | Pré-Vendas',
        'Qualificação | Pré-Vendas e Vendas',
        'Touchpoint | Apresentação de Proposta',
        'Touchpoint | Briefing de Cotação (Pré-Cotação)',
        'Touchpoint | Demonstração da Plataforma',
        'Touchpoint | Mapeamento e Diagnóstico',
        'Touchpoint | Reunião com Consultoria de Benefícios',
        'Touchpoint | Reunião com Time de Operação (Alinhamentos)',
        'Touchpoint | Reunião com Time de Saúde',
        'Touchpoint | Reunião de Alinhamentos (Negociação)',
        'Touchpoint | Visita, almoço (Relacionamento)',
        'Saúde | Comitê de Saúde'
    )
    OR "HS_ACTIVITY_TYPE" IS NULL
  )
  AND "HS_MEETING_OUTCOME" IN ('COMPLETED', 'CONCLUÍDO [PRESENCIAL]')
  AND "HS_TIMESTAMP" >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND "HS_TIMESTAMP" < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE));
```

### Reuniões Estratégicas
```sql
WITH EmpresasElegiveis AS (
  SELECT 
    "NOME_DA_EMPRESA"
  FROM (
      SELECT
        UPPER("NAME") AS "NOME_DA_EMPRESA",
        "ESTAGIO_NA_PIPO",
        "MRR",
        "ELEGIVEL___REUNIAO_ESTRATEGICA",
        "ID",
        "HUBSPOT_TEAM_ID",
        "DATA_CLIENTE",
        ROW_NUMBER() OVER (
            PARTITION BY UPPER("NAME") 
            ORDER BY 
                CASE WHEN "DATA_CLIENTE" IS NOT NULL THEN 1 ELSE 2 END ASC, 
                "ID" DESC
        ) as rn_unica
      FROM "PROSPECTION"."GOLD"."HUBSPOT_COMPANIES"
  )
  WHERE rn_unica = 1
    AND (
      (
        "ESTAGIO_NA_PIPO" IN ('Renovação', 'Onboarding', 'Engajamento')
        AND "MRR" >= 15000
        AND "ELEGIVEL___REUNIAO_ESTRATEGICA" IS NULL
      )
      OR (
        "ESTAGIO_NA_PIPO" IN ('Renovação', 'Onboarding', 'Engajamento')
        AND "HUBSPOT_TEAM_ID" = '48954665'
        AND "MRR" >= 10000
      )
    )
)

SELECT
  COUNT(DISTINCT UPPER(comp."NAME")) AS "QUANTIDADE_REUNIOES_NO_TRIMESTRE_PARA_EMPRESAS_ELEGIVEIS"
FROM
  "PROSPECTION"."GOLD"."HUBSPOT_MEETINGS" AS meet
JOIN 
  "PROSPECTION"."GOLD"."HUBSPOT_COMPANIES" AS comp ON meet."HUBSPOT_COMPANY_ID" = comp."ID"
WHERE
  meet."HS_ACTIVITY_TYPE" = 'RC | Reunião de alinhamento estratégico semestral'
  AND meet."HS_MEETING_OUTCOME" IN ('COMPLETED', 'CONCLUÍDO [PRESENCIAL]')
  AND DATE_TRUNC('quarter', CAST(meet."HS_TIMESTAMP" AS DATE)) = DATE_TRUNC('quarter', CURRENT_DATE)
  AND UPPER(comp."NAME") IN (SELECT "NOME_DA_EMPRESA" FROM EmpresasElegiveis);
```

### % Implantações no Prazo
```sql
SELECT ROUND(
  SUM(CASE WHEN DATE_TRUNC('day', "CLOSED_DATE") <= DATE_TRUNC('day', "DATA_PREVISTA_PARA_FINALIZAR_TODA_A_JORNADA_DE_ONBOARDING") THEN 1.0 ELSE 0.0 END)
  / NULLIF(COUNT(*), 0) * 100, 1) AS percentual_no_prazo
FROM "PROSPECTION"."GOLD"."HUBSPOT_TICKETS"
WHERE "PIPELINE" = 'Implantação'
  AND "TIPO_DE_PROCESSO___ONBOARDING" NOT IN ('Demanda Extra','Preenchimento pendente')
  AND "PIPELINE_STAGE" IN ('Processo finalizado', 'Apólice Implantada')
  AND "ARCHIVED" = 'false'
  AND DATE_TRUNC('quarter', "CLOSED_DATE") = DATE_TRUNC('quarter', CURRENT_DATE)
```

### CSAT Implantação
```sql
WITH RespostasUnicas AS (
  SELECT
    CASE WHEN TO_CHAR(HS_CREATEDATE,'DD/MM/YYYY HH24:MI') = '09/02/2026 14:56'
      AND HS_CONTACT_EMAIL_ROLLUP = 'leonardo.machado@silveiro.com.br' THEN 5
      ELSE SATISFCACAO_COM_A_COMUNICACAO END AS NOTA_COM,
    CASE WHEN TO_CHAR(HS_CREATEDATE,'DD/MM/YYYY HH24:MI') = '09/02/2026 14:56'
      AND HS_CONTACT_EMAIL_ROLLUP = 'leonardo.machado@silveiro.com.br' THEN 5
      ELSE PLANEJAMENTO_DE_REUNIOES_E_EXECUCAO_CRONOGRAMA END AS NOTA_CRONO,
    CASE WHEN TO_CHAR(HS_CREATEDATE,'DD/MM/YYYY HH24:MI') = '09/02/2026 14:56'
      AND HS_CONTACT_EMAIL_ROLLUP = 'leonardo.machado@silveiro.com.br' THEN 5
      ELSE PERCEPCAO_SOBRE_OS_MATERIAIS END AS NOTA_MAT,
    ROW_NUMBER() OVER (PARTITION BY COALESCE(HS_CONTACT_FIRSTNAME||' '||HS_CONTACT_LASTNAME,'') ORDER BY HS_CREATEDATE DESC) AS ranking_recente
  FROM "PROSPECTION"."GOLD"."HUBSPOT_FEEDBACK_SUBMISSIONS"
  WHERE DATE_TRUNC('quarter', HS_CREATEDATE) = DATE_TRUNC('quarter', CURRENT_DATE)
    AND COALESCE(HS_CONTACT_FIRSTNAME||' '||HS_CONTACT_LASTNAME,'') <> 'MARIA PAULA CAETANO DE OLIVEIRA'
    AND HS_OBJECT_ID <> '516333818391'
)
SELECT ROUND((SUM(NOTA_COM)+SUM(NOTA_CRONO)+SUM(NOTA_MAT))::NUMERIC
  / NULLIF((COUNT(NOTA_COM)+COUNT(NOTA_CRONO)+COUNT(NOTA_MAT)),0), 2) AS media_csat
FROM RespostasUnicas WHERE ranking_recente = 1
```

### Churn Realizado
```sql
WITH MRR_PERDIDO AS (
  SELECT SUM(fi."VITALICIO_TOTAL") AS VALOR
  FROM "FINANCE"."SILVER"."SHEETS_VIDAS_RECEITA_GERENCIAL_INVOICES" fi
  JOIN "PROSPECTION"."GOLD"."HUBSPOT_COMPANIES" hc ON hc."MAIN_COMPANY_ID" = fi."COMPANY_ID"
  WHERE DATE_TRUNC('quarter', TO_DATE(hc."DATA_SAIDA_CLIENTE", 'YYYY-MM-DD')) = DATE_TRUNC('quarter', CURRENT_DATE)
    AND fi."METABASE_DATA" = DATEADD('month', -1, DATE_TRUNC('quarter', TO_DATE(hc."DATA_SAIDA_CLIENTE", 'YYYY-MM-DD')))
    AND hc."ESTAGIO_NA_PIPO" = 'Churn'
    AND LOWER(hc."NAME") NOT LIKE '%togito%'
    AND LOWER(hc."NAME") NOT LIKE '%fake%'
    AND LOWER(hc."NAME") NOT LIKE '%teste%'
),
MRR_APOLICES AS (
  SELECT SUM("APOLICE___MRR") AS VALOR
  FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS"
  WHERE "PIPELINE" = 'Apólices'
    AND "APOLICE___MRR" IS NOT NULL
    AND DATE_TRUNC('quarter', "CLOSEDATE") = DATE_TRUNC('quarter', CURRENT_DATE)
)
SELECT COALESCE(SUM(VALOR), 0) AS churn_total
FROM (SELECT VALOR FROM MRR_PERDIDO UNION ALL SELECT VALOR FROM MRR_APOLICES)
```

### [G+] Cotações Entregues no Prazo
*(Usar CTE de Holidays + Business_Days acima)*
```sql
SELECT ROUND(CAST(COUNT(CASE
  WHEN t.complexidade = 'Estudo Tarifário' AND t.dias_uteis <= 5 THEN 1
  WHEN t.complexidade IN ('Odonto - Nível I','Odonto - Nível II','Saúde - Nível I','Saúde - Nível II','Vida - Nível I','Vida - Nível II') AND t.dias_uteis <= 15 THEN 1
  WHEN t.complexidade = 'Consultoria de benefícios - Nível III' AND t.dias_uteis <= 20 THEN 1
  WHEN t.complexidade = 'Cross-sell' AND t.dias_uteis <= 10 THEN 1
  ELSE NULL END) AS FLOAT) / NULLIF(COUNT(*), 0) * 100, 1) AS perc_sla_gplus
FROM (
  SELECT "COTAR___GRAU_DE_COMPLEXIDADE_DA_COTACAO" AS complexidade,
    (SELECT COUNT(*) FROM Business_Days bd WHERE bd.cal_date > "HS_DATE_ENTERED_2228911" AND bd.cal_date <= "DATA_DEVOLUTIVA_DISPONIVEL") AS dias_uteis
  FROM "PROSPECTION"."GOLD"."HUBSPOT_TICKETS"
  WHERE "HUBSPOT_TEAM_ID" = 63416257
    AND "TIME_SOLICITANTE" IN ('Vendas', 'RC')
    AND "DATA_DEVOLUTIVA_DISPONIVEL" >= DATE_TRUNC('quarter', CURRENT_DATE)
    AND "ARCHIVED" = 'false'
    AND "TIPO_DE_SOLICITACAO" NOT IN ('Portabilidade', 'Portabilidade - FC')
    AND "BENEFICIO_A_SER_COTADO" NOT IN ('Farmácia', 'Previdência Privada')
    AND "DATA_DEVOLUTIVA_DISPONIVEL" IS NOT NULL
    AND "HS_DATE_ENTERED_2228911" IS NOT NULL
    AND "COTAR___GRAU_DE_COMPLEXIDADE_DA_COTACAO" IN (
      'Estudo Tarifário','Odonto - Nível I','Odonto - Nível II','Saúde - Nível I',
      'Saúde - Nível II','Vida - Nível I','Vida - Nível II',
      'Consultoria de benefícios - Nível III','Cross-sell')
) t
```
*Para P&M: substituir `"HUBSPOT_TEAM_ID" = 63416257` por `"HUBSPOT_TEAM_ID" = 4078526`*

### % Cotações Aceitas PLC (100 dias)
```sql
WITH cotacoes AS (
  SELECT "PRAZO_DA_SOLICITACAO_DE_COTACAO" AS STATUS,
    DATEDIFF(DAY, CURRENT_DATE, "DATA_PROX_REAJUSTE") AS DIAS_ATE_REAJUSTE
  FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS"
  WHERE "PIPELINE" = 'Relacionamento com cliente'
    AND "DATA_PROX_REAJUSTE" >= DATEADD(month, 4, DATE_TRUNC('quarter', CURRENT_DATE))
    AND "DATA_PROX_REAJUSTE" <= DATEADD(month, 6, DATE_TRUNC('quarter', CURRENT_DATE)) - 1
    AND "APOLICE___BENEFICIO" IN ('Saúde', 'Odonto', 'Saúde e Odonto')
    AND "PRAZO_DA_SOLICITACAO_DE_COTACAO" <> 'Não se aplica'
    AND "TIPO_DE_OPORTUNIDADE" IN ('Renovação', 'Reajuste')
)
SELECT ROUND(COUNT(CASE WHEN STATUS = 'Dentro do prazo' THEN 1 END) / NULLIF(COUNT(*), 0) * 100, 1) AS percentual_no_prazo
FROM cotacoes
WHERE DIAS_ATE_REAJUSTE < 100 OR STATUS = 'Dentro do prazo'
```

### [G+] Conversão de Estudos em Vendas
```sql
WITH oportunidades AS (
  SELECT deal_stage FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS"
  WHERE houve_participacao_de_placement_ = 'true'
    AND classificacao_tamanho_da_empresa___pipo IN ('G (601+)', 'Enterprise')
    AND deal_stage IN ('12 Não finalizada, mas com gongos','13 Finalizada com gongos','14 Finalizada sem gongos')
    AND DATE_TRUNC('quarter', "CLOSEDATE") = DATE_TRUNC('quarter', CURRENT_DATE)
)
SELECT ROUND(CAST(COUNT(CASE WHEN deal_stage IN ('12 Não finalizada, mas com gongos','13 Finalizada com gongos') THEN 1 END) AS FLOAT)
  / NULLIF(COUNT(*), 0) * 100, 1) AS conversao_gplus
FROM oportunidades
```
*Para P&M: substituir `('G (601+)', 'Enterprise')` por `('Startup (1-80)', 'P (81-200)', 'M (201-600)')`*

### Receita com Operadoras (AG + Premiação)
```sql
SELECT SUM(valor_bruto) AS total_valor_bruto
FROM finance.silver.sheets_controle_de_faturamento
WHERE data_emissao >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND data_emissao < DATEADD(quarter, 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND tipo_de_receita IN ('Agenciamento', 'Premiação')
```
> Usar o valor bruto completo no Notion (sem dividir).

### % Retenção de Receita (NRR)
```sql
WITH
cross_sell AS (
  SELECT 1 AS id, SUM("AMOUNT") AS RECEITA_CROSS_SELL
  FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS"
  WHERE "PIPELINE" = 'Relacionamento com cliente' AND "DEAL_STAGE" = 'Gongo'
    AND "TIPO_DE_OPORTUNIDADE" = 'Cross Sell'
    AND DATE_TRUNC('quarter', "CLOSEDATE") = DATE_TRUNC('quarter', CURRENT_DATE)
),
renovacoes AS (
  SELECT 1 AS id,
  SUM(CAST(COALESCE(t."VALOR_DA_FATURA",0) AS FLOAT)
    * (CASE WHEN ABS(CAST(COALESCE(t."REAJUSTE_FINAL",0) AS FLOAT)) >= 1 THEN CAST(COALESCE(t."REAJUSTE_FINAL",0) AS FLOAT)/100.0 ELSE CAST(COALESCE(t."REAJUSTE_FINAL",0) AS FLOAT) END)
    * (CASE WHEN ABS(CAST(COALESCE(t."COMISSAO___VITALICIO_PORCENTAGEM",0) AS FLOAT)) >= 1 THEN CAST(COALESCE(t."COMISSAO___VITALICIO_PORCENTAGEM",0) AS FLOAT)/100.0 ELSE CAST(COALESCE(t."COMISSAO___VITALICIO_PORCENTAGEM",0) AS FLOAT) END)
  ) AS RECEITA_RENOVACAO
  FROM "PROSPECTION"."GOLD"."HUBSPOT_TICKETS" t
  JOIN "PROSPECTION"."GOLD"."HUBSPOT_COMPANIES" hc ON hc."NAME" = t."HS_PRIMARY_COMPANY_NAME"
  WHERE t."PIPELINE" = 'Cotação' AND t."PIPELINE_STAGE" = 'Gongo'
    AND t."TIPO_DE_SOLICITACAO" = 'Renovação / Reajuste / Migração de Porte'
    AND DATE_TRUNC('quarter', t."CLOSED_DATE") = DATE_TRUNC('quarter', CURRENT_DATE)
),
aumento_vitalicio AS (
  SELECT 1 AS id,
  SUM(CAST(COALESCE("VALOR_DA_ULTIMA_FATURA",0) AS FLOAT) * (
    (CASE WHEN ABS(CAST(COALESCE("AUMENTO_DE_VITALICIO_APROVADO_",0) AS FLOAT)) >= 1 THEN CAST(COALESCE("AUMENTO_DE_VITALICIO_APROVADO_",0) AS FLOAT)/100.0 ELSE CAST(COALESCE("AUMENTO_DE_VITALICIO_APROVADO_",0) AS FLOAT) END)
    - (CASE WHEN ABS(CAST(COALESCE("COMISSAO",0) AS FLOAT)) >= 1 THEN CAST(COALESCE("COMISSAO",0) AS FLOAT)/100.0 ELSE CAST(COALESCE("COMISSAO",0) AS FLOAT) END)
  )) AS RECEITA_AUMENTO_VITALICIO
  FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS"
  WHERE "PIPELINE" = 'Relacionamento com cliente' AND "TIPO_DE_OPORTUNIDADE" = 'Negociação de Vitalício'
    AND "DEAL_STAGE" = 'Gongo'
    AND DATE_TRUNC('quarter', "INICIO_DO_AUMENTO_DE_VITALICIO") = DATE_TRUNC('quarter', CURRENT_DATE)
),
receita_perdida AS (
  SELECT 1 AS id, SUM(VALOR) * -1 AS RECEITA_PERDIDA FROM (
    SELECT SUM(fi."VITALICIO_TOTAL") AS VALOR
    FROM "FINANCE"."SILVER"."SHEETS_VIDAS_RECEITA_GERENCIAL_INVOICES" fi
    JOIN "PROSPECTION"."GOLD"."HUBSPOT_COMPANIES" hc ON hc."MAIN_COMPANY_ID" = fi."COMPANY_ID"
    WHERE DATE_TRUNC('quarter', TO_DATE(hc."DATA_SAIDA_CLIENTE",'YYYY-MM-DD')) = DATE_TRUNC('quarter', CURRENT_DATE)
      AND fi."METABASE_DATA" = DATEADD('month', -1, DATE_TRUNC('quarter', TO_DATE(hc."DATA_SAIDA_CLIENTE",'YYYY-MM-DD')))
      AND hc."ESTAGIO_NA_PIPO" = 'Churn'
    UNION ALL
    SELECT SUM("APOLICE___MRR") AS VALOR FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS"
    WHERE "PIPELINE" = 'Apólices' AND "APOLICE___MRR" IS NOT NULL
      AND DATE_TRUNC('quarter', "CLOSEDATE") = DATE_TRUNC('quarter', CURRENT_DATE)
  )
),
saldo AS (
  SELECT (COALESCE(cs.RECEITA_CROSS_SELL,0)+COALESCE(r.RECEITA_RENOVACAO,0)+COALESCE(av.RECEITA_AUMENTO_VITALICIO,0)+COALESCE(rp.RECEITA_PERDIDA,0)) AS SALDO
  FROM (SELECT 1 AS id) base
  LEFT JOIN cross_sell cs ON base.id=cs.id
  LEFT JOIN renovacoes r ON base.id=r.id
  LEFT JOIN aumento_vitalicio av ON base.id=av.id
  LEFT JOIN receita_perdida rp ON base.id=rp.id
),
base_anterior AS (
  SELECT SUM(inv."VITALICIO_TOTAL") AS RECEITA_BASE
  FROM "FINANCE"."SILVER"."SHEETS_VIDAS_RECEITA_GERENCIAL_INVOICES" AS inv
  LEFT JOIN (
    SELECT hc."MAIN_COMPANY_ID", ROW_NUMBER() OVER (PARTITION BY hc."MAIN_COMPANY_ID" ORDER BY hc."UPDATED_AT" DESC) AS rn
    FROM "PROSPECTION"."GOLD"."HUBSPOT_COMPANIES" AS hc
    WHERE hc."HUBSPOT_TEAM_ID" IS NOT NULL AND hc."DATA_CLIENTE" IS NOT NULL AND hc."ARCHIVED" = FALSE
  ) AS ch ON ch."MAIN_COMPANY_ID" = inv."COMPANY_ID" AND ch.rn = 1
  WHERE DATE_TRUNC('month', inv."METABASE_DATA") = DATEADD('month', -1, DATE_TRUNC('quarter', CURRENT_DATE))
)
SELECT ROUND(((b.RECEITA_BASE + s.SALDO) / NULLIF(b.RECEITA_BASE, 0)) * 100, 2) AS nrr_percentual
FROM saldo s, base_anterior b
```
> Inserir o resultado numérico diretamente no Notion (ex: 100.54).

---


---

## Geração de Comentários — Cavaleiros [GD - SAOs]

Para cada cavaleiro, após buscar os dados de realizado e pace, gerar um comentário analítico e atualizar a coluna `Comentários` no Notion junto com `QTD Atual`.

### Queries auxiliares necessárias

**Pace esperado na semana atual (todos os cavaleiros):**
```sql
WITH RECURSIVE
params AS (
    SELECT DATE_TRUNC('quarter', CURRENT_DATE) AS dt_inicio,
           DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE)) - 1 AS dt_fim
),
calendario AS (
    SELECT DATE_TRUNC('WEEK', (SELECT dt_inicio FROM params))::date AS data_semana
    UNION ALL
    SELECT (data_semana + INTERVAL '1 week')::date
    FROM calendario
    WHERE data_semana < (SELECT dt_fim FROM params)
),
metas AS (
    SELECT 'Inbound'      AS cavaleiro, 38 AS meta UNION ALL
    SELECT 'SDR Outbound' AS cavaleiro, 18 AS meta UNION ALL
    SELECT 'EV Outbound'  AS cavaleiro, 12 AS meta UNION ALL
    SELECT 'Parcerias'    AS cavaleiro, 10 AS meta
),
saos_raw AS (
    SELECT
        DATE_TRUNC('WEEK', d.hs_v2_date_entered_9102669)::date AS data_semana,
        CASE
            WHEN d.ORIGEM IN ('Levantada', 'Materiais', 'Eventos', 'Indicação') THEN 'Inbound'
            WHEN d.ORIGEM = 'Prospecção' AND d.CN IN ('1134248428', '84342335', '493569292') THEN 'SDR Outbound'
            WHEN d.ORIGEM = 'Prospecção' AND d.CN IN ('331668616', '465298555', '175077773', '149768337') THEN 'EV Outbound'
            WHEN d.ORIGEM = 'Parcerias' THEN 'Parcerias'
        END AS cavaleiro
    FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
    WHERE d.hs_v2_date_entered_9102669 >= (SELECT dt_inicio FROM params)
      AND d.hs_v2_date_entered_9102669 < (SELECT dt_fim FROM params) + INTERVAL '1 day'
      AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
      AND (d.ORIGEM_MICRO NOT IN ('M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC', 'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias') OR d.ORIGEM_MICRO IS NULL)
      AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
),
vendas AS (
    SELECT data_semana, cavaleiro, COUNT(*) AS contagem
    FROM saos_raw WHERE cavaleiro IS NOT NULL GROUP BY 1, 2
),
base AS (
    SELECT c.data_semana, m.cavaleiro, m.meta,
        COALESCE(v.contagem, 0) AS realizado_na_semana,
        CASE
            WHEN (c.data_semana + 6) >= (SELECT dt_fim FROM params) THEN 1.0
            WHEN (c.data_semana + 6) < (SELECT dt_inicio FROM params) THEN 0.0
            ELSE ((c.data_semana + 6) - (SELECT dt_inicio FROM params))::numeric
                 / (((SELECT dt_fim FROM params) - (SELECT dt_inicio FROM params)) + 1)
        END AS pct_tempo_decorrido
    FROM calendario c CROSS JOIN metas m
    LEFT JOIN vendas v ON v.data_semana = c.data_semana AND v.cavaleiro = m.cavaleiro
),
calculo AS (
    SELECT data_semana, cavaleiro, meta,
        SUM(realizado_na_semana) OVER (PARTITION BY cavaleiro ORDER BY data_semana ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS realizado_acumulado,
        GREATEST(ROUND(meta * pct_tempo_decorrido, 0), 2) AS pace_esperado
    FROM base
),
pace_pct AS (
    SELECT data_semana, cavaleiro, meta, realizado_acumulado, pace_esperado,
        ROUND(realizado_acumulado::numeric / NULLIF(pace_esperado::numeric, 0), 3) AS pct_pace
    FROM calculo WHERE data_semana <= DATE_TRUNC('WEEK', CURRENT_DATE)
),
com_anterior AS (
    SELECT p.*, LAG(pct_pace) OVER (PARTITION BY cavaleiro ORDER BY data_semana) AS pct_pace_anterior
    FROM pace_pct p
)
SELECT cavaleiro, meta, realizado_acumulado, pace_esperado, pct_pace, pct_pace_anterior,
    ROUND((pct_pace - COALESCE(pct_pace_anterior, pct_pace)) * 100, 0) AS variacao_pp,
    CASE
        WHEN pct_pace_anterior IS NULL THEN '—'
        WHEN pct_pace - pct_pace_anterior > 0.05 THEN '↑'
        WHEN pct_pace - pct_pace_anterior < -0.05 THEN '↓'
        ELSE '→'
    END AS tendencia
FROM com_anterior
WHERE data_semana = DATE_TRUNC('WEEK', CURRENT_DATE)
ORDER BY cavaleiro
```

**Leads atrasados — Inbound (acima da mediana histórica):**
```sql
WITH mediana_origem AS (
    SELECT d.ORIGEM,
        MEDIAN(DATEDIFF('day', d.hs_v2_date_entered_24595562, d.hs_v2_date_entered_24595561)) AS mediana_con_sql
    FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
    WHERE d.hs_v2_date_entered_24595562 >= DATEADD('year', -1, CURRENT_DATE)
      AND d.hs_v2_date_entered_24595562 < DATE_TRUNC('quarter', CURRENT_DATE)
      AND d.hs_v2_date_entered_24595561 IS NOT NULL
      AND d.ORIGEM IN ('Levantada', 'Materiais', 'Eventos', 'Indicação')
      AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
      AND (d.ORIGEM_MICRO NOT IN ('M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC', 'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias') OR d.ORIGEM_MICRO IS NULL)
      AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
    GROUP BY 1
)
SELECT d.ORIGEM AS origem, d.DEALNAME AS empresa,
    DATEDIFF('day', d.hs_v2_date_entered_24595562, CURRENT_DATE) AS dias_parado,
    ROUND(m.mediana_con_sql, 1) AS mediana,
    ROUND(DATEDIFF('day', d.hs_v2_date_entered_24595562, CURRENT_DATE) - m.mediana_con_sql, 1) AS atraso
FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
JOIN mediana_origem m ON m.ORIGEM = d.ORIGEM
WHERE d.hs_v2_date_entered_24595562 >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND d.hs_v2_date_entered_24595562 < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND d.hs_v2_date_entered_24595561 IS NULL
  AND d.hs_v2_date_entered_24595564 IS NULL
  AND d.ORIGEM IN ('Levantada', 'Materiais', 'Eventos', 'Indicação')
  AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
  AND (d.ORIGEM_MICRO NOT IN ('M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC', 'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias') OR d.ORIGEM_MICRO IS NULL)
  AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
  AND DATEDIFF('day', d.hs_v2_date_entered_24595562, CURRENT_DATE) > m.mediana_con_sql
ORDER BY atraso DESC LIMIT 5
```

**Deals atrasados — SDR e EV Outbound (acima da mediana histórica por consultor):**
```sql
WITH mediana_consultor AS (
    SELECT
        CASE WHEN d.CN IN ('1134248428', '84342335', '493569292') THEN 'SDR Outbound'
             WHEN d.CN IN ('331668616', '465298555', '175077773', '149768337') THEN 'EV Outbound'
        END AS cavaleiro,
        d.CONSULTOR_DE_NEGOCIO_NAME AS consultor,
        MEDIAN(DATEDIFF('day', d.hs_v2_date_entered_24595562, d.hs_v2_date_entered_24595561)) AS mediana_con_sql
    FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
    WHERE d.hs_v2_date_entered_24595562 >= DATEADD('year', -1, CURRENT_DATE)
      AND d.hs_v2_date_entered_24595562 < DATE_TRUNC('quarter', CURRENT_DATE)
      AND d.hs_v2_date_entered_24595561 IS NOT NULL
      AND d.ORIGEM = 'Prospecção'
      AND d.CN IN ('1134248428', '84342335', '493569292', '331668616', '465298555', '175077773', '149768337')
      AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
      AND (d.ORIGEM_MICRO NOT IN ('M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC', 'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias') OR d.ORIGEM_MICRO IS NULL)
      AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
    GROUP BY 1, 2
)
SELECT
    CASE WHEN d.CN IN ('1134248428', '84342335', '493569292') THEN 'SDR Outbound'
         WHEN d.CN IN ('331668616', '465298555', '175077773', '149768337') THEN 'EV Outbound'
    END AS cavaleiro,
    d.CONSULTOR_DE_NEGOCIO_NAME AS consultor,
    d.DEALNAME AS empresa,
    DATEDIFF('day', d.hs_v2_date_entered_24595562, CURRENT_DATE) AS dias_parado,
    ROUND(m.mediana_con_sql, 1) AS mediana,
    ROUND(DATEDIFF('day', d.hs_v2_date_entered_24595562, CURRENT_DATE) - m.mediana_con_sql, 1) AS atraso
FROM "PROSPECTION"."GOLD"."HUBSPOT_DEALS" d
JOIN mediana_consultor m
    ON m.consultor = d.CONSULTOR_DE_NEGOCIO_NAME
    AND m.cavaleiro = CASE WHEN d.CN IN ('1134248428', '84342335', '493569292') THEN 'SDR Outbound'
                           WHEN d.CN IN ('331668616', '465298555', '175077773', '149768337') THEN 'EV Outbound' END
WHERE d.hs_v2_date_entered_24595562 >= DATE_TRUNC('quarter', CURRENT_DATE)
  AND d.hs_v2_date_entered_24595562 < DATEADD('quarter', 1, DATE_TRUNC('quarter', CURRENT_DATE))
  AND d.hs_v2_date_entered_24595561 IS NULL
  AND d.hs_v2_date_entered_24595564 IS NULL
  AND d.ORIGEM = 'Prospecção'
  AND d.CN IN ('1134248428', '84342335', '493569292', '331668616', '465298555', '175077773', '149768337')
  AND d.CLASSIFICACAO_TAMANHO_DA_EMPRESA___PIPO IN ('P (81-200)', 'M (201-600)', 'G (601+)', 'Enterprise')
  AND (d.ORIGEM_MICRO NOT IN ('M&A - Convenia | Parcerias', 'Não se aplica | Oportunidade de FC', 'M&A - Fidati | Parcerias', 'Parceria - Fidati | Parcerias') OR d.ORIGEM_MICRO IS NULL)
  AND (d.ARCHIVED = 'false' OR d.ARCHIVED = FALSE)
  AND DATEDIFF('day', d.hs_v2_date_entered_24595562, CURRENT_DATE) > m.mediana_con_sql
ORDER BY cavaleiro, atraso DESC LIMIT 10
```

### Estrutura do comentário por cavaleiro

Gerar o texto do comentário com base nos dados coletados e atualizar a coluna `Comentários` no Notion junto com `QTD Atual` e `Data Atualização`.

**Formato padrão (2-3 frases):**
```
{realizado} SAOs de {meta} ({%pace}% do pace · {tendência}{variacao_pp}pp).
{Frase sobre funil — gargalo ou destaque principal}.
{Frase sobre alerta específico — lead/deal atrasado, se houver}.
```

**Regras por cavaleiro:**

**Inbound:**
- Frase 2: mencionar total de leads conectados no Q2 e taxa de conversão Con→SQL vs. histórico. Se alguma origem está abaixo do histórico, citar qual.
- Frase 3: se houver leads atrasados acima da mediana, citar empresa e dias de atraso (top 2 no máximo). Se não houver, omitir a frase 3.

Exemplo:
> *"2 SAOs de 38 (25% do pace · ↓ -15pp). 21 leads conectados no Q2 — Indicação convertendo 20% vs. 75% histórico, Levantada 18% vs. 56%. PetroReconcavo parado há 15 dias (+11 dias acima da mediana)."*

**SDR Outbound:**
- Frase 2: mencionar se há SAOs e de onde vieram (pipeline do Q2 ou anterior). Citar consultor com melhor e pior desempenho se relevante.
- Frase 3: se houver deals críticos acima da mediana, citar consultor e top 2 empresas. Se não houver, omitir.

Exemplo:
> *"3 SAOs de 18 (75% do pace · ↓ -75pp). SAOs vieram de pipeline anterior ao Q2 — nenhum SQL dos conectados neste trimestre ainda. Letícia com 4 deals críticos: GRUPO ENFOK e DIMENSA (+11 dias acima da mediana)."*

**EV Outbound:**
- Mesma lógica do SDR Outbound, adaptada para EV.

Exemplo:
> *"1 SAO de 12 (50% do pace · ↑ +50pp). SAO veio de pipeline anterior ao Q2. Breno com 1 em SQL — gargalo em SQL→SAO. Marcelo: Sympla parado há 16 dias (+9 dias acima da mediana)."*

**Parcerias:**
- Frase 2: mencionar funil (conectados, taxa de conversão). Se conversão está acima ou abaixo do histórico.
- Frase 3: se volume está baixo, mencionar isso como ponto de atenção. Se houver leads atrasados, citar.

Exemplo:
> *"1 SAO de 10 (50% do pace · ↑ +50pp). Funil com boa conversão (50% Con→SQL, 100% SQL→SAO) — problema é volume: apenas 6 leads conectados no Q2."*

## Slack — Notificação

**Canal:** `#area-clientes-líderes` (ID: `C03GCAU7Q3Y`)

**Mensagem:**
```
🗓️ <!channel> A tabela de métricas do Cafezinho foi atualizada!
Os números do trimestre estão fresquinhos no Notion. Agora é com vocês — por favor, incluam os comentários e destaques da semana diretamente no Notion. ☕
👉 https://www.notion.so/piposaude/Caf-Semanal-Lideran-a-de-Clientes-1664744bd803808b8364ebaa295c1ff4
```

> Usar a ferramenta `Slack:slack_send_message` com o channel_id `C03GCAU7Q3Y`.

---

## Passo a Passo de Execução

1. **Determinar trimestre vigente** via `DATE_TRUNC('quarter', CURRENT_DATE)` no Snowflake
2. **Buscar dados HubSpot** (Clientes, MRR, Leads, SQLs, SAOs) — usar `total` retornado pela API
3. **Rodar queries Snowflake** (Reuniões, Comitês, Ações, Estratégicas, Implantações, CSAT, Churn, Cotações G+, Cotações P&M, Cotações PLC, Conversão G+, Conversão P&M, Receita Operadoras, NRR)
4. **Rodar queries Snowflake — SAOs por Cavaleiro** (Inbound, SDR Outbound, EV Outbound, Parcerias) — seção "5. Snowflake — SAOs por Cavaleiro"
5. **Rodar queries auxiliares de cavaleiro** — pace, leads atrasados Inbound, deals atrasados SDR/EV — seção "Geração de Comentários"
6. **Aplicar regras de formatação** antes de enviar ao Notion
7. **Atualizar Notion** — para cada page_id do trimestre vigente, chamar `notion-update-page` com `QTD Atual` e `date:Data Atualização:start = hoje`. Para indicadores `[GD - SAOs]`, incluir também `Comentários` com o texto gerado conforme estrutura da seção "Geração de Comentários"
8. **Enviar mensagem no Slack** no canal `C03GCAU7Q3Y`

---

## Notas Importantes

- Indicadores **NPS** e **Turnover** são manuais — não atualizar
- Se valor nulo (ex: Churn zerado no início do trimestre), inserir `0`
- Frequência esperada: **toda segunda-feira, antes das 9h**

---

## 🔄 Manutenção a Cada Novo Trimestre

Ao virar o trimestre (ex: 1Q→2Q, 2Q→3Q), é necessário atualizar esta skill antes da primeira execução. Siga os passos abaixo:

### Passo 1 — Criar nova tabela no Notion

A nova tabela de métricas precisa existir na página do Cafezinho antes de qualquer atualização. Normalmente ela é criada manualmente pela liderança. Confirme com o time se a tabela do novo trimestre já foi criada.

### Passo 2 — Descobrir os novos Page IDs

Cada linha da tabela no Notion tem um Page ID único. Para descobri-los, rode o seguinte bloco e peça para Claude listar os IDs:

```
Busque todos os page IDs da tabela [NQ] do Cafezinho no Notion.
Collection ID: collection://[ID DA NOVA COLEÇÃO]
```

O Collection ID aparece na URL da tabela quando você clica em "Open as full page" no Notion, ou pode ser obtido via `notion-fetch` na página principal do Cafezinho:
- URL da página principal: `https://www.notion.so/piposaude/Caf-Semanal-Lideran-a-de-Clientes-1664744bd803808b8364ebaa295c1ff4`

### Passo 3 — Atualizar esta skill

Substitua o bloco **"Mapeamento de Page IDs"** pelo novo trimestre com os IDs corretos. O bloco a atualizar está na seção `## Notion — Configuração` acima, identificado pela linha:

```
### Mapeamento de Page IDs — [TRIMESTRE ATUAL]
```

Troque também o nome do trimestre no título da seção.

### Passo 4 — Atualizar a tabela de trimestres

Na seção `### Tabelas por trimestre`, adicione a linha do novo trimestre:

| Trimestre | Collection ID |
|---|---|
| 1Q26 | `collection://33b4744b-d803-81ac-a143-000b38d1750a` |
| 2Q26 | `collection://2ea4744b-d803-8112-aa0d-000bec58fbfa` |
| **[NOVO]** | `collection://[NOVO ID]` |

### Passo 5 — Verificar feriados nas queries de Cotação

A CTE de `Holidays` tem feriados hardcoded até 2026. Se estiver virando para 2027, adicionar os feriados variáveis (Carnaval, Semana Santa, Corpus Christi) do novo ano na lista de datas fixas.

### Referência: padrão de nomes dos indicadores por trimestre

Os nomes dos indicadores nas linhas do Notion seguem o mesmo padrão a cada trimestre — apenas o campo `Meta` muda. Os Page IDs são únicos por tabela e precisam sempre ser mapeados novamente. Use esta referência para confirmar que todos os 28 indicadores foram mapeados:

1. Clientes Ganhos G+
2. Clientes Ganhos P&M
3. Clientes Ganhos Total
4. MRR Ganhos G+
5. MRR Ganhos P&M
6. MRR Ganhos Total
7. Leads Conectados G+
8. Leads Conectados P&M
9. Leads Conectados Total
10. Qualificações Realizadas G+
11. Qualificações Realizadas P&M
12. Qualificações Realizadas Total
13. SAOs G+
14. SAOs P&M
15. SAOs Total
16. Reuniões de Resultado Realizadas
17. Comitês de Saúde Realizados
18. Ações de Alto Valor Realizadas
19. Reuniões com Personas Estratégicas
20. % Implantações no Prazo
21. CSAT Implantação
22. Churn Realizado
23. [G+] Cotações Entregues Dentro do Prazo
24. [P/M] Cotações Entregues Dentro do Prazo
25. % Cotações Aceitas pelo time de Placement com 100 dias de antecedência
26. [G+] Conversão de Estudos em Vendas
27. [P/M] Conversão de Estudos em Vendas
28. Receita com Operadoras (AG+Premiação)
29. % Retenção de Receita
30. [GD - SAOs] Inbound
31. [GD - SAOs] SDR Outbound
32. [GD - SAOs] EV Outbound
33. [GD - SAOs] Parcerias
