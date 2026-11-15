# Regras de Negócio

## RN01 --- Liberação de prova

Uma prova só pode ser publicada após revisão administrativa e quando
todas as questões possuírem resposta correta registrada.

Antes de publicar, validar: - prova em estado permitido para
publicação; - metadados obrigatórios; - ao menos uma questão, se
confirmado como requisito; - ordem das questões válida; - enunciados não
vazios; - alternativas válidas; - exatamente uma alternativa correta por
questão.

A validação e a mudança de status devem ser protegidas contra
concorrência.

Após publicação, o conteúdo e o gabarito ficam congelados. Para editar,
o administrador deve retirar a prova de disponibilidade. Alterações no
banco reutilizável de questões não podem modificar o snapshot da prova.

## RN02 --- Acesso às provas

Aluno só pode consultar e iniciar provas com status PUBLISHED. DRAFT,
REVIEW e UNAVAILABLE não podem ser iniciadas nem aparecer nas listagens
de aluno.

A autorização deve ser aplicada no servidor em todas as operações, não
apenas na interface.

## RN03 --- Uma tentativa por aluno/prova

Cada aluno pode ter no máximo uma tentativa por prova. A regra deve ser
garantida por constraint UNIQUE no banco e tratamento de conflito na
aplicação.

A política de retomada de uma tentativa IN_PROGRESS após logout,
fechamento do navegador ou falha de rede precisa ser definida pela
equipe. A retomada não cria nova tentativa.

## RN04 --- Respostas durante a avaliação

-   O aluno só pode responder questões pertencentes à tentativa ativa.
-   A alternativa selecionada deve pertencer à questão correspondente.
-   O servidor não envia a indicação da alternativa correta durante a
    prova.
-   Respostas podem ser atualizadas enquanto a tentativa estiver
    IN_PROGRESS.
-   Tentativa COMPLETED não aceita alterações comuns.

## RN05 --- Finalização e correção

A finalização deve ocorrer no servidor e ser idempotente. Uma segunda
submissão não pode gerar outra tentativa ou duplicar resultado.

A correção usa o snapshot da prova e é calculada no servidor.

## RN06 --- Divulgação

As configurações `showAnswerKeyAfterSubmission` e
`showPerformanceAfterSubmission` são independentes.

Após a finalização, cada informação é disponibilizada somente se a
configuração correspondente permitir. Não inferir que a prova precisa
ser encerrada para todos os alunos antes da divulgação, pois essa regra
não foi especificada.

## RN07 --- Histórico

Edições posteriores no banco de questões não podem alterar o conteúdo,
gabarito ou resultado de tentativas já realizadas. Provas e tentativas
devem manter referências ao conteúdo congelado utilizado.

## RN08 --- Importação de PDF

Extração concluída não equivale a revisão concluída. Questões extraídas
devem permanecer em estado intermediário até a revisão administrativa.
