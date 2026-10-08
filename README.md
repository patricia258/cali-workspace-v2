# CALI Workspace V2
Nova experiência visual de homologação do CALI Workspace. **Não é a aplicação de produção.**

## Situação
- Primeira prova funcional em React + TypeScript + Vite.
- Layout claro, editorial, bordô/marfim/dourado, tabelas compactas, sidebar gradiente.
- Jornadas demonstrativas: Visão Geral, Equipe (quatro abas) e Horas do cliente.
- Páginas de Calendário, Ocorrências, Documentos e Relatórios intencionalmente marcadas como pendentes.
- Todos os dados são **fictícios e locais**; nenhum Supabase, OAuth, envio de e-mail ou gravação.
- Status do produto: **aguardando avaliação da CALI**.

## Executar
```bash
npm install
npm run typecheck
npm run build
npm run dev
```

## Documentação obrigatória
Leia **[Handoff mestre](docs/HANDOFF_MESTRE_CALI_WORKSPACE_V2_2026-10-08.md)** antes de implementar qualquer fluxo.

## Ambientes
- Produção oficial (não alterar): https://app.calirh.com
- Repositório oficial: https://github.com/patricia258/app.cali
- Código V2: https://github.com/patricia258/cali-workspace-v2
- Vercel V2: projeto `cali-workspace-v2`, proteção de autenticação Vercel ativa.
- Supabase oficial: projeto CALI MAPA `kqtbfeeqbcllwvlkbrkq`, schema `cali_workspace`. **Não conectar nesta fase.**

## Segurança
Não usar clientes nem dados reais em homologação visual. Não adicionar credenciais ao repositório. Não publicar no domínio de produção. As regras funcionais definitivas devem ser reconciliadas com o projeto original antes de qualquer integração.

## Próximos passos
1. Avaliação e ajustes visuais da V2 pela CALI.
2. Extrair componentes e testes, consolidar rotas.
3. Inventário e contratos de APIs/roles/RLS.
4. Autenticação e testes isolados, antes dos fluxos reais.
5. Migração incremental, mantendo rollback.
