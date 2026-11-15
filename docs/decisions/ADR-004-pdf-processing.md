# ADR-004 --- Extração textual e OCR para PDFs

-   **Status:** Proposed
-   **Data:** 2026-11-15
-   **Responsáveis:** equipe do projeto

## Contexto

O sistema deve processar PDFs digitais e documentos digitalizados, com
meta de até 30 segundos para até 50 questões e precisão mínima de 90% em
arquivos compatíveis.

## Decisão

Adotar pipeline híbrido determinístico: - pdfjs-dist para extração
textual; - Tesseract.js para páginas sem texto utilizável; - parser
determinístico para estruturar questões e alternativas; - revisão
administrativa antes de salvar questões oficiais.

## Alternativas consideradas

-   Apenas texto: não atende documentos digitalizados.
-   OCR em todas as páginas: custo maior e possível perda de qualidade
    em PDFs digitais.
-   IA generativa como parser obrigatório: custo, latência,
    variabilidade e dependência externa.
-   Pipeline híbrido: aproveita texto nativo e usa OCR quando
    necessário.

## Consequências

### Positivas

-   Processamento local sem custo por token.
-   Maior previsibilidade.
-   Revisão humana corrige ambiguidades.

### Negativas / riscos

-   Layouts variados exigem evolução do parser.
-   OCR pode consumir CPU/memória e ultrapassar limites serverless.
-   Precisão depende do conjunto de documentos.

## Validação

Construir dataset rotulado, medir precisão e tempo, e testar em ambiente
representativo da Vercel. Decidir fila e worker após o experimento.
