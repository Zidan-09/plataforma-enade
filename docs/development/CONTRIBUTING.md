# Guia de Contribuição

## 1. Antes de começar

-   Consulte esta documentação.
-   Leia o requisito e as regras de negócio relacionados.
-   Verifique se existe Issue no Kanban/GitHub.
-   Confirme dependências e contratos com o responsável pelo módulo.

## 2. Durante a implementação

-   Trabalhe em branch própria.
-   Mantenha o escopo da Issue.
-   Não altere contratos de outros módulos sem alinhamento.
-   Escreva testes junto com a implementação.
-   Atualize documentação quando houver mudança de comportamento ou
    decisão.
-   Não adicione dependências sem justificar sua necessidade.

## 3. Antes de abrir Pull Request

Executar localmente: - lint; - verificação TypeScript; - testes
unitários relevantes; - testes de integração quando aplicável; - build
de produção quando aplicável.

Descrever o que foi implementado, como testar e quais riscos permanecem.

## 4. Revisão

O autor não aprova sozinho sua própria mudança. O revisor deve
conferir: - critérios de aceite; - regras de negócio; - limites entre
módulos; - segurança; - testes; - migrações; - efeitos em
funcionalidades existentes.

## 5. Definition of Done

-   [ ] Critérios de aceite atendidos.
-   [ ] Testes adicionados/atualizados.
-   [ ] Lint e TypeScript aprovados.
-   [ ] Sem segredos ou dados sensíveis no diff.
-   [ ] Documentação atualizada.
-   [ ] Revisão aprovada.
-   [ ] CI aprovada.
