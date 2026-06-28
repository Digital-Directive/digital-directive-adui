# Contribuindo

Este projeto está na fase de arquitetura. Contribuições devem melhorar clareza,
contratos, segurança, governança ou plano de implementação.

## Antes de alterar

- Leia o PRD em `docs/prd/adui-prd-v1.md`.
- Preserve a decisão central: agente não manipula DOM diretamente.
- Registre mudanças arquiteturais relevantes em `docs/adr`.
- Atualize contratos JSON quando um documento depender de novos campos.

## Padrão de mudança

- Documentos devem ser objetivos e rastreáveis.
- Schemas devem ser JSON válido.
- Exemplos não devem conter dados reais de clientes, usuários ou tenants.
- Ações críticas devem declarar confirmação e risco.
