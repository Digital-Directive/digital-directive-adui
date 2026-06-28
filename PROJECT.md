# Projeto: ADUI

## Metadados

- Nome: ADUI
- Nome completo: Agent-Driven User Interface
- Organização: Digital Directive
- Status: Draft v1.0
- Primeiro domínio: Barbearia Platform
- Prioridade: Alta
- Tipo de entrega atual: arquitetura e documentação

## Visão arquitetural

O ADUI conecta chat, LLM, runtime agentico, camada de permissões, ferramentas do
frontend e auditoria. O agente não aciona componentes por seletores DOM; ele
solicita ferramentas registradas como `navigate`, `highlight`, `fillForm`,
`click`, `submit`, `search`, `select`, `upload` e `download`.

## Módulos planejados

| Módulo | Responsabilidade |
| --- | --- |
| UI Registry | Indexar páginas, componentes, formulários, diálogos, menus e ações. |
| Interface Awareness | Expor página atual, breadcrumb, modal, foco, inputs, botões, permissões e estado. |
| ADUI Runtime | Interpretar intenção, planejar chamadas de ferramenta e controlar modos de execução. |
| Permission Layer | Aplicar ACL, risco, consentimento e bloqueios de segurança. |
| Frontend Tools | Executar ações declaradas no frontend e retornar resultados estruturados. |
| Highlight Engine | Destacar elementos com spotlight, seta, tooltip, máscara e borda animada. |
| Onboarding Engine | Orquestrar tutoriais guiados e estados de espera por interação. |
| Audit Pipeline | Registrar solicitante, agente, ferramenta, componente, parâmetros e resultado. |
| Observability | Medir sucesso, falhas, tempo, cliques evitados, abandono e pontos de atrito. |

## Marcos

| Fase | Entrega |
| --- | --- |
| 1 | Navegação, highlight, onboarding, fill form e click. |
| 2 | Execução completa, sessão do agente, auditoria e rollback. |
| 3 | Automações complexas, fluxos reutilizáveis, tutoriais inteligentes e analytics. |
| 4 | Aprendizado dos fluxos, sugestões proativas, onboarding personalizado e assistente contextual permanente. |

## Critérios de sucesso

- Reduzir o tempo de onboarding de novos usuários em 60%.
- Reduzir chamados de suporte sobre uso da interface em 50%.
- Tornar 100% das ações executadas pelo agente auditáveis.
- Garantir confirmação explícita para 100% das ações críticas.
- Disponibilizar ferramentas reutilizáveis para qualquer tela do sistema.
