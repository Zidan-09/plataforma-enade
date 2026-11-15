# Arquitetura da Aplicação

## 1. Decisão arquitetural

Adotar **Monólito Modular**, implementado em Next.js com App Router e
TypeScript, organizado por módulos de negócio e com separação pragmática
em camadas.

Não adotar microsserviços neste escopo. O processamento de PDF poderá
ser executado por um worker separado caso os limites da Vercel tornem
isso necessário; essa separação operacional não exige transformar todo o
sistema em microsserviços.

## 2. Stack acordada / proposta

  -----------------------------------------------------------------------
  Área                    Tecnologia              Situação
  ----------------------- ----------------------- -----------------------
  Linguagem               TypeScript              Definida

  Aplicação web           Next.js App Router      Definida

  UI                      React                   Definida pelo Next.js

  Estilização             Tailwind CSS            Proposta

  Componentes             shadcn/ui               Proposta

  Validação               Zod                     Proposta

  Persistência            PostgreSQL              Definida

  ORM                     Prisma                  Proposta

  Autenticação            Auth.js ou solução      Pendente de validação
                          equivalente             

  Hash de senha           Argon2id                Proposta

  Extração textual        pdfjs-dist              Proposta

  OCR                     Tesseract.js            Proposta

  Testes unitários        Vitest                  Definida

  Testes de navegador     Playwright              Recomendado

  Lint                    ESLint                  Definida

  Qualidade estática      SonarQube               Definida

  Segurança de            Snyk                    Definida
  dependências                                    

  CI                      GitHub Actions          Definida

  Deploy                  Vercel                  Definida
  -----------------------------------------------------------------------

A equipe deve escolher versões estáveis compatíveis no início da
implementação e registrá-las no lockfile. Não utilizar versões
flutuantes em produção.

## 3. Camadas

### Presentation

Responsável por: - Páginas e layouts do Next.js. - Componentes React. -
Server Actions e Route Handlers. - Validação de formato e transformação
de entrada. - Conversão dos resultados de aplicação em respostas
apropriadas.

Não deve conter regras de negócio complexas nem acessar Prisma
diretamente.

### Application

Responsável por: - Casos de uso. - Orquestração de operações. - DTOs de
entrada e saída. - Coordenação de transações por meio de
portas/abstrações. - Verificação de pré-condições da operação.

Não deve depender de componentes React ou detalhes do Next.js.

### Domain

Responsável por: - Entidades e objetos de valor. - Estados e transições
válidas. - Invariantes e regras de negócio. - Contratos de repositório
quando necessários.

Não importa Next.js, React, Prisma, Zod ou bibliotecas de
infraestrutura.

### Infrastructure

Responsável por: - Implementações de repositórios. - Prisma e
PostgreSQL. - Armazenamento de arquivos. - Adaptadores de PDF e OCR. -
Integrações externas.

## 4. Direção das dependências

-   Presentation pode chamar Application.
-   Application pode depender de Domain e de contratos.
-   Domain não depende das demais camadas.
-   Infrastructure implementa contratos definidos pelo domínio ou
    aplicação.
-   Composition roots/factories conectam implementações concretas.

Evitar dependências circulares entre módulos. Um módulo não deve
importar diretamente detalhes internos de outro módulo. A comunicação
deve ocorrer por contratos públicos, casos de uso ou serviços de
aplicação explicitamente definidos.

## 5. Estrutura de diretórios

``` text
src/
├── app/
│   ├── (auth)/
│   ├── (admin)/
│   ├── (student)/
│   ├── api/
│   ├── layout.tsx
│   └── globals.css
├── modules/
│   ├── identity/
│   ├── exams/
│   ├── questions/
│   ├── pdf-processing/
│   ├── assessments/
│   └── results/
├── shared/
│   ├── components/
│   ├── errors/
│   ├── infrastructure/
│   ├── types/
│   └── utils/
└── lib/
    └── config/

prisma/
├── schema.prisma
└── migrations/

tests/
├── integration/
├── e2e/
└── fixtures/
```

Estrutura interna sugerida para cada módulo:

``` text
module-name/
├── domain/
│   ├── entities/
│   ├── value-objects/
│   ├── enums/
│   ├── errors/
│   └── repositories/
├── application/
│   ├── use-cases/
│   ├── dto/
│   └── services/
├── infrastructure/
│   ├── persistence/
│   └── adapters/
└── presentation/
    ├── components/
    ├── actions/
    └── schemas/
```

Criar somente diretórios necessários. Não criar arquivos vazios para
simular uma arquitetura completa.

## 6. Next.js: regras de implementação

-   Preferir Server Components quando não houver necessidade real de
    estado/interação no cliente.
-   Usar Client Components apenas para interatividade que dependa do
    navegador.
-   Server Actions e Route Handlers são pontos de entrada, não camadas
    de negócio.
-   Validar entradas no servidor mesmo que exista validação no
    formulário.
-   Verificar autenticação e autorização em cada operação sensível.
-   Não confiar em middleware/proxy como única proteção.
-   Não expor segredos, gabaritos ou dados privados em props, HTML, logs
    ou respostas de API.
-   Evitar importação de módulos server-only em componentes client.
-   Isolar operações de Node.js, OCR e processamento de arquivos em
    módulos incompatíveis com Edge Runtime.

## 7. Operações críticas

As seguintes operações devem ser transacionais ou protegidas por
restrições de banco: - Publicação de prova. - Início de tentativa
única. - Registro de resposta. - Finalização da tentativa e cálculo do
resultado. - Persistência do resultado de extração revisado.

## 8. Escalabilidade pragmática

Começar com uma única aplicação implantada na Vercel e PostgreSQL
gerenciado. Armazenar PDFs em object storage, não no filesystem efêmero
da função.

O worker de PDF deve ser desacoplado da requisição. A execução poderá
inicialmente usar infraestrutura compatível com a Vercel, mas a decisão
final depende de teste de duração, memória, CPU e limites do plano
contratado. Se necessário, hospedar apenas o worker em serviço separado.

## 9. Observabilidade

Registrar logs estruturados para: - Identificador de requisição. -
Identificador de importação PDF. - Etapa e duração do processamento. -
Erros de integração. - Falhas de autenticação/autorização relevantes. -
Falhas de publicação e finalização.

Nunca registrar senhas, tokens, conteúdo sensível de sessão ou gabaritos
em logs comuns.
