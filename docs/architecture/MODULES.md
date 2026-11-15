# Módulos e Limites de Responsabilidade

## 1. Identity

Responsabilidades: - Autenticação. - Sessões. - Usuários e perfis
ADMIN/STUDENT. - Autorização e políticas de acesso.

Não é responsabilidade de Identity decidir se uma prova pode ser
publicada; isso pertence a Exams.

## 2. Exams

Responsabilidades: - Cadastro e metadados da prova. - Estado da prova. -
Associação ordenada de questões. - Configurações de divulgação de
gabarito e desempenho. - Publicação e retirada de disponibilidade.

Regras de publicação devem ser aplicadas por caso de uso e domínio,
nunca apenas pela interface.

## 3. Questions

Responsabilidades: - Banco reutilizável de questões. - Enunciados e
alternativas. - Definição da alternativa correta. - Revisão e validação
da questão. - Versionamento/snapshot do conteúdo utilizado em provas.

Questions não deve publicar provas.

## 4. PDF Processing

Responsabilidades: - Receber solicitação de importação. - Validar
arquivo e metadados. - Extrair texto e executar OCR quando necessário. -
Identificar questões e alternativas. - Armazenar resultados preliminares
e alertas. - Permitir reprocessamento.

O resultado da extração é uma sugestão para revisão. Não é
automaticamente uma questão aprovada nem uma prova publicada.

## 5. Assessments

Responsabilidades: - Iniciar tentativa. - Garantir uma tentativa por
aluno/prova. - Entregar questões sem gabarito. - Registrar respostas. -
Finalizar tentativa.

Não deve confiar em pontuação calculada pelo navegador.

## 6. Results

Responsabilidades: - Corrigir tentativas no servidor. - Calcular
desempenho. - Aplicar configurações de divulgação. - Disponibilizar
gabarito e resultado somente quando permitido.

## 7. Contratos entre módulos

-   PDF Processing entrega questões extraídas em formato intermediário
    para revisão pelo fluxo de Questions.
-   Exams referencia versões/snapshots das questões selecionadas.
-   Assessments consome a versão publicada da prova, sem acesso ao
    gabarito no DTO enviado ao aluno.
-   Results usa a resposta registrada e a versão correta preservada no
    snapshot.
-   Identity fornece identidade autenticada e perfil; cada módulo
    continua responsável por autorizar suas próprias operações.

## 8. Proibições

-   Importar diretamente arquivos internos de outro módulo.
-   Acessar Prisma diretamente em componentes ou Server Actions.
-   Duplicar regras de publicação em várias telas.
-   Fazer o módulo PDF persistir questões aprovadas ignorando o fluxo de
    revisão.
-   Expor gabarito por meio de endpoints de listagem ou detalhe
    destinados ao aluno.
