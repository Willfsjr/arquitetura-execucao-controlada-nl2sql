# Fluxo da Execução Controlada

## Etapa 1 — Entrada do usuário
O usuário envia uma pergunta em linguagem natural.

Exemplo:
“Qual foi o lucro do produto X no último semestre?”

## Etapa 2 — Geração de intenção
A LLM interpreta a pergunta e produz uma estrutura intermediária, como:

- métrica: lucro
- entidade: produto X
- período: último semestre
- tipo de saída: agregado temporal ou total

## Etapa 3 — Normalização
O sistema resolve ambiguidades:
- converte datas relativas
- resolve identificadores
- valida definições de negócio

## Etapa 4 — Aplicação das políticas
O policy engine verifica:
- se o papel do usuário permite essa métrica
- se o escopo é compatível com empresa, filial, tenant ou período
- se os objetos solicitados estão no allowlist
- se a estrutura pretendida respeita as regras
- se os limites de execução estão dentro da política

## Etapa 5 — Compilação controlada
Se a intenção for aprovada, o sistema gera SQL a partir de templates previamente autorizados.

## Etapa 6 — Execução
O executor controlado roda a consulta em ambiente read-only, com timeout, limite de linhas e logging.

## Etapa 7 — Resposta com evidência
O sistema devolve:
- resultado
- SQL final
- filtros aplicados
- definição da métrica
- ou recusa com justificativa resumida
