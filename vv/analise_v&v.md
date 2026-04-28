## 1. Referencial — VER e VAL nos Modelos

**Verificação (VER)** garante que os produtos de trabalho foram construídos corretamente, conforme os requisitos especificados. No CMMI cobre desde a seleção de artefatos e estabelecimento de critérios (SP 1.x) até revisão por pares (SP 2.x) e execução/análise dos testes (SP 3.x). No MPS.BR aparece a partir do **Nível F** com três resultados de processo: preparar a verificação (VER 1), realizá-la (VER 2) e registrar defeitos (VER 3).

**Validação (VAL)** demonstra que o produto satisfará seu uso pretendido no ambiente real do cliente. No CMMI cobre seleção de produtos, estabelecimento de ambiente e critérios (SP 1.x) e execução/análise (SP 2.x). No MPS.BR aparece a partir do **Nível E** com estrutura análoga: preparar (VAL 1), realizar (VAL 2) e registrar problemas (VAL 3).

---

## 2. Evidências no Repositório

### 2.1 Verificação

**Testes automatizados (Rust CI)**
O `CONTRIBUTING.md` exige `cargo test` antes de qualquer pull request. O workflow *Rust CI* dispara a cada push e PR, executando build e testes unitários/integração. O histórico de execuções do Actions registra mais de 11 mil runs desse workflow, indicando aplicação consistente ao longo do projeto.
*Cobre: VER SP 3.1, VER SP 3.2 / VER 2 (MPS.BR)*

**Testes End-to-End e de Integração**
Existem workflows dedicados: *E2E Tests*, *Windows E2E Tests* e *Windows CLI Integration Test*. Eles exercitam fluxos completos de uso em ambientes Linux e Windows, aproximando-se de uma verificação sistêmica do produto.
*Cobre: VER SP 3.1 / VER 2 (MPS.BR)*

**Análise de qualidade de código**
O workflow *Code Quality & Optimization* executa análise estática a cada commit, tipicamente usando `clippy` (linter Rust) e `rustfmt` (formatação). Funciona como verificação contínua de conformidade com padrões de codificação.
*Cobre: VER SP 1.3, VER SP 3.1 / VER 1-2 (MPS.BR)*

**Revisão por pares via Pull Requests**
O fluxo de contribuição adota PRs com revisão antes do merge. Issues e PRs utilizam labels de categorização e prioridade (`bug`, `enhancement`, `high priority`, `medium priority`), e há histórico de comentários técnicos e solicitações de mudança.
*Cobre parcialmente: VER SP 2.1, VER SP 2.2 / VER 2 (MPS.BR)*

### 2.2 Validação

**Testing Bounties**
Para PRs relevantes, o time publica issues de bounty (ex.: issue #2037) oferecendo remuneração ($20/relatório) para que testadores externos validem as mudanças em seus próprios ambientes. Os relatórios exigem: SO e hardware utilizados, passos seguidos e resultados. Trata-se de validação efetiva em ambiente real, cobrindo configurações impossíveis de replicar internamente.
*Cobre: VAL SP 2.1, VAL SP 2.2 / VAL 2-3 (MPS.BR)*

**Feedback via Issues e Discussions**
O repositório mantém canal aberto de issues e discussões. Bugs reportados por usuários reais (como o #1501, sobre falhas no Windows) alimentam ciclos de correção e re-validação, constituindo evidência de uso do produto em ambiente real.
*Cobre: VAL SP 2.2 / VAL 3 (MPS.BR)*

---

## 3. Lacunas e Não-Conformidades

**Ausência de Plano de Verificação e Validação**
Não existe nenhum documento que defina formalmente quais artefatos serão verificados/validados, por qual técnica, com quais critérios e em qual momento do ciclo. Essa é a lacuna mais crítica em relação a ambos os modelos.
*Impacto: VER SP 1.1, 1.3 / VAL SP 1.1, 1.3 — VER 1 e VAL 1 (MPS.BR) não satisfeitos*

**Sem métricas de cobertura de testes**
Não há relatórios de code coverage integrados ao CI. Ferramentas como `cargo-tarpaulin` ou `llvm-cov` estão ausentes. Sem essa métrica, é impossível avaliar quantitativamente o quanto do código é exercitado pelos testes.
*Impacto: VER SP 3.2 prejudicado*

**Qualidade inconsistente nos Pull Requests**
Análise do histórico de PRs revela casos sem instruções de teste, com código experimental declarado explicitamente (`'DISGUSTING HACK TEMPORARY FOR MACOS'`) e sem issue associada. Um PR permaneceu aberto por mais de 34 dias sem resposta. A revisão por pares ocorre, mas sem processo padronizado.
*Impacto: VER SP 2.1 e 2.2 não atendidos formalmente*

**E2E cross-platform incompleto**
O PR #2499 (status Draft em março/2026) visa estabelecer um setup unificado de testes e2e multiplataforma. Enquanto estiver em draft, a cobertura de validação automatizada em todas as plataformas suportadas permanece incompleta.
*Impacto: VAL SP 1.2 / VAL 1 (MPS.BR) parcialmente satisfeito*

**Sem rastreabilidade requisito→teste**
Não há matriz de rastreabilidade ligando funcionalidades (descritas no README ou via issues) aos casos de teste correspondentes. Não é possível determinar, pela documentação, quais testes cobrem quais requisitos.
*Impacto: VER SP 1.3, VAL SP 1.3*

---

## 4. Quadro de Conformidade

### CMMI-DEV

| Subprática | Descrição resumida | Status |
|---|---|:---:|
| VER SP 1.1 | Selecionar produtos para verificação | ⚠️ |
| VER SP 1.2 | Estabelecer ambiente de verificação | ⚠️ |
| VER SP 1.3 | Critérios e procedimentos de verificação | ❌ |
| VER SP 2.1 | Preparar revisão por pares | ⚠️ |
| VER SP 2.2 | Conduzir revisão por pares | ⚠️ |
| VER SP 3.1 | Executar verificação | ✅ |
| VER SP 3.2 | Analisar resultados da verificação | ⚠️ |
| VAL SP 1.1 | Selecionar produtos para validação | ⚠️ |
| VAL SP 1.2 | Estabelecer ambiente de validação | ⚠️ |
| VAL SP 1.3 | Critérios e procedimentos de validação | ❌ |
| VAL SP 2.1 | Executar validação | ✅ |
| VAL SP 2.2 | Analisar resultados da validação | ⚠️ |

### MPS.BR

| Resultado de Processo | Status | Observação |
|---|:---:|---|
| VER 1 — Preparar verificação | ❌ | Sem plano formal |
| VER 2 — Realizar verificações | ✅ | CI automatizado e robusto |
| VER 3 — Registrar defeitos | ⚠️ | Issues existem, sem sistematização |
| VAL 1 — Preparar validação | ❌ | Sem plano, sem critérios formais |
| VAL 2 — Realizar validação | ✅ | Bounties e feedback de usuários |
| VAL 3 — Registrar problemas | ⚠️ | Issues registradas, análise informal |

**Legenda:** ✅ Atendido · ⚠️ Parcialmente atendido · ❌ Não atendido

---

## 5. Conclusão

O screenpipe demonstra **maturidade técnica real** em verificação e validação: CI consolidado com mais de 11 mil execuções, testes e2e em múltiplas plataformas e um mecanismo criativo de validação por usuários reais via bounties. O processo funciona na prática.

A principal lacuna está na **camada de planejamento e documentação**: os processos existem mas não estão formalizados, o que impede conformidade com os resultados VER 1 e VAL 1 de ambos os modelos. Isso é justamente o que diferencia o **CMMI Nível 2 do Nível 3** — processos gerenciados versus processos definidos e institucionalizados.

**Nível estimado:** CMMI entre Nível 2–3 · MPS.BR compatível com Nível G/F em execução, porém sem satisfazer os resultados de preparação exigidos para os Níveis F e E formalmente.