# Estratégia de Testes

## 1. Ferramentas

-   Vitest: testes unitários e parte dos testes de integração.
-   Playwright: testes E2E em navegador.
-   PostgreSQL de teste: integração real com constraints e transações.
-   ESLint e TypeScript: verificações estáticas.

## 2. Testes unitários

Priorizar domínio e casos de uso: - Transições de estado de prova. -
Validação de publicação. - Exatamente uma alternativa correta. - Uma
tentativa por aluno/prova. - Resposta vinculada à questão correta. -
Regras de divulgação. - Parser de questões com exemplos pequenos. -
Normalização de texto extraído.

Testes de domínio não devem precisar de Next.js ou banco real.

## 3. Testes de integração

Validar: - Repositórios Prisma. - Constraints UNIQUE. - Transações de
publicação. - Concorrência ao iniciar tentativa. - Persistência de
respostas. - Finalização idempotente. - Leitura e gravação de
importações.

Utilizar PostgreSQL de teste compatível com o banco de produção. Mocks
não comprovam comportamento de constraints ou transações.

## 4. Testes E2E

Fluxos mínimos: 1. ADMIN autentica. 2. ADMIN envia PDF. 3. Sistema
processa e apresenta resultado. 4. ADMIN revisa questões e define
gabarito. 5. ADMIN cria e publica prova. 6. STUDENT autentica e
visualiza prova publicada. 7. STUDENT inicia prova e responde. 8.
STUDENT finaliza. 9. STUDENT consulta resultado/gabarito conforme
configuração. 10. Segundo início da mesma prova é bloqueado. 11. Aluno
não acessa telas ou operações administrativas. 12. Prova indisponível
não pode ser iniciada.

## 5. Fixtures

Manter PDFs de teste autorizados e anonimizados quando necessário em
`tests/fixtures/`. Não versionar documentos protegidos ou material cuja
redistribuição não seja permitida.

Incluir casos: - PDF digital com texto. - PDF escaneado. - PDF misto. -
Questões com imagens ou formatação incomum, se suportadas. - Documento
inválido/corrompido. - Questão com alternativa ausente ou ambígua.

## 6. Cobertura

A cobertura deve orientar a identificação de lacunas, não ser tratada
isoladamente como prova de qualidade. Definir metas após baseline
inicial. Regras críticas devem ter testes explícitos, inclusive cenários
negativos.

## 7. Critério de conclusão

Uma tarefa só pode ser concluída quando: - testes relevantes passam; -
novos cenários críticos foram adicionados; - lint e TypeScript passam; -
critérios de aceite foram verificados; - limitações conhecidas estão
documentadas.
