# Quality Gates

## 1. Pull Request

A PR não deve ser integrada quando ocorrer: - erro de ESLint; - erro de
TypeScript; - teste obrigatório falhando; - build falhando; - Quality
Gate do SonarQube reprovado, conforme configuração aprovada; -
vulnerabilidade bloqueante conforme política do Snyk; - ausência de
aprovação exigida.

## 2. SonarQube

Configurar análise de: - bugs; - vulnerabilidades; - code smells; -
duplicação; - cobertura importada dos relatórios de teste, quando
suportada.

Definir Quality Gate e limiares após primeira execução de baseline. Não
inventar percentual de cobertura sem considerar o projeto. Não reduzir
limiares para esconder regressões.

## 3. Snyk

Executar análise de dependências e, se habilitado, análise de
código/containers. Definir política para severidade, exploitability e
exceções. Toda exceção deve ter justificativa, responsável e prazo de
revisão.

## 4. ESLint e TypeScript

-   Sem erros de lint.
-   Sem erros de compilação/typecheck.
-   Exceções devem ser localizadas e justificadas.

## 5. Testes

-   Testes de regras críticas são obrigatórios.
-   Falhas não podem ser ignoradas ou marcadas como flaky sem Issue e
    plano de correção.
-   Testes E2E dos fluxos essenciais devem rodar antes de release.

## 6. Relatório

A PR deve apresentar status dos checks e link para os relatórios
relevantes. A equipe deve registrar decisões sobre falsos positivos e
exceções de segurança.
