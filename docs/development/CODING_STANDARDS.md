# Padrões de Desenvolvimento

## 1. Princípios

-   SOLID aplicado com pragmatismo.
-   Clean Code e nomes expressivos.
-   DRY sem abstrações prematuras.
-   Tipagem forte; evitar `any`.
-   Composição antes de herança quando adequada.
-   Funções pequenas com responsabilidade clara.
-   Regras de negócio explícitas e testáveis.

## 2. TypeScript

-   Habilitar `strict`.
-   Evitar `any`; quando inevitável, justificar e limitar.
-   Usar `unknown` para dados externos e validar antes de utilizar.
-   Não usar non-null assertion sem justificativa.
-   Modelar estados com unions/enums em vez de strings arbitrárias.
-   Não duplicar tipos de domínio em componentes.

## 3. Nomenclatura

-   Arquivos: `kebab-case`.
-   Classes e tipos: `PascalCase`.
-   Variáveis e funções: `camelCase`.
-   Constantes: `UPPER_SNAKE_CASE` quando forem constantes globais
    reais.
-   Componentes React: `PascalCase`.
-   Use cases: verbo + objeto, por exemplo `PublishExam`.
-   Interfaces de repositório: nomes do domínio, por exemplo
    `ExamRepository`.

## 4. Domínio e aplicação

-   Entidades protegem seus invariantes.
-   Use cases representam operações observáveis do sistema.
-   DTOs não são entidades de domínio.
-   Repositórios abstraem persistência, não regras de negócio.
-   Não retornar modelos Prisma diretamente para Presentation.
-   Não colocar regra de negócio em Server Actions, componentes ou
    hooks.
-   Não criar abstração sem necessidade concreta.

## 5. Erros

-   Utilizar erros tipados para falhas esperadas de domínio/aplicação.
-   Não expor stack trace ou detalhes internos ao usuário.
-   Converter erros de infraestrutura em respostas seguras na fronteira
    da aplicação.
-   Registrar contexto técnico em logs sem incluir segredos.
-   Não ignorar exceptions silenciosamente.

## 6. Validação

-   Validar entradas externas no servidor com schema.
-   Validar novamente invariantes no domínio.
-   Não confiar em validação exclusivamente client-side.
-   Normalizar dados apenas quando isso não alterar o significado do
    conteúdo.

## 7. React e Next.js

-   Server Components por padrão.
-   Client Components somente quando necessários.
-   Componentes visuais não acessam banco.
-   Server Actions chamam casos de uso.
-   Não colocar segredo em variável `NEXT_PUBLIC_`.
-   Não utilizar Edge Runtime para dependências que exigem Node.js.

## 8. Padrões de projeto permitidos quando justificados

-   Repository: abstração de persistência.
-   Use Case: operação de aplicação.
-   Strategy: estratégias de extração TEXT/OCR.
-   Adapter: bibliotecas e serviços externos.
-   Factory: construção complexa quando necessária.
-   Dependency Injection: composição de implementações.
-   State: transições com comportamento específico.

Não introduzir padrão apenas para aumentar o número de abstrações.

## 9. Formatação e lint

-   ESLint como verificação obrigatória.
-   Executar formatter adotado pelo repositório antes do commit.
-   Não desabilitar regra global para resolver um caso local.
-   Justificar exceções com comentário curto e específico.

## 10. Segurança

-   Nunca commitar `.env` ou credenciais.
-   Nunca registrar senha, token ou segredo em logs.
-   Não confiar em IDs recebidos do cliente sem verificar autorização e
    pertencimento.
-   Não retornar gabarito a endpoints de aluno durante a avaliação.
