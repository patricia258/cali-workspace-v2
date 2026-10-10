# Handoff — Contas, decisores e acessos

## Requisito funcional confirmado
Uma empresa pode possuir mais de um decisor e mais de um usuário autorizado. Registrar, por pessoa: nome, cargo, e-mail, telefone/WhatsApp, papel (principal, decisor adicional ou acesso adicional), autorização de acesso, tipo de permissão, status da conta de acesso e relacionamento com a empresa. Permitir adicionar e remover contatos. O decisor principal pode não coincidir com todos os usuários autorizados.

## Estado da prévia
O protótipo V2 administrativo oferece edição local ilustrativa da etapa Decisores e acessos, sem persistir, criar usuários ou modificar permissões. O filtro de status simula somente os estados disponíveis nos dados demonstrativos. Os logos usam monogramas quando não há imagem de demonstração; na integração utilizar os arquivos reais do cadastro sem fabricar links.

## Trabalho necessário na integração oficial
Conferir schema Supabase, RLS e políticas de convite antes de implementar múltiplos decisores/acessos; definir vínculo, papel, ciclo de convite, alteração/revogação de acesso e auditoria. Não assumir que o modelo atual de uma única pessoa suporta múltiplos registros. Não migrar banco nem autorizar terceiros sem aprovação específica.

## Semântica de situação
Diferenciar status do contrato/conta (ativo, standby/pausado, bloqueado, inativo/encerrado, arquivado) de pendência operacional de projetos (aguardando cliente). O segundo não deve aparecer como estado contratual sem regra específica. O protótipo usa dados fictícios e não é fonte de verdade para estados reais.
