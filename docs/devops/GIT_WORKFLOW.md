# Git e GitHub Workflow

## 1. Modelo

Utilizar GitHub Flow simplificado: - `main`: branch protegida e
implantável. - branches curtas por tarefa. - Pull Request para integrar
alterações.

## 2. Branches

Formato:

``` text
feat/<assunto>
fix/<assunto>
test/<assunto>
docs/<assunto>
refactor/<assunto>
chore/<assunto>
```

Exemplos: - `feat/pdf-import` - `feat/exam-publication` -
`fix/duplicate-attempt` - `test/question-parser`

## 3. Commits

Seguir Conventional Commits:

``` text
<type>(<scope>): <description>
```

Tipos comuns: - feat - fix - docs - test - refactor - chore - ci - build

Exemplos: - `feat(exams): implement exam publication` -
`fix(assessments): prevent duplicate attempts` -
`test(pdf): cover scanned document parsing` -
`docs(architecture): document module boundaries`

Preferir commits pequenos, coerentes e reversíveis.

## 4. Pull Requests

Toda PR deve informar: - objetivo e contexto; - Issue relacionada; -
mudanças realizadas; - evidências/testes; - migrações e variáveis
novas; - riscos e limitações; - impacto em requisitos ou arquitetura.

## 5. Proteção da main

Configurar: - proibição de push direto; - aprovação de pelo menos um
integrante diferente do autor; - checks obrigatórios de CI; - resolução
de conversas antes do merge; - histórico consistente.

## 6. Kanban

Colunas sugeridas:
`Backlog → Ready → In Progress → In Review → Testing → Done`

Cada cartão deve ter descrição, critérios de aceite, responsável e
vínculo com requisito quando aplicável.
