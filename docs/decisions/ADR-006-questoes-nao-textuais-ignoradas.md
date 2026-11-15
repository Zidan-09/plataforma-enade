# ADR-006 --- Extração ignora questões com elementos não textuais

-   **Status:** Accepted
-   **Data:** 2026-11-15
-   **Responsáveis:** equipe do projeto

## Contexto

As provas do ENADE podem conter questões com figuras, imagens, tabelas,
diagramas e outros elementos gráficos. A documentação inicial não definia
como o pipeline de extração devia lidar com esse conteúdo, e a fixture de
testes mencionava "questões com imagens ou formatação incomum, se
suportadas", deixando o suporte em aberto.

A decisão de produto é fechar esse gap: a extração automática deve
processar apenas questões integralmente textuais.

## Decisão

Questões que possuam figuras, imagens, tabelas ou qualquer elemento não
textual são **ignoradas** na extração. O pipeline processa apenas questões
100% textuais.

Concretamente:

-   O parser não tenta extrair enunciado, alternativas ou numeração de
    questões que contêm elementos gráficos.
-   Questões ignoradas são registradas com estado explícito e motivo, para
    auditoria e contagem.
-   A revisão administrativa não pode aprovar uma questão ignorada como
    questão oficial.
-   Questões textuais contidas no mesmo PDF continuam sendo extraídas
    normalmente.

## Alternativas consideradas

-   **Extrair também elementos gráficos:** exigiria modelagem de mídia
    (storage, snapshot, revisão visual), estender o parser a tabelas e
    figuras, e ampliar RNF03 a um escopo muito maior. Alto custo, prazo e
    risco, sem evidência de que seja requisito inicial.
-   **Ignorar questões não textuais:** escopo mínimo, reduz risco de
    precisão e mantém o pipeline focado em texto. Desvantagem: questões
    com figuras não entram no banco sem ação manual explícita.
-   **Usar IA generativa para interpretar figuras/tabelas:** viola a
    restrição inicial de não depender de IA na primeira versão e introduz
    custo e variabilidade.

## Consequências

### Positivas

-   Escopo de extração bem delimitado e testável.
-   Precisão (RNF03) mede apenas questões textuais, sem ruído de
    elementos gráficos.
-   Revisão humana foca em questões textuais; não há risco de aprovar
    questões parcialmente extraídas.
-   Simplifica o parser e o modelo de dados.

### Negativas / riscos

-   Questões com figuras/tabelas do ENADE não entram automaticamente no
    banco; exigem tratamento manual separado pela equipe.
-   A heurística de detecção de "elemento não textual" pode gerar falsos
    positivos (ex.: figura pequena que é apenas ícone) ou falsos
    negativos (ex.: elemento gráfico mal detectado pelo pdfjs).
-   O pipeline precisa de um mecanismo de registro do motivo de
    ignoramento para auditoria.

## Validação

-   Unit test: parser retorna estado IGNORED com motivo quando a região
    contém imagem/tabela; retorna normalmente quando 100% textual.
-   Fixture de teste: PDF com questão textual + questão com figura → apenas
    a textual é extraída; a de figura é registrada como ignorada.
-   Revisar a heurística de detecção contra um conjunto representativo de
    PDFs reais e ajustar limiares conforme necessário.