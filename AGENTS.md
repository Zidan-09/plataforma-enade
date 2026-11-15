# Instruções Gerais para Agentes de IA

Este arquivo contém regras obrigatórias para qualquer agente de IA que
trabalhe neste repositório.

## 1. Fonte da verdade

Antes de planejar ou modificar código: 1. Leia `docs/README.md`. 2. Leia
`docs/PROJECT.md`. 3. Consulte os documentos de arquitetura, requisitos
e regras de negócio relevantes. 4. Consulte os ADRs relacionados.

Se documentação e código divergirem, não escolha silenciosamente.
Identifique a divergência e peça decisão humana ou proponha atualização
documentada.

## 2. Limites de atuação

-   Não alterar arquitetura, stack, requisitos ou regras de negócio
    unilateralmente.
-   Não criar microsserviços ou abstrações desnecessárias.
-   Não instalar dependências sem justificar necessidade, manutenção,
    licença e impacto.
-   Não editar arquivos fora do escopo da tarefa sem autorização.
-   Não realizar commits, pushes, merges, deploys ou alterações
    destrutivas sem autorização explícita.
-   Não modificar migrations já aplicadas em ambientes compartilhados.
-   Não desabilitar checks para fazer o pipeline passar.

## 3. Regras arquiteturais

-   Respeitar os módulos e camadas documentados.
-   Domain não importa Next.js, React, Prisma ou bibliotecas externas.
-   Presentation não acessa Prisma diretamente.
-   Server Actions e Route Handlers são adaptadores de entrada.
-   Casos de uso concentram orquestração.
-   Regras críticas são verificadas no servidor.
-   Não retornar modelos Prisma diretamente à interface.
-   Não criar dependências circulares entre módulos.

## 4. Segurança obrigatória

-   Toda operação administrativa verifica sessão e role ADMIN no
    servidor.
-   Não confiar em middleware ou UI como única autorização.
-   Nunca expor senha, hash, token ou segredo.
-   Nunca enviar resposta correta ao cliente durante a prova.
-   Validar pertencimento de tentativa, prova, questão e alternativa.
-   Tratar upload como entrada não confiável.
-   Não incluir `.env`, credenciais ou dados privados no Git.
-   Não registrar conteúdo sensível em logs.

## 5. Regras de negócio críticas

-   Somente provas publicadas são visíveis/iniciáveis por STUDENT.
-   Publicação exige prova revisada e todas as questões com exatamente
    uma alternativa correta.
-   Prova publicada deve preservar seu conteúdo por snapshot.
-   Um aluno tem no máximo uma tentativa por prova; a garantia inclui
    constraint única no banco.
-   Respostas são persistidas e validadas no servidor.
-   Tentativa concluída não pode ser alterada por operações comuns.
-   Gabarito e desempenho são liberados independentemente, conforme
    configuração.

## 6. Processo de trabalho

Para cada tarefa: 1. Entender Issue e critérios de aceite. 2.
Identificar módulos e arquivos afetados. 3. Apresentar plano curto antes
de mudanças relevantes. 4. Implementar o menor escopo que resolve o
problema. 5. Adicionar/atualizar testes. 6. Executar lint, typecheck e
testes relevantes. 7. Revisar diff em busca de regressões e arquivos
fora de escopo. 8. Atualizar documentação se necessário. 9. Relatar
arquivos alterados, testes executados, resultados e pendências.

## 7. Proibições

-   Não inventar requisitos.
-   Não afirmar que testes passaram sem executá-los.
-   Não afirmar que RNF de desempenho/precisão foi atendido sem medição.
-   Não substituir OCR por IA ou vice-versa sem decisão.
-   Não introduzir `any` indiscriminadamente.
-   Não capturar e ignorar exceções.
-   Não deixar TODO crítico sem registrar.
-   Não alterar fixtures/dados de teste para mascarar falha.

## 8. Incertezas

Quando faltar informação: - identifique a dúvida; - explique o
impacto; - proponha uma opção; - aguarde aprovação quando a decisão
alterar arquitetura, segurança, dados ou comportamento de negócio.

## 9. Relatório final

Sempre informar: - resumo do que foi feito; - arquivos alterados; -
testes executados e resultado real; - riscos ou limitações; - decisões
que exigem revisão humana.
