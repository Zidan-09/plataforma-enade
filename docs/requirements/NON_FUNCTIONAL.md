# Requisitos Não Funcionais

  -----------------------------------------------------------------------
  ID                      Requisito               Critério / validação
  ----------------------- ----------------------- -----------------------
  RNF01                   Usabilidade             Interface clara,
                                                  consistente e
                                                  responsiva em desktop,
                                                  tablet e celular.
                                                  Validar fluxos com
                                                  usuários e breakpoints
                                                  definidos.

  RNF02                   Desempenho              Processar PDF
                                                  compatível de até 50
                                                  questões em até 30
                                                  segundos. Medir em
                                                  ambiente documentado e
                                                  com dataset
                                                  representativo.

  RNF03                   Precisão                Alcançar pelo menos 90%
                                                  de acerto na
                                                  identificação e
                                                  estruturação de
                                                  enunciados e
                                                  alternativas em PDFs
                                                  compatíveis. Avaliar
                                                  contra dataset
                                                  revisado.

  RNF04                   Segurança               Senhas com hash
                                                  criptográfico adequado
                                                  e funcionalidades
                                                  administrativas
                                                  restritas a ADMIN
                                                  autenticado.

  RNF05                   Disponibilidade         Meta de 99% durante
                                                  operação, excluindo
                                                  manutenção programada.
                                                  A disponibilidade
                                                  depende também de
                                                  Vercel, banco, storage
                                                  e serviços externos.

  RNF06                   Compatibilidade         Testar versões estáveis
                                                  recentes de Chrome,
                                                  Firefox, Edge e Safari.
  -----------------------------------------------------------------------

## Plano de validação

### RNF01

-   Testar navegação por teclado.
-   Verificar responsividade em resoluções representativas.
-   Validar mensagens de erro e estados de carregamento.
-   Evitar depender apenas de cor para comunicar estado.

### RNF02 e RNF03

-   Criar conjunto de PDFs de referência.
-   Documentar hardware/plano, número de páginas e características dos
    PDFs.
-   Executar múltiplas medições.
-   Reportar mediana e pior caso observado.
-   Separar PDFs digitais de PDFs que exigem OCR.
-   Não excluir silenciosamente falhas do cálculo.

### RNF04

-   Testar autorização negativa.
-   Verificar armazenamento de hash, nunca senha em texto puro.
-   Verificar que gabarito não aparece em respostas, HTML, logs ou
    payloads do aluno durante a prova.
-   Executar Snyk e revisão de segurança.

### RNF05

-   Monitorar disponibilidade da aplicação e dependências.
-   Definir estratégia de backup e recuperação do PostgreSQL.
-   Documentar manutenção e incidentes.
-   Tratar 99% como objetivo operacional a ser medido, não como garantia
    automática da Vercel.

### RNF06

-   Executar testes E2E nos navegadores suportados quando viável.
-   Verificar layout, autenticação e fluxo de prova.
