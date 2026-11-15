# ADR-003 --- Autenticação e autorização

-   **Status:** Proposed
-   **Data:** 2026-11-15
-   **Responsáveis:** equipe do projeto

## Contexto

O sistema possui dois perfis: ADMIN e STUDENT. Senhas devem ser
armazenadas com hash criptográfico e operações administrativas devem ser
protegidas.

## Decisão

Utilizar uma solução de autenticação compatível com Next.js que ofereça
sessões seguras e integração server-side. Auth.js é a opção inicial a
avaliar. Hash de senha com Argon2id se a aplicação gerenciar credenciais
diretamente.

A autorização será baseada em role e aplicada no servidor em cada caso
de uso/operação sensível.

## Alternativas consideradas

-   Auth.js: integração com ecossistema Next.js; validar estratégia de
    credenciais e persistência.
-   Serviço gerenciado de identidade: reduz responsabilidade
    operacional, mas adiciona dependência externa.
-   Implementação própria de sessão: maior controle e maior risco/custo
    de segurança.

## Consequências

### Positivas

-   Papéis explícitos.
-   Autorização centralizável.
-   Separação entre autenticação e regras dos módulos.

### Negativas / riscos

-   Configuração incorreta de sessão pode comprometer o sistema.
-   Fluxo de recuperação de senha e provisionamento de ADMIN ainda
    precisa ser definido.

## Validação

Revisar documentação atual da biblioteca escolhida, testar sessão,
logout, CSRF, cookies e autorização negativa.
