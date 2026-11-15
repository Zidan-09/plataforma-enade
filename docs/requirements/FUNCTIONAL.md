# Requisitos Funcionais

## Autenticação e usuários

-   **RF01 --- Autenticação:** autenticar administradores e alunos com
    credenciais individuais e controlar acesso conforme perfil.

## Importação e questões

-   **RF02 --- Upload de PDF:** permitir ao administrador enviar PDFs
    contendo provas do ENADE.
-   **RF03 --- Extração automática:** identificar enunciados, numeração
    e alternativas, preservando ordem e associação. **Apenas questões
    100% textuais; questões com figuras, imagens, tabelas ou outros
    elementos não textuais são ignoradas.**
-   **RF04 --- Visualização:** apresentar questões extraídas para
    revisão administrativa.
-   **RF05 --- Edição:** permitir corrigir numeração, enunciado e
    alternativas, além de incluir ou excluir alternativas.
-   **RF06 --- Gabarito:** permitir registrar a alternativa correta e
    impedir publicação quando houver questão sem resposta correta.

## Provas

-   **RF07 --- Cadastro:** salvar prova revisada com ano, curso e área,
    sem publicação automática.
-   **RF08 --- Listagem:** aluno visualiza exclusivamente provas
    publicadas/disponíveis.

## Realização e resultados

-   **RF09 --- Responder prova:** selecionar prova, visualizar questões,
    registrar respostas, navegar e finalizar.
-   **RF10 --- Persistir respostas:** associar respostas ao aluno,
    tentativa, prova e questão.
-   **RF11 --- Gabarito e desempenho:** permitir ao administrador
    configurar divulgação após finalização.
-   **RF12 --- Persistência:** persistir usuários, provas, questões,
    alternativas, gabaritos e respostas.

## Critério de rastreabilidade

Cada requisito deve estar associado a: - pelo menos uma Issue; - um ou
mais casos de uso; - critérios de aceite; - testes que comprovem o
comportamento.

A equipe não deve marcar requisito como concluído apenas porque a tela
existe.
