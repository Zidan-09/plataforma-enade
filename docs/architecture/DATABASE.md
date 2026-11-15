# Modelo de Dados --- Visão Lógica

Este documento descreve entidades e invariantes. O schema Prisma
definitivo deve ser produzido após revisão da equipe e dos
relacionamentos.

## 1. Entidades

### User

-   id
-   name
-   email (único)
-   passwordHash
-   role: ADMIN \| STUDENT
-   createdAt
-   updatedAt

### Exam

-   id
-   title
-   year
-   course
-   area (se aplicável)
-   status: DRAFT \| REVIEW \| PUBLISHED \| UNAVAILABLE
-   showAnswerKeyAfterSubmission
-   showPerformanceAfterSubmission
-   createdBy
-   createdAt
-   updatedAt
-   publishedAt

### Question

-   id
-   statement
-   sourceNumber (opcional)
-   reviewStatus
-   createdAt
-   updatedAt

### Alternative

-   id
-   questionId
-   label
-   content
-   isCorrect

A regra de exatamente uma alternativa correta deve ser validada no
domínio e na persistência quando tecnicamente possível. A publicação
exige que cada questão utilizada tenha uma única resposta correta.

### ExamQuestion

Associação ordenada entre Exam e Question: - id - examId - questionId -
position - snapshotVersion ou referência à versão congelada

Restrições: - UNIQUE(examId, position) - Evitar duplicação da mesma
questão na mesma prova, salvo decisão explícita em contrário.

### ExamQuestionSnapshot / ExamQuestionAlternative

Representa o conteúdo imutável usado na prova: - enunciado congelado. -
número/posição exibidos. - alternativas congeladas e seus
identificadores/rótulos. - indicação da alternativa correta preservada
em armazenamento server-side.

O snapshot não deve ser enviado integralmente ao aluno. A camada de
apresentação deve construir DTO sem gabarito.

### Attempt

-   id
-   examId
-   studentId
-   status: IN_PROGRESS \| COMPLETED
-   startedAt
-   submittedAt
-   score (opcional, calculado no servidor)
-   UNIQUE(studentId, examId)

A restrição única é obrigatória para impedir tentativas duplicadas
inclusive sob concorrência.

### AttemptAnswer

-   id
-   attemptId
-   examQuestionId ou snapshotQuestionId
-   selectedAlternativeId (nullable enquanto não respondida)
-   answeredAt
-   UNIQUE(attemptId, examQuestionId)

A referência deve apontar para a alternativa do snapshot, não para uma
alternativa mutável da questão original.

### PdfImport

-   id
-   originalFileName
-   storageKey
-   status: PENDING \| PROCESSING \| COMPLETED \| FAILED
-   errorCode (opcional)
-   errorMessage sanitizada (opcional)
-   pageCount (opcional)
-   startedAt
-   completedAt
-   createdBy
-   createdAt

### ExtractionResult / ExtractedQuestion

Armazena o resultado intermediário: - importId - número detectado -
enunciado detectado - alternativas detectadas - página de origem -
método utilizado (TEXT/OCR) - alertas e confiança, se mensurável -
estado de revisão

## 2. Relacionamentos principais

-   User 1:N Exam (createdBy).
-   User 1:N Attempt.
-   Exam 1:N ExamQuestion.
-   Question 1:N Alternative.
-   Exam 1:N Attempt.
-   Attempt 1:N AttemptAnswer.
-   PdfImport 1:N ExtractedQuestion.
-   ExamQuestion 1:1 snapshot da questão utilizada.

## 3. Invariantes

1.  E-mail do usuário é único.
2.  Somente ADMIN executa operações administrativas.
3.  Prova publicada contém ao menos uma questão válida (confirmar mínimo
    exigido pelo trabalho).
4.  Cada questão da prova possui alternativas válidas e exatamente uma
    correta.
5.  Prova publicada não pode ter conteúdo ou gabarito alterado.
6.  Um aluno possui no máximo uma tentativa por prova.
7.  Uma resposta pertence à tentativa e à questão daquela prova.
8.  Tentativa concluída não pode ser modificada por operações comuns.
9.  A correção usa o snapshot da prova, não o banco mutável de questões.
10. Gabarito não é retornado durante a realização da prova.

## 4. Transações e concorrência

-   Início de tentativa: inserir Attempt e tratar conflito da constraint
    UNIQUE; não usar apenas consulta prévia.
-   Publicação: validar e alterar status na mesma transação, protegendo
    contra alterações concorrentes.
-   Finalização: validar tentativa, persistir submissão, calcular
    resultado no servidor e marcar COMPLETED de forma atômica.
-   Resposta: aceitar somente questão e alternativa pertencentes à
    tentativa/prova autenticada.

## 5. Índices sugeridos

-   User(email) UNIQUE.
-   Attempt(studentId, examId) UNIQUE.
-   AttemptAnswer(attemptId, examQuestionId) UNIQUE.
-   Exam(status, publishedAt).
-   ExamQuestion(examId, position) UNIQUE.
-   PdfImport(status, createdAt).

## 6. Decisões pendentes

-   Se curso/área serão tabelas de domínio ou campos textuais.
-   Se a plataforma aceitará questões discursivas no futuro.
-   Política de exclusão/anonimização de usuários.
-   Retenção e exclusão dos PDFs originais.
-   Se haverá limite de tempo por prova.
