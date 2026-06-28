# Segurança

O ADUI é uma superfície de execução agentica. Segurança, consentimento e
auditoria fazem parte do produto, não são complementos.

## Regras iniciais

- Não comitar segredos ou dados reais.
- Não registrar payloads sensíveis sem mascaramento.
- Não permitir que agentes executem ações críticas sem confirmação explícita.
- Não executar ações como `USER`; sessões agenticas usam `actor_type = AGENT`.
- Não criar ferramentas sem ACL e trilha de auditoria.

## Ações críticas bloqueadas por padrão

- Exclusões críticas.
- Pagamentos.
- Movimentações financeiras.
- Alteração de permissões.
- Criação, exclusão ou elevação de usuários.
- Alteração de preço sem confirmação.
- Cancelamento em lote.

## Relato de falhas

Falhas de segurança devem ser tratadas como prioridade alta e documentadas com:

- escopo afetado;
- modo de reprodução;
- impacto;
- mitigação proposta;
- evidência sem dados sensíveis.
