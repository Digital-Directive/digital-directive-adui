# AGENTS.md

Este repositório contém a arquitetura e a documentação inicial do ADUI
(Agent-Driven User Interface) da Digital Directive.

## Diretriz principal

- Este projeto nasce como documentação e contratos de arquitetura. Não introduza
  runtime de produção sem uma decisão arquitetural registrada em `docs/adr`.
- O ADUI nunca deve manipular DOM diretamente. A execução do agente acontece
  apenas por ferramentas declaradas pelo frontend.
- Toda ação executável deve ter schema, ACL, política de confirmação e trilha de
  auditoria.
- Sessões agenticas devem operar com `actor_type = AGENT`; nunca simular o
  usuário humano como executor direto.

## Separação de responsabilidades

- Frontend, SDKs, tooling, schemas e bibliotecas de UI podem ser TypeScript.
- Backend, runtime server-side, workers, jobs, integrações e serviços de
  produção devem seguir o padrão Digital Directive em Rust.
- Infraestrutura deve ser documentada e, quando implementada, nascer em projeto
  próprio de Terraform/IaC.
- Dados e migrations operacionais não pertencem a este repositório.

## Segurança

- Não comitar segredos, tokens, chaves, dados pessoais reais ou dumps de
  produção.
- Ações críticas exigem confirmação explícita e registro auditável.
- Pagamentos, permissões, exclusões críticas, alteração de usuários e
  movimentações financeiras ficam bloqueados por padrão até existir política
  formal de risco e confirmação.

## Operação local

- Ao executar comandos neste workspace, prefixe com `rtk`.
- Antes de publicar alterações, valide os documentos e schemas relevantes.
