# Visão do Projeto

## 1. Resumo

A Plataforma de Simulados ENADE é uma aplicação web para administrar um
banco de questões extraídas de provas anteriores, montar avaliações e
permitir que alunos realizem simulados.

O sistema terá dois perfis: **ADMIN** e **STUDENT**. A decisão atual não
contempla um perfil separado de professor. Caso a equipe queira essa
distinção, deverá alterar os requisitos e registrar uma decisão
arquitetural.

## 2. Objetivos

-   Permitir autenticação individual e autorização por perfil.
-   Receber PDFs de provas do ENADE.
-   Extrair automaticamente enunciados, numeração e alternativas de PDFs
    digitais e, quando necessário, de páginas digitalizadas por OCR.
-   Permitir revisão e correção manual das questões extraídas.
-   Manter um banco reutilizável de questões.
-   Permitir que administradores montem, revisem e publiquem provas.
-   Permitir que alunos realizem provas disponíveis uma única vez.
-   Registrar respostas e disponibilizar gabarito e desempenho conforme
    configuração da prova.
-   Demonstrar práticas de DevOps, qualidade, segurança e colaboração.

## 3. Atores

### ADMIN

Pode, conforme autorização do servidor: - Gerenciar provas e questões. -
Enviar PDFs e acompanhar importações. - Revisar e corrigir questões
extraídas. - Definir a alternativa correta. - Montar provas e controlar
disponibilidade. - Configurar divulgação de gabarito e desempenho.

### STUDENT

Pode: - Consultar somente provas publicadas. - Iniciar uma prova
disponível se ainda não possuir tentativa. - Navegar pelas questões e
registrar respostas. - Finalizar a avaliação. - Consultar gabarito e
desempenho quando liberados.

## 4. Fora do escopo inicial

Salvo alteração aprovada: - Perfil de professor separado de
administrador. - Múltiplas tentativas para a mesma prova. - Aplicativo
mobile nativo. - Correção de questões discursivas. - Plataforma de
videoconferência ou aulas. - Microsserviços e backend independente. -
Uso obrigatório de IA generativa para extração. - Garantia de extração
perfeita sem revisão humana.

## 5. Premissas

-   A aplicação será web e utilizará Next.js com TypeScript.
-   A arquitetura será um monólito modular.
-   O banco relacional será PostgreSQL, acessado por Prisma.
-   A aplicação será implantada na Vercel, sujeita à validação dos
    limites operacionais.
-   O repositório e o fluxo de colaboração utilizarão Git e GitHub.
-   OpenCode será utilizado como ferramenta de agentes de IA.
-   A extração combinará PDF.js para texto e Tesseract.js para OCR,
    inicialmente.

## 6. Critérios de sucesso

-   Fluxos de administrador e aluno funcionam com autorização no
    servidor.
-   Provas não podem ser publicadas sem revisão e gabarito completo.
-   Um aluno não consegue iniciar duas tentativas para a mesma prova.
-   Respostas corretas não são expostas durante a realização.
-   Questões e resultados históricos permanecem consistentes após
    edições no banco de questões.
-   CI executa verificações de qualidade e segurança.
-   RNF de tempo e precisão de extração são medidos com um conjunto de
    PDFs de teste representativo.
