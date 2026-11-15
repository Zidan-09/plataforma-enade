# ADR-005 --- Estratégia de testes

-   **Status:** Accepted
-   **Data:** 2026-11-15
-   **Responsáveis:** equipe do projeto

## Contexto

A plataforma possui regras críticas de autorização, publicação,
tentativa única, persistência e correção. Testes unitários isolados não
comprovam constraints e fluxos reais.

## Decisão

Utilizar: - Vitest para testes unitários e parte dos testes de
integração; - PostgreSQL real em testes de integração de
persistência/transações; - Playwright para fluxos E2E no navegador; -
ESLint e TypeScript para análise estática.

## Alternativas consideradas

-   Apenas Vitest com mocks: rápido, mas não valida comportamento real
    do banco ou navegador.
-   Apenas E2E: lento e insuficiente para localizar falhas de domínio.
-   Estratégia em camadas: melhor equilíbrio entre velocidade e
    confiança.

## Consequências

### Positivas

-   Testes próximos da regra de negócio.
-   Validação de constraints reais.
-   Cobertura de jornadas críticas.

### Negativas / riscos

-   Mais configuração e tempo de CI.
-   Necessidade de manter ambiente de teste.

## Validação

Configurar pipeline e garantir testes para publicação, tentativa única,
autorização e divulgação de resultados.
