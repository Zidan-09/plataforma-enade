# Arquitetura de Processamento de PDFs

## 1. Objetivo

Extrair automaticamente numeração, enunciados e alternativas de PDFs de
provas do ENADE, preservando ordem e associação. A extração é assistiva:
todo resultado deve passar por revisão administrativa antes de integrar
o banco oficial de questões.

## 2. Estratégia inicial

-   `pdfjs-dist`: leitura de páginas, texto e posições quando
    disponíveis.
-   `Tesseract.js`: OCR de páginas ou regiões sem texto utilizável.
-   Parser determinístico: identificação de padrões de questão e
    alternativas.
-   Revisão humana: correção de resultados ambíguos ou incompletos.

Não utilizar IA generativa como dependência obrigatória da primeira
versão.

## 3. Pipeline

1.  Receber arquivo.
2.  Validar extensão, MIME real, tamanho e integridade.
3.  Armazenar o original em object storage.
4.  Criar registro `PdfImport` com status PENDING.
5.  Enfileirar/agendar processamento.
6.  Ler o PDF página por página.
7.  Avaliar qualidade/quantidade de texto extraído.
8.  Aplicar extração textual nas páginas adequadas.
9.  Aplicar OCR somente onde necessário.
10. Normalizar texto sem perder referência à página e ordem.
11. Identificar questões, enunciados e alternativas.
12. Registrar resultados, alertas e status.
13. Disponibilizar revisão administrativa.
14. Após revisão, enviar questões ao fluxo de Questions.

## 4. Parser

O parser deve: - Reconhecer padrões de numeração configuráveis. -
Reconhecer rótulos de alternativas (A, B, C, D, E e variações
suportadas). - Preservar quebras de parágrafo relevantes. - Associar
alternativas à questão correta. - Detectar questões incompletas e
numeração duplicada. - Registrar página de origem. - Evitar assumir que
todo marcador de letra é uma alternativa.

O parser deve ser testado com PDFs reais variados. Não presumir um único
layout para todas as edições do ENADE.

## 5. Estados

`PENDING → PROCESSING → COMPLETED`

Em falha: `PROCESSING → FAILED`. Deve existir operação explícita de
retry, com controle para evitar dois processamentos simultâneos do mesmo
import.

`COMPLETED` significa que o pipeline terminou, não que as questões foram
aprovadas.

## 6. Desempenho e precisão

RNF02 estabelece até 30 segundos para PDF compatível com até 50
questões. Medir: - tempo total; - tempo de extração textual; - tempo de
OCR; - número de páginas; - memória máxima; - quantidade de questões
detectadas.

RNF03 estabelece precisão mínima de 90%. Definir dataset de referência
revisado manualmente e medir separadamente: - detecção de questões; -
identificação de enunciados; - identificação de alternativas; -
associação correta entre questão e alternativas.

Não declarar conformidade sem dataset, metodologia e resultados
documentados.

## 7. Segurança de arquivos

-   Validar conteúdo real, não confiar apenas no nome/extensão.
-   Definir limite de tamanho e quantidade de páginas.
-   Rejeitar arquivos corrompidos ou protegidos por senha se não houver
    suporte.
-   Não executar conteúdo ativo incorporado.
-   Armazenar fora do filesystem efêmero da função.
-   Usar nomes internos aleatórios para objetos.
-   Restringir leitura e download a usuários autorizados.
-   Não expor URL pública permanente de PDFs privados.
-   Aplicar timeout, limites de memória e proteção contra abuso.

## 8. Execução assíncrona

Não manter uma requisição HTTP aberta durante OCR.

O upload cria um registro e dispara o trabalho. A execução deve ter: -
identificador idempotente; - lock/controle de concorrência; - retry
limitado; - timeout; - status persistido; - logs estruturados.

A Vercel tem limites de duração e recursos que variam por plano e
configuração. Validar o cenário real. Se o worker não cumprir os
requisitos, executar somente o worker em serviço compatível separado,
mantendo o restante da aplicação no Next.js.

## 9. Decisões pendentes

-   Provedor de object storage.
-   Mecanismo de fila/execução assíncrona.
-   Limite máximo de arquivo e páginas.
-   Suporte a PDF protegido por senha.
-   Estratégia de renderização das páginas para OCR.
-   Conjunto de PDFs de referência para avaliação.
