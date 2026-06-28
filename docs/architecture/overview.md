# Visão de Arquitetura

## Fronteira do sistema

O ADUI é uma camada transversal entre o chat/LLM e a interface React. Ele não é
um bot de Selenium, não é automação por seletor CSS e não deve receber acesso
irrestrito ao DOM. A UI expõe ferramentas declaradas e o runtime decide quando
chamá-las.

```text
Usuário
  ↓ intenção
Chat / Entrada multimodal
  ↓ prompt estruturado
LLM
  ↓ plano e tool calls
ADUI Runtime
  ↓ checagem
Permission Layer
  ↓ execução permitida
Frontend Tool Bus
  ↓ ações declaradas
React UI + UI Registry
  ↓ eventos
Audit Log + Observability
```

## Componentes

### Chat

Captura intenção do usuário, exibe explicações, pede confirmações e mostra
resumos antes de ações relevantes.

### LLM

Interpreta intenção, escolhe modo de operação e solicita ferramentas. O LLM não
tem permissão final para executar ações críticas.

### ADUI Runtime

Mantém plano de execução, estado da sessão agentica, modo atual e histórico de
ferramentas chamadas.

### Permission Layer

Valida ACL, tenant, perfil do solicitante, risco da ação e necessidade de
confirmação.

### Frontend Tool Bus

Expõe ferramentas declaradas, valida input por schema e normaliza resultados.

### UI Registry

Indexa páginas, componentes, formulários, diálogos, menus, ações, estados e
capabilities disponíveis.

### Interface Awareness

Fornece snapshot controlado da interface: rota atual, breadcrumb, modal aberto,
elemento focado, inputs disponíveis, botões disponíveis, permissões e estado.

### Audit Pipeline

Registra toda tentativa, execução, bloqueio, confirmação e resultado.

## Estados de execução

| Estado | Descrição |
| --- | --- |
| `IDLE` | Nenhuma tarefa agentica ativa. |
| `PLANNING` | Runtime interpreta intenção e monta plano. |
| `WAITING_PERMISSION` | Aguardando ACL, consentimento ou confirmação. |
| `EXECUTING_TOOL` | Ferramenta em execução. |
| `WAITING_USER` | Aguardando clique, input, confirmação ou upload. |
| `COMPLETED` | Tarefa finalizada. |
| `FAILED` | Falha controlada com auditoria. |
| `ROLLED_BACK` | Ação revertida quando possível. |

## Modos de operação

| Modo | Pode navegar | Pode destacar | Pode preencher | Pode salvar | Requer confirmação |
| --- | --- | --- | --- | --- | --- |
| Guide | Não | Sim | Não | Não | Não |
| Assist | Sim | Sim | Sim | Não | Para qualquer execução |
| Execute | Sim | Sim | Sim | Sim | Sim |
| Autonomous Session | Sim | Sim | Sim | Sim | Sim, por política |

## Regra central

Toda ação do agente passa por:

```text
Intenção → Plano → Ferramenta declarada → Permissão → Execução → Auditoria
```
