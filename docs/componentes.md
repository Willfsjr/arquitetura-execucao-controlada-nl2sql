# Componentes da Arquitetura

## C1 — Interpretador de intenção

Responsável por receber a pergunta em linguagem natural e produzir uma intenção estruturada em formato controlado, como JSON ou AST.

### Função
- interpretar a solicitação do usuário
- identificar entidades, métricas e filtros
- produzir uma representação padronizada

### Restrição
- não deve gerar SQL livre diretamente

## C2 — Normalizador/Resolver

Responsável por resolver elementos ambíguos ou relativos antes da aplicação das políticas.

### Exemplos
- transformar “último semestre” em intervalo de datas concreto
- resolver código de produto ou cliente
- validar o significado de métricas como “lucro” ou “margem”

## C3 — Policy Engine

É o núcleo da arquitetura e do TCC.

### Responsabilidades
- aplicar RBAC
- impor escopo obrigatório
- validar allowlist de tabelas, colunas e views
- bloquear padrões estruturais indevidos
- impor limites de execução
- decidir allow ou deny

## C4 — Compilador Intenção → SQL

Transforma a intenção validada em SQL seguro e previsível.

### Regras
- uso de templates controlados
- bind variables obrigatórias
- ausência de concatenação livre
- geração compatível com objetos permitidos

## C5 — Executor controlado

Executa a consulta no banco com restrições operacionais e trilha de auditoria.

### Controles
- conexão read-only
- timeout
- limite de linhas
- logging estruturado
- registro de erros

## C6 — Resposta com evidência

Responsável por apresentar o resultado de forma auditável.

### Elementos esperados
- resultado analítico
- SQL final executado
- filtros aplicados
- definição da métrica utilizada
- justificativa resumida em caso de recusa
