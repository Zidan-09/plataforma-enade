# ADR-002 --- PostgreSQL e Prisma

-   **Status:** Proposed
-   **Data:** 2026-11-15
-   **Responsáveis:** equipe do projeto

## Contexto

O domínio contém relações entre usuários, provas, questões,
alternativas, tentativas e respostas. Há invariantes que dependem de
transações e constraints relacionais.

## Decisão

Adotar PostgreSQL como banco relacional e Prisma como ORM, sujeito à
validação da compatibilidade da versão escolhida com Next.js e o
ambiente de deploy.

## Alternativas consideradas

-   Banco documental: menos adequado às relações e constraints centrais.
-   SQL com driver/query builder: maior controle, mas exige mais
    implementação manual.
-   Outros ORMs: possíveis, sem vantagem identificada até o momento.

## Consequências

### Positivas

-   Integridade referencial e constraints.
-   Transações.
-   Integração TypeScript.
-   Migrations versionadas.

### Negativas / riscos

-   Necessidade de configurar conexões/pooling para serverless.
-   Modelagem e migrations exigem revisão.

## Validação

Criar protótipo com constraints de tentativa única, transação de
publicação e ambiente de preview/produção.
