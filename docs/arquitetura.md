# Arquitetura de Execução Controlada para NL2SQL

## Visão geral

Esta arquitetura foi proposta para reduzir o risco de prompt injection e de ações indevidas em aplicações NL2SQL.

O princípio central é simples: a LLM não é tratada como autoridade de execução. Ela não gera SQL livre para ser executado diretamente. Em vez disso, a LLM apenas produz uma intenção estruturada, que será validada por componentes determinísticos antes de qualquer execução no banco.

## Pipeline de alto nível

Usuário → LLM → intenção estruturada → normalizador/resolvedor → policy engine → compilador por templates → executor controlado → resposta com evidência

## Objetivos da arquitetura

- reduzir dependência de SQL livre gerado pela LLM
- impedir ações indevidas no banco
- reforçar controle de escopo e autorização
- tornar a execução auditável
- aumentar previsibilidade e reprodutibilidade

## Princípios

### 1. LLM como componente não confiável
A LLM pode errar, alucinar ou ser induzida por prompt injection. Por isso, sua saída deve ser tratada como proposta, não como decisão final.

### 2. Intenção estruturada antes de SQL
A aplicação trabalha com uma representação intermediária, como JSON ou AST, antes da geração do SQL.

### 3. Políticas determinísticas antes da execução
Toda autorização, escopo, allowlist, limite e validação estrutural deve ser aplicada por componentes determinísticos.

### 4. SQL gerado de forma controlada
O SQL final deve ser compilado a partir de templates autorizados, com parâmetros bindados.

### 5. Resposta com evidência
A saída ao usuário deve incluir elementos que aumentem transparência, como SQL final, filtros aplicados e definição de métrica.
