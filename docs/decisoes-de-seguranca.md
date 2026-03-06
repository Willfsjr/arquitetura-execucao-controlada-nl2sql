# Decisões de Segurança da Arquitetura

## 1. Não executar SQL livre da LLM
A arquitetura rejeita a ideia de confiar diretamente no SQL produzido pelo modelo. A LLM apenas sugere intenção estruturada.

## 2. Compilação por templates
O SQL é gerado por padrões previamente definidos, reduzindo risco de estrutura inesperada ou bypass semântico.

## 3. Policy Engine como ponto central de decisão
A autorização não depende do texto do prompt nem da interpretação da LLM. A decisão de allow ou deny é tomada por regras determinísticas.

## 4. Escopo obrigatório
Mesmo que o usuário tente remover filtros, o escopo deve ser imposto pelo sistema com base no papel e no contexto autorizado.

## 5. Restrição estrutural
A arquitetura considera risco elevado em estruturas como:
- DML ou DDL
- acesso fora do allowlist
- joins não previstos
- subqueries não autorizadas
- consultas sem limite

## 6. Execução com menor privilégio
O executor atua em conexão read-only e, sempre que possível, sobre views controladas.

## 7. Auditoria como requisito funcional
Toda decisão precisa ser rastreável, inclusive consultas negadas, erros e tentativas de abuso.

## 8. Evidência como parte da resposta
A transparência da resposta é parte da governança do sistema, não apenas um detalhe de interface.
