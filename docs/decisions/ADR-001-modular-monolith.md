# ADR-001 --- Arquitetura de Monólito Modular

-   **Status:** Accepted
-   **Data:** 2026-11-15
-   **Responsáveis:** equipe do projeto

## Contexto

A plataforma é uma aplicação web acadêmica com módulos de autenticação,
provas, questões, processamento de PDFs, avaliações e resultados. O
escopo não justifica a complexidade operacional de microsserviços ou de
um backend independente.

## Decisão

Adotar Next.js fullstack em arquitetura de monólito modular, com módulos
de negócio e camadas Presentation, Application, Domain e Infrastructure.

## Alternativas consideradas

-   Microsserviços: maior isolamento, porém custo operacional e
    complexidade desnecessários neste estágio.
-   Backend separado: tecnicamente possível, mas aumenta a quantidade de
    aplicações e contratos.
-   Monólito sem módulos: simples inicialmente, porém facilita
    acoplamento e mistura de responsabilidades.

## Consequências

### Positivas

-   Menor complexidade de deploy.
-   Compartilhamento de tipos e contratos TypeScript.
-   Separação lógica de responsabilidades.
-   Adequado ao tamanho inicial do sistema.

### Negativas / riscos

-   Exige disciplina para manter limites entre módulos.
-   Processamento pesado pode exigir worker separado.

## Validação

Revisar dependências entre módulos e validar o processamento PDF no
ambiente de deploy.
