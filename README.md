# Arquitetura de Execução Controlada para NL2SQL

Este repositório documenta a arquitetura proposta no TCC para execução segura de consultas em aplicações NL2SQL.

## Ideia central
A LLM é tratada como componente não confiável. Ela não executa SQL livremente. Em vez disso, produz uma intenção estruturada que passa por validação, políticas determinísticas, compilação controlada e execução auditável.

## Pipeline proposto
Usuário → LLM → intenção estruturada → normalizador/resolvedor → policy engine → compilador por templates → executor controlado → resposta com evidência

## Componentes
### 1. Interpretador de intenção
Responsável por transformar a pergunta em uma estrutura padronizada, como JSON ou AST.

### 2. Normalizador e resolvedor
Resolve datas relativas, códigos, nomes e definições de métricas.

### 3. Policy Engine
Aplica regras de autorização, escopo, allowlist, limites e validação estrutural.

### 4. Compilador Intenção → SQL
Gera SQL de forma controlada, com templates fixos e parâmetros bindados.

### 5. Executor controlado
Executa a consulta com conexão read-only, timeout, limite de linhas e trilha de auditoria.

### 6. Resposta com evidência
Retorna o resultado acompanhado do SQL final, filtros aplicados e definição da métrica usada.

## Objetivo da arquitetura
Reduzir a dependência de SQL livre gerado pela LLM e aumentar:
- segurança
- auditabilidade
- previsibilidade
- governança
- reprodutibilidade

## Estrutura do repositório
- `docs/arquitetura.md`
- `docs/componentes.md`
- `docs/fluxo.md`
- `diagramas/`
- `prototipo/`
- `exemplos/`

## Aplicação
Arquitetura proposta como base prática do meu TCC sobre segurança em aplicações NL2SQL.

## Status
Em desenvolvimento.
