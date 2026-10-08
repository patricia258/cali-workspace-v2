# CALI Workspace V2 — Handoff mestre técnico, funcional e visual
**Data-base:** 08/10/2026 · **Status:** desenvolvimento inicial de homologação · **Aprovação:** conceito visual direcional aprovado; implementação final e produção NÃO aprovadas.

> Documento vivo. O conteúdo desta V2 nunca substitui automaticamente decisões do Workspace vigente. Toda migração precisa preservar contrato, histórico, permissões e rastreabilidade.

## 1. Propósito e não objetivos
O CALI Workspace é a plataforma de acompanhamento da assessoria estratégica de pessoas da CALI RH (HRB — RH para o Negócio). A CALI atua como People Advisory externa, e não como sistema de rotinas de DP ou HRIS completo. A administradora registra e conduz; o cliente acompanha, participa, valida, aprova e avalia aquilo a que tem direito. A experiência da V2 deve comunicar senioridade consultiva, decisões, cronologia e valor percebido.

**Não fazer:** clonar código, identidade, conteúdo, módulos ou arquitetura da Bizneo; assumir que a referência HCM representa o produto CALI; inventar dados executivos; trocar banco ou autenticação sem auditoria; criar módulos de ponto, férias, folha, denúncias, avaliação 360° ou outros somente porque aparecem nas imagens de referência.

**Regra visual decisiva:** não construir todas as páginas a partir de uma linha de 4 a 6 cards no topo. Dashboard = mesa de trabalho, Horas = extrato consultivo, Equipe = diretório + estrutura + indicadores, Avaliações só se houver serviço/escopo validado. Cards são pontuais, não o elemento organizador universal.

## 2. Projetos, repositórios e ambientes
| Papel | Recurso | Identificador |
|---|---|---|
| Produção vigente | GitHub | https://github.com/patricia258/app.cali |
| Produção vigente | Vercel | projeto `app-cali`, domínio `https://app.calirh.com` |
| V2 homologação | GitHub | https://github.com/patricia258/cali-workspace-v2 |
| V2 homologação | Vercel | projeto `cali-workspace-v2`; criado, conectar ao GitHub antes do deploy |
| Backend oficial | Supabase | CALI MAPA: `kqtbfeeqbcllwvlkbrkq`; schema `cali_workspace` para Workspace |
| Prospecção | Supabase | CALI Prospect Compass: `jslzdfhldkjlvdfrvfmf`; não modificar |
| Legado de portal | Supabase | Portal Cali: `atvbvtayywnbbjxwetjt`, inativo; verificar dependências antes de qualquer consolidação |

**Não conectar a V2 ao Supabase de produção até existir plano de isolamento e testes autorizados.** No início, dados fictícios locais; nenhuma chave de produção, mesmo anon, no deploy demonstrativo. `VITE_DEMO_MODE=true` no desenvolvimento. Não copiar secrets, arquivos privados, clientes, e-mails ou endereços reais.

**Projeto Vercel distinto não equivale a banco distinto**. A futura conexão poderá reutilizar o mesmo Supabase oficial, mas requer contas/empresas sandbox, políticas RLS auditadas, isolamento de outbound e bloqueio explícito de efeitos colaterais (e-mail, convites, calendário, notificações, cobrança).

## 3. Estado da primeira entrega e limites
Implementado no repositório V2: aplicação Vite/React/TypeScript, tokens visuais no CSS, sidebar bordô com gradiente, navegação para 7 módulos, Visão Geral, Equipe (diretório, estrutura, movimentações, indicadores) e Horas do cliente, drawer contextual, filtros e layouts responsivos. Os módulos Calendário, Ocorrências, Documentos e Relatórios são **marcadores** e não implementações reais. Todos os dados da V2 são **fictícios**; botões indisponíveis avisam que dependem de integração. Nenhuma operação de escrita no Supabase foi incluída. UI de homologação, não substituta da produção.

Os screenshots da Bizneo e conceito visual aprovado em 08/10 guiaram compacidade, densidade, hierarquia, tabelas, modais e painéis laterais; a identidade CALI permanece própria. **A imagem-conceito é referência de direção, não especificação pixel-perfect**.

## 4. Identidade e tokens
| Token | Valor | Aplicação |
|---|---|---|
| Bordô | `#5A1E2D` | sidebar em gradiente, selecionado, links e CTA prioritário |
| Marfim | `#F7F3EE` | fundo da aplicação |
| Grafite | `#2B2B2B` | títulos e texto principal |
| Taupe | `#B7A99A` | divisórias e metadados |
| Dourado fosco | `#B58C52` | detalhes de precisão, pequenos destaques |
| Branco | `#FFFFFF` | tabelas, superfícies principais, áreas editoriais |

Só versão clara nesta fase. Preservar contraste AA nas tipografias pequenas; cores de status nunca isoladas do texto. Interface mais branca que colorida; evitar saturação em indicadores e arco-íris de badges. Wordmark editorial CALI; não inserir símbolos inventados como se fossem o logotipo oficial. Sidebar pode ser estreita por padrão e expandir com interação. No desktop, ter hierarquia de 3 níveis: navegação global, abas do módulo, filtros locais. Headings e dados não devem repetir seu próprio título em 3 containers.

## 5. Componentes fundamentais — comportamento esperado
1. **Shell único:** sidebar fixa/colapsável sem remontagem, topbar discreta, responsividade, estados claros de foco, e badge de homologação fora de produção.
2. **Tabelas densas:** cabeçalho fixável se necessário, datas e valores coerentes, filtros reais, paginação, vazios informativos, seleção/ações com permissão, coluna de identidade sempre visível; horizontais longas com overflow intencional.
3. **Abas:** preservar o estado local ou documentar reset; URL/rota deep-link nas implementações definitivas.
4. **Drawer contextual:** manter fundo e contexto, foco acessível, Escape, fechamento por overlay, barra de ações fixa se longa; proteger dados sensíveis.
5. **Modal:** reserva para decisão/edição e confirmação; não aninhar modais; bloquear submit duplo; foco e scroll previsíveis.
6. **Filtros:** indicar período e estado confirmado, origem dos dados, seleção clara e opção de limpar; datas efetivas vs data de registro.
7. **Estados:** carregamento único CALI (folha/lima aprovado), skeleton só quando justificado, erro específico e retry, vazio que explique próxima ação, read-only explícito.
8. **Notificações:** links profundos para objeto correto, deduplicação, cliente só vê fatos publicados, comunicação externa com status de entrega real.
9. **Mídia:** foto ou avatar autorizado em moldura editorial; sem informações pessoais em screenshots públicos.
10. **Tema:** apenas diurno para V2 inicial. Sem introduzir alternância dia/noite nesta fase.

## 6. Jornada administrativa completa (fonte atual / futura migração)
**A. Onboarding da conta:** proposta aprovada/contrato comercial → cadastro empresa/plano/contatos → termo específico de adesão à plataforma → aceite versionado e rastreável → convite e ativação de usuário cliente → configuração de visibilidade e frentes. A falta de termo verificável é lacuna atual; não transferir convite automático sem guarda de adesão.

**B. Planejamento:** empresa → projeto → escopo, frentes e calendário de ciclo → cronograma proposto → envio ao cliente → aceite/ajuste dentro da regra de prazo → ativação da execução. Projetos contêm workstreams e entregáveis; subtarefas são unidades executáveis; datas, responsáveis e dependências não devem se perder.

**C. Execução:** atividade (timer ou manual) → alocação a projeto, entregável, tarefa, reunião ou ocorrência → consolidação de horas → monitorar consumo e limites → cliente consulta em modo leitura. Registrar origem e autoria; nunca contar horas duplicadas pelo timer e lançamento manual.

**D. Interação:** evento e registro → ocorrência ou solicitação → responsáveis e SLA, comentários, anexos, transições → notificação pertinente → encerramento/avaliação/reabertura autorizada. Não transformar todo registro interno em conversa exposta ao cliente.

**E. Entrega:** documento ou entregável → revisão, envio, ajustes, aceite ou solicitação de correção → histórico e logs → eventual NPS. Versionamento, protocolo, visibility e source of truth coerentes.

**F. Relatório:** fechamento mensal/trimestral → fatos computados por período → curadoria da administradora → aprovação interna → publicação para empresa correta → leitura/ciente do cliente e histórico de revisões. Nunca preencher indicadores sem origem confiável.

**G. Renovação/encerramento:** histórico do ciclo, exportação autorizada, permissões reduzidas, retenção/descontinuação conforme contrato e política vigente. Não excluir registros por padrão.

## 7. Jornadas do cliente
Início = panorama do contrato, entregas/pendências, próximo encontro e leitura clara; Planejamento = validar cronograma e ajustes; Frentes = contratadas e oportunidades discretas sem upsell intrusivo; Horas = contratado/usado/restante, atividades e contexto; Ocorrências = solicitar e acompanhar, conversar com estado evidente, eventual reabertura; Documentos = consultar/publicações/ciência com versão; Relatórios = leitura executiva por período, reconhecimento de ciência quando aplicável; Equipe = pessoas, movimentações e indicadores conforme base/escopo autorizados. Sem telas editáveis onde produto exige somente consulta.

## 8. Pacotes: regras e pendências
- **CALI Partner:** assessoria estratégica mensal; duração oficial mínima **8 meses**. Indicadores base e leitura relevante, não um painel propositalmente inútil.
- **CALI Full:** assessoria ampliada; duração oficial mínima **12 meses**. Aprofundar indicadores por áreas/gestores, análise e recomendações **somente** se dados, escopo e finalidade aprovados.
- **CALI Build:** proposta de implementação guiada; mapa detalhado de recursos/horas, entregas e período dependem da contratação. **Não inventar** prazo mínimo, horas, preços ou matriz de direitos.
- O diferencial comercial não pode ser bloqueios arbitrários a informações básicas; permissões de visibilidade devem seguir contrato e justificativa.

## 9. Equipe: modelo e indicadores
Origem atual: `cali_workspace.team_members`, `team_member_private`, `team_changes`, `team_months`, `team_month_snapshots`, `team_month_reviews`, `team_vacancies`. Os snapshots mensais e confirmação controlam a confiabilidade. Nunca contar usuário com login como equivalente a colaborador cadastrado.

**Ficha mínima:** identificação profissional, cargo, área, gestor, vínculo, jornada, situação, admissão, localização/unidade, histórico. Remuneração e dados pessoais opcionais em tabela isolada e permissões separadas; não exibir dados de saúde, orientação sexual ou informação sensível porque está no banco. Campos contratuais de DP na referência Bizneo não são requisitos CALI.

**Movimentações:** data efetiva, tipo, origem, antes/depois, autor, período, revisão, situação; não apagar histórico de desligados; importação CSV nunca implica desligamento por ausência de linha.

**Indicadores base para revisão com negócio:** headcount por mês confirmado; entradas, saídas, saldo; distribuição por área/gestor; admissões e desligamentos; tempo de casa; quadro por vínculo. **Turnover:** acordar fórmula, denominador, intervalos, admissão/desligamento efetivos, tratamento de meses sem base e de dados incompletos. Não inferir causa voluntária/involuntária de observação livre; exigir classificação verificável, quando autorizada. Filtros de organização/segmentos precisam preservar base e sinalizar grupos pequenos ou vazios. Suprimir segmentos que facilitem reidentificação.

**Headcount e relatórios:** prioridade de valor. Interface precisa oferecer visão por período e hierarquia organizacional, comparação entre meses, drilldown, exportação e leitura qualitativa. **Escopo atual da instrução da usuária:** não reformular funcionalmente os relatórios de headcount agora, além da análise e preservação; só planejar a evolução. A V2 traz painel de dados fictícios explicitamente rotulado como prova visual, não cálculo oficial.

**Qualidade:** um único mês real confirmado não basta para validar tendência, comparação, transferência/desligamento histórico e taxa. Gerar fixtures sintéticos, testar 12 meses, mudança retroativa, fusões de áreas, gestor desligado, duplicidades, correção no mês e acessos por empresa.

## 10. Horas e agenda
A produção possui `hour_entries`, `work_timers`, `service_cycles`, `company_hours_visibility`, `hour_alerts` e RPCs de resumo. Não reimplementar fórmulas no frontend como fonte da verdade. A página do cliente deve contar, de modo editorial e com baixa carga cognitiva: plano/período, total contratado, utilizado, disponível/excedente, atividades contextualizadas, relação com entregas e observações sobre ajuste. Cliente não edita o extrato. Períodos que não possuem horas contratadas não devem receber denominador inventado.

Calendário: reduzir dimensão visual, manter eventos reais, integração Google/Meet e pedidos de remarcação com trilha. Somente mostrar sincronização confirmada. Agenda deve integrar atividade, reunião e eventual ocorrência sem duplicar itens.

## 11. Ocorrências, documentos, relatórios e avaliações
Ocorrências: protocolos, tipo, atribuição, status e SLA real, chat contextual, anexos, reabertura, notas e visibilidade; melhorar densidade visual e composer, preservando histórico. Bloquear exposição de memória interna da consultora em conversa cliente.

Documentos: preservar áreas já aprovadas; `files`, `account_documents`, `document_acknowledgements` e `drive_connections`; estados de sincronização, versões, ciência e autorização. Drive de cliente nunca é público por padrão.

Relatórios: `reports`, `report_client_events` + versões e aprovações. Resumo executivo narrativo, fatos, movimentações, riscos, decisões, horas e próximos passos; diferenças entre rascunho/publicado, PDF, ciência e logs devem coincidir. Evitar duplicar V17 ADM/V5 cliente semanticamente.

Avaliações: somente NPS/feedback já contratados e resultados autorizados; não inventar módulo de performance individual por similaridade com Bizneo.

## 12. Modelo de dados, segurança e integrações
- **Supabase:** RLS ligado não garante política correta. Testar isolamento entre empresa A/B para cada SELECT/INSERT/UPDATE/DELETE, RPC e storage; verificar acessos do administrador, cliente principal e futuro parceiro interno (papel ainda pendente).
- **Autenticação:** fluxo real de login, recuperação, sessão expirada, empresa não vinculada, convite, desativação e bloqueio por termo; provar em desktop/mobile e aba anônima.
- **Storage e documentos:** caminhos por empresa e permissão por papel, links assinados, tipos/tamanho, rastreamento de acesso.
- **Integrações:** Mapa de People, Portal de propostas, Calendar/Meet, Drive e e-mails de comunicação; inventariar edge functions, webhooks, templates, secrets e callbacks. Projeto Portal Cali no Supabase está inativo, **não inferir** que todos os formulários já foram migrados.
- **Saídas:** envio de e-mail, WhatsApp e notificações só com gatilhos validados e idempotência; `enqueued` não equivale a entregue.
- **LGPD:** finalidade, minimização, consentimento/aceite quando aplicável, retenção, exportação e exclusão sob regras documentadas; política específica do Workspace pendente de inventário jurídico.
- **Analytics:** não usar fotos/reais, dados de clientes reais ou identificadores pessoais em protótipos públicos.

## 13. Padrão de entrega / testes
| Gate | Evidência exigida |
|---|---|
| Integridade | npm install; npm run typecheck; npm run build; sem warnings bloqueadores |
| UX | Desktop 1440/1280/1024 + mobile 390; foco, teclado, scroll, back, transições e contraste |
| Controle de contexto | trocar empresa, período, aba e filtros sem deixar dados anteriores ou métricas inconsistentes |
| RLS | A não vê B; cliente não grava horas; parceiro interno vê somente empresas atribuídas quando papel existir |
| Horas | timer iniciado/pausado/cancelado, duração, fuso, mês, visibilidade e alertas 50/80 |
| Equipe | cadastro, importação com prévia, atualização, confirmação, história e indicadores de 12 meses |
| Calendário | criar/remarcar/cancelar, duplicidade e convite externo |
| Ocorrências | criar, responder, anexar, notificar, encerrar, avaliar, pedir reabertura |
| Entregas | draft/review/enviar/aprovar/ajustar/lock e protocolo |
| Documentos | upload/visibilidade/publicação/ciência/download/versão |
| Relatórios | fonte/versão/aprovação/PDF/publicação/ciência/revisão |
| Deploy | preview com dados artificiais, env mínimas, smoke test antes de qualquer domínio oficial |

### Definição de pronto por tela
1. Todos os elementos da tela existem por necessidade do fluxo, não decoração.
2. Cada indicador informa o período, origem, base e limitações.
3. Cada ação habilitada funciona de ponta a ponta, ou fica claramente desativada.
4. Sem estado falso de sucesso, sem loading infinito, sem backend adivinhado.
5. Hierarquia, navegação e densidade consistentes com design system.
6. Feedback de aceite/reprovação registrado pela CALI; aprovação não é deduzida de deploy READY.

## 14. Plano incremental
**Fase 0 (realizada):** ambiente Vercel separado criado; repositório V2 fornecido; prova React com fixtures e sem banco.
**Fase 1:** homologar shell e três telas (Visão Geral, Equipe, Horas). Ajustar densidade, cores, responsividade e componentes conforme feedback explícito.
**Fase 2:** auditar modelo e fluxos oficiais, definir contratos de API, fixtures e permissões; planejar integração isolada. Evitar clone massivo de código obsoleto.
**Fase 3:** conectar base de testes controlada; conferir autenticação e contexto multiempresa.
**Fase 4:** migrar Calendário, Ocorrências, Documentos, Relatórios e demais módulos prioritários preservando lógica; testes completos.
**Fase 5:** reconciliar dados e produção, ativar observabilidade, backup/export, rollback e aceite formal. A V2 substitui UI oficial **somente** após decisão explícita; manter domínio `app.calirh.com`.

## 15. Handoff de mudança obrigatória
Cada alteração no projeto precisa registrar: **autor**, data, commit, arquivos, motivo, impacto no fluxo, migração de banco? (sim/não), novos envs? (sim/não), testes automatizados, QA manual ADM/cliente, estado de aprovação (não enviado / aguardando / aprovado / rejeitado), rollback e próximas pendências. Não juntar mudança estética e alteração destrutiva de regras no mesmo commit.

## 16. Pendências que exigem validação humana
- Termo específico do Workspace e ativação de cliente.
- Matriz de indicadores e funcionalidades por CALI Partner, Full e Build, sem bloquear informação base.
- Fórmula de turnover, critérios de voluntário/involuntário, comparação temporal e amostras pequenas.
- Escopo da futura visão de desempenho (não existe autorização para clonar módulo Bizneo).
- Migração de formulário/Portal para Supabase principal; verificar dependências reais.
- Credenciais de teste e validação end-to-end em todas as contas/papéis.
- Publicação Vercel V2 ligada ao repositório (ambiente separado, sem secrets de produção).
- Política de armazenamento, retenção e eventual rotina de anonimização.
- Decisão sobre estrutura de relatórios de headcount — **não modificar agora**.

## 17. Fontes e precedência
1. Aprovações expressas da CALI neste projeto em 08/10/2026 (direção visual compacta e editorial; dados e fluxos conservados; só tema claro; prioridade headcount, sem mudar seu funcionamento agora).
2. GitHub produção: `docs/PRODUCT_RULES.md`, `docs/CALI_PROJECT_REFERENCES.md`, `docs/EQUIPE_EMPRESA_SPEC_2026-10-01.md`, `docs/WORKSPACE_PRIVACY_AUDIT_2026-10-01.md`, componentes V17 e V5.
3. Auditoria CALI Workspace preparada em 08/10/2026, usada como checklist não como certificação.
4. Banco Supabase CALI MAPA: tabelas e políticas existentes — verificar em live antes de qualquer integração.
5. Prints e demonstração Bizneo: **apenas** referência de UX, composição e densidade. Não são especificação funcional nem licença para copiar interface.

**Separar sempre:** observado na produção / visto no código / previsto no handoff / demonstrado artificialmente / teste pendente / aprovado pela CALI.
