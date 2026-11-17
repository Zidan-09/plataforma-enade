# Estratégia de Sprints — Kanban

Documento de estratégia para validação do gestor. O gestor direciona cada uma das 12 tarefas (cards do Product Backlog) para os desenvolvedores.

## 1. Premissas

- Equipe: **4 desenvolvedores + 1 gestor**.
- Total: **12 tarefas** (cards do `docs/gestors/PRODUCT BACKLOG.pdf`).
- Cota por desenvolvedor: **3 tarefas** no total (12 ÷ 4).
- Ritmo: **3 sprints de 1 semana cada**.
- Vazão planejada: **4 tarefas por sprint** (1 por desenvolvedor por sprint).
- Colunas do quadro (conforme `docs/devops/GIT_WORKFLOW.md`): `Backlog → Ready → In Progress → In Review → Testing → Done`.

## 2. Papéis

| Papel | Responsabilidade |
|---|---|
| Desenvolvedor implementador | Implementa a tarefa, abre PR, resolve apontamentos do review e dos testes. |
| Desenvolvedor testador (sempre diferente do implementador) | Implementa/atualiza os testes da tarefa de outro desenvolvedor, conforme `docs/development/TESTING.md`. |
| Gestor | Distribui as tarefas, acompanha o quadro, executa o `code_review` final e aprova o `Done`. |

O gestor não acumula implementação nem testes; atua como revisor final e desbloqueador.

## 3. Ciclo de vida de cada tarefa

Toda tarefa percorre o mesmo pipeline, sem pular etapas:

1. **Ready → In Progress:** implementador assume 1 tarefa por vez. Branch curta por tarefa (`feat/<assunto>`, `fix/<assunto>`).
2. **In Progress → In Review:** implementador abre PR com objetivo, Issue, evidências e riscos (padrão de PR do `GIT_WORKFLOW.md`).
3. **In Review → Testing:** um desenvolvedor **diferente** do implementador assume o cartão e implementa os testes (unitários/integração/E2E conforme aplicável). Branch sugerida: `test/<assunto>`.
4. **Testing → Done:** gestor faz o `code_review` final, verifica critérios de aceite e aprova o merge na `main`. Sem aprovação do gestor, o cartão não fecha.

Regra de ouro: **quem implementou não testa a própria tarefa; quem testou não aprova — o gestor aprova.**

## 4. Rodízio de testes

Para garantir que todos testem o código de todos e evitar pares fixos:

- O testador de uma tarefa é sempre um desenvolvedor diferente do implementador.
- O gestor define o rodízio no início de cada sprint (sugestão: rotação circular Dev1 → Dev2 → Dev3 → Dev4 → Dev1).
- Ninguém testa duas tarefas do mesmo implementador na mesma sprint, salvo exceção autorizada pelo gestor e registrada no cartão.

## 5. Distribuição por sprint (a preencher pelo gestor)

Cada desenvolvedor implementa **1 tarefa** e testa **1 tarefa de outro colega** por sprint. O gestor preenche as tabelas abaixo a partir dos 12 cards do Product Backlog.

### Sprint 1 — Semana 1 (4 tarefas)

| # | Tarefa (card do backlog) | Implementa | Testa | Status |
|---|---|---|---|---|
| 1 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 2 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 3 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 4 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |

Meta de saída: 4 tarefas em `Done` (implementadas + testadas + revisadas pelo gestor).

### Sprint 2 — Semana 2 (4 tarefas)

| # | Tarefa (card do backlog) | Implementa | Testa | Status |
|---|---|---|---|---|
| 5 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 6 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 7 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 8 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |

Meta de saída: acumulado de 8 tarefas em `Done`.

### Sprint 3 — Semana 3 (4 tarefas)

| # | Tarefa (card do backlog) | Implementa | Testa | Status |
|---|---|---|---|---|
| 9 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 10 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 11 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |
| 12 | _a definir pelo gestor_ | _Dev_ | _Dev (≠ implementador)_ | `Ready` |

Meta de saída: 12 tarefas em `Done`. Cada desenvolvedor soma 3 implementações + participação nos testes.

## 6. Regras operacionais

- **WIP limit:** 1 tarefa em `In Progress` e 1 em `Testing` por pessoa. Não puxar tarefa nova com a anterior pendente de review/teste.
- **Cartão completo:** descrição, critérios de aceite, responsável (implementador + testador) e vínculo com requisito/RF, conforme padrão do Kanban.
- **Branches e PRs:** sem push direto na `main`; PR com checks de CI verdes e pelo menos 1 aprovação (a do gestor conta como final).
- **Bloqueios:** cartão parado há mais de 1 dia útil vai para o gestor com motivo e proposta de desbloqueio.

## 7. Definition of Done (resumo)

Nada vai para `Done` sem o gestor confirmar:

- Critérios de aceite atendidos.
- Testes relevantes passando (novos cenários críticos incluídos).
- Lint e TypeScript passando.
- `code_review` do gestor aprovado.
- Limitações conhecidas documentadas no cartão/PR.

Referência completa: `docs/development/TESTING.md` e `docs/devops/QUALITY_GATES.md`.

## 8. Validação pendente do gestor

- [ ] Confirmar os 4 nomes (Dev1–Dev4) e registrar na tabela de cada sprint.
- [ ] Distribuir os 12 cards do Product Backlog nas 3 sprints (ordem de prioridade).
- [ ] Definir o rodízio de testadores da Sprint 1.
- [ ] Confirmar cerimônias mínimas (ex.: planejamento segunda, review/sexta).
