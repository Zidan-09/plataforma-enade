# Documentação técnica --- Plataforma de Simulados ENADE

Esta documentação é a referência técnica compartilhada pela equipe e
pelos agentes de IA durante o desenvolvimento.

## Objetivo

Construir uma plataforma web na qual administradores importam e revisam
questões de provas anteriores do ENADE, montam simulados e os
disponibilizam para alunos. Os alunos realizam cada prova uma única vez
e podem consultar gabarito e desempenho após a finalização, conforme as
configurações da avaliação.

## Como navegar

  --------------------------------------------------------------------------------------------
  Documento                                                Finalidade
  -------------------------------------------------------- -----------------------------------
  [PROJECT.md](PROJECT.md)                                 Visão, escopo, atores e objetivos

  [ARCHITECTURE.md](architecture/ARCHITECTURE.md)          Arquitetura, camadas e dependências

  [MODULES.md](architecture/MODULES.md)                    Responsabilidades e limites dos
                                                           módulos

  [DATABASE.md](architecture/DATABASE.md)                  Modelo lógico e invariantes de
                                                           persistência

  [PDF_PROCESSING.md](architecture/PDF_PROCESSING.md)      Pipeline de extração textual e OCR

  [FUNCTIONAL.md](requirements/FUNCTIONAL.md)              Requisitos funcionais

  [NON_FUNCTIONAL.md](requirements/NON_FUNCTIONAL.md)      Requisitos não funcionais e
                                                           critérios

  [BUSINESS_RULES.md](requirements/BUSINESS_RULES.md)      Regras de negócio verificáveis

  [CODING_STANDARDS.md](development/CODING_STANDARDS.md)   Padrões de código e organização

  [TESTING.md](development/TESTING.md)                     Estratégia e níveis de teste

  [CONTRIBUTING.md](development/CONTRIBUTING.md)           Como contribuir

  [GIT_WORKFLOW.md](devops/GIT_WORKFLOW.md)                Branches, commits e Pull Requests

  [CI_CD.md](devops/CI_CD.md)                              Pipeline de integração e deploy

  [QUALITY_GATES.md](devops/QUALITY_GATES.md)              Critérios mínimos de qualidade

  [AGENTS.md](../AGENTS.md)                                Regras obrigatórias para agentes de
                                                           IA

  [ADRs](decisions/)                                       Histórico de decisões arquiteturais
  --------------------------------------------------------------------------------------------

## Estado das decisões

Os documentos registram a arquitetura acordada até o momento. Decisões
que dependem de experimento, plano de hospedagem ou confirmação da
equipe estão explicitamente marcadas como **PENDENTE DE VALIDAÇÃO**. Não
trate uma proposta técnica como fato já comprovado.

## Princípios

1.  Regras de negócio críticas são executadas no servidor.
2.  O domínio não depende de Next.js, React, Prisma ou bibliotecas de
    terceiros.
3.  A prova publicada e as tentativas concluídas devem manter
    consistência histórica.
4.  Toda alteração relevante passa por revisão e verificações
    automatizadas.
5.  Os agentes não podem alterar requisitos ou decisões arquiteturais
    unilateralmente.
6.  A documentação deve evoluir junto com o código.

## Como propor uma mudança

1.  Identifique o documento e a decisão afetados.
2.  Explique o contexto, o problema e as alternativas.
3.  Registre uma proposta em `decisions/` no formato ADR.
4.  Solicite revisão humana.
5.  Após aprovação, atualize os documentos relacionados e implemente a
    mudança.
