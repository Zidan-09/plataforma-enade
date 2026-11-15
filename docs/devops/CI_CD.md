# CI/CD

## 1. Objetivo

Automatizar validações em Pull Requests e promover somente alterações
aprovadas para produção.

## 2. Workflow de CI

Disparar em Pull Requests para `main` e, conforme configuração, em push
para `main`.

Etapas: 1. Checkout. 2. Configurar versão Node.js definida pelo projeto.
3. Instalar dependências usando lockfile (`npm ci`, se npm for o
gerenciador escolhido). 4. ESLint. 5. TypeScript (`tsc --noEmit`). 6.
Testes Vitest. 7. Testes de integração com PostgreSQL de serviço. 8.
Build Next.js. 9. SonarQube analysis e Quality Gate. 10. Snyk test.

A equipe deve definir quais etapas são obrigatórias para toda PR e quais
podem executar em workflow separado para controlar tempo e custo.
Segurança crítica e checks de qualidade não devem ser ignorados.

## 3. Deploy

A integração GitHub--Vercel pode criar previews para Pull Requests e
deploy de produção após merge na branch principal.

Evitar manter um workflow GitHub Actions que duplique desnecessariamente
o mecanismo de deploy nativo da Vercel. Se Actions for responsável por
disparar deploy, documentar claramente a autoridade e evitar deploy
concorrente.

## 4. Migrações

-   Versionar migrations Prisma.
-   Não editar migrations já aplicadas em ambientes compartilhados.
-   Revisar migrations destrutivas.
-   Aplicar migrations de produção por etapa controlada.
-   Fazer backup antes de alterações arriscadas.
-   Não executar `db push` como substituto de migrations em produção.

## 5. Segredos

Configurar secrets e variáveis nos ambientes corretos do GitHub/Vercel.
Usar credenciais distintas para desenvolvimento, preview e produção
quando possível. Nunca imprimir secrets nos logs.

## 6. Rollback

Documentar como reverter deploy e como lidar com migrations não
retrocompatíveis. Preferir mudanças de banco em etapas compatíveis com a
versão anterior da aplicação.
