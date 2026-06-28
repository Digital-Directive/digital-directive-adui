# ADUI

ADUI (Agent-Driven User Interface) é a arquitetura da Digital Directive para
permitir que agentes de IA naveguem, expliquem e executem ações na interface do
produto usando ferramentas declaradas, permissões explícitas e auditoria
completa.

Status: `Draft v1.0`

Projeto inicial: Barbearia Platform

Escopo atual: documentação, arquitetura e contratos iniciais. Este repositório
não contém runtime de produção nesta primeira fase.

## Objetivo

Transformar a interface gráfica em uma superfície executável pelo agente sem
abrir mão de consentimento, permissões, observabilidade e rastreabilidade. O
usuário poderá pedir ações como:

- "Cadastre um novo barbeiro."
- "Me ensina a criar um agendamento."
- "Preenche esse formulário para mim."
- "Vai até a tela de clientes."
- "Mostra onde fica essa opção."
- "Configura meus horários de atendimento."

## Princípios

- O agente usa ferramentas declaradas pelo frontend, não acesso livre ao DOM.
- Toda ferramenta possui schema, ACL, confirmação quando necessário e auditoria.
- A execução agentica usa sessão própria com `actor_type = AGENT`.
- O modo assistido pode preencher campos, mas não salva sem confirmação.
- Ações destrutivas ou financeiras exigem confirmação explícita.
- A arquitetura deve ser transversal para qualquer tela do sistema, não uma
  automação pontual da barbearia.

## Documentação

- [PRD v1.0](docs/prd/adui-prd-v1.md)
- [Visão de arquitetura](docs/architecture/overview.md)
- [Runtime ADUI](docs/architecture/runtime.md)
- [Ferramentas do frontend](docs/architecture/frontend-tools.md)
- [Segurança e auditoria](docs/architecture/security-audit.md)
- [Onboarding e highlight](docs/architecture/onboarding-highlight.md)
- [Roadmap por fases](docs/roadmap/phases.md)
- [ADR 0001](docs/adr/0001-agent-driven-ui-boundary.md)

## Contratos iniciais

- [Tool Schema](docs/contracts/tool.schema.json)
- [Component Metadata Schema](docs/contracts/component-metadata.schema.json)
- [Agent Session Schema](docs/contracts/agent-session.schema.json)
- [Audit Event Schema](docs/contracts/audit-event.schema.json)

## Relação com a Barbearia Platform

A barbearia é o primeiro domínio de validação porque concentra fluxos de alto
valor operacional: agenda, barbeiros, clientes, serviços, horários e onboarding.
O ADUI, porém, deve permanecer uma infraestrutura de plataforma.
