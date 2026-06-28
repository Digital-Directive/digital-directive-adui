# PRD: ADUI (Agent-Driven User Interface)

Status: Draft v1.0

Projeto: Barbearia Platform

Componente: Frontend + AI Runtime + Auditoria

Prioridade: Alta

## Visão

O ADUI é um subsistema que permite que agentes de IA interajam diretamente com a
interface gráfica da aplicação da mesma forma que um usuário faria, sempre
respeitando permissões, consentimento e auditoria.

O objetivo não é apenas responder perguntas, mas transformar a interface em uma
superfície executável pelo agente.

## Objetivo principal

Permitir que a IA:

- navegue pela interface;
- execute ações;
- preencha formulários;
- ensine usuários;
- automatize tarefas repetitivas;
- mantenha auditoria completa.

## Problemas atuais

Interfaces tradicionais criam barreiras como:

- usuários não sabem onde clicar;
- curva de aprendizado alta;
- muitos formulários;
- processos repetitivos;
- treinamento manual;
- suporte sobrecarregado.

O ADUI reduz essas barreiras ao transformar fluxos de UI em capacidades
assistidas, guiadas e auditáveis.

## Casos de uso

### Navegação

Usuário: "Abre meus agendamentos."

ADUI:

- troca de página;
- abre filtros;
- posiciona a tela corretamente.

### Preenchimento assistido

Usuário: "Cria um barbeiro chamado João."

ADUI:

- abre a tela;
- preenche campos;
- mostra resumo;
- pede confirmação;
- salva apenas após autorização.

### Execução direta

Usuário: "Cancela o agendamento das 15h."

ADUI:

- localiza o agendamento;
- confirma a intenção;
- executa a ação permitida;
- registra auditoria.

### Onboarding

Usuário: "Como funciona essa tela?"

ADUI:

- destaca componentes;
- explica a função de cada área;
- espera interação;
- acompanha até finalizar.

### Tutorial guiado

Modo semelhante a onboarding de Stripe, Linear ou Notion:

- bloqueia distrações;
- destaca botões;
- mostra setas;
- aguarda clique;
- continua o fluxo.

### Automação

Usuário: "Configura minha agenda de terça."

O agente pode executar várias ações em sequência, desde que cada ferramenta,
permissão e confirmação sejam respeitadas.

## Modos de operação

| Modo | Permissão de execução |
| --- | --- |
| Guide Mode | Apenas explica. Não executa. |
| Assist Mode | Pode preencher campos. Nunca salva sozinho. |
| Execute Mode | Executa ações completas mediante autorização. |
| Autonomous Session | Sessão temporária do agente, sempre com `actor_type = AGENT`. |

## Sessão do agente

Toda execução do ADUI utiliza um tipo próprio de sessão:

```text
Session
  id
  tenant
  actor_type
```

Valores de `actor_type`:

- `USER`
- `AGENT`
- `SYSTEM`

O ADUI nunca executa como `USER`.

## Auditoria

Toda ação deve registrar:

- usuário solicitante;
- agente executor;
- horário;
- tela;
- componente;
- ação;
- parâmetros;
- resultado.

Exemplo:

```text
User: Arthur
Agent: ADUI
Action: Create Barber
Fields:
  name = João
Origin: Frontend Agent
Timestamp: 2026-06-27T00:00:00-03:00
```

## Ferramentas do frontend

O frontend deverá expor ferramentas como:

- `navigate`
- `highlight`
- `fillForm`
- `click`
- `submit`
- `scroll`
- `openModal`
- `closeModal`
- `search`
- `select`
- `drag`
- `drop`
- `upload`
- `download`
- `copy`
- `paste`

Cada ferramenta possui schema, permissões e auditoria.

## Modelo de tool calling

O ADUI nunca manipula DOM diretamente. Sempre utiliza ferramentas declaradas.

Exemplo:

```json
{
  "tool": "navigate",
  "input": {
    "page": "/clients"
  }
}
```

## Registro de componentes

Cada componente pode registrar capacidades.

Exemplo:

```text
CustomerForm
  capabilities:
    fill
    validate
    submit
    clear
```

## Component metadata

Cada elemento pode declarar:

- `id`
- `role`
- `description`
- `actions`
- `permissions`
- `visibility`
- `enabled`

## UI Registry

Módulo responsável por indexar:

- páginas;
- componentes;
- formulários;
- diálogos;
- menus;
- ações.

## Interface awareness

O agente deve conhecer:

- página atual;
- breadcrumb;
- modal aberto;
- elemento focado;
- inputs disponíveis;
- botões disponíveis;
- permissões;
- estado da aplicação.

## Highlight Engine

Permite destacar componentes com:

- borda animada;
- máscara;
- seta;
- tooltip;
- spotlight.

## Onboarding Engine

Fluxos guiados são compostos por etapas:

```text
Step 1: Abra clientes
Step 2: Clique Novo
Step 3: Digite nome
Step 4: Salvar
```

O fluxo pode aguardar interações como:

- `WAIT_CLICK`
- `WAIT_INPUT`
- `WAIT_CONFIRM`
- `WAIT_UPLOAD`

## Auto fill

Pode preencher campos como nome, telefone, CPF, endereço e observações. Antes de
salvar, o ADUI deve mostrar resumo, pedir confirmação e executar apenas após
autorização.

## Confirmação inteligente

Toda ação destrutiva exige confirmação. Exemplos:

- excluir;
- cancelar;
- alterar preço;
- apagar cliente.

## Rollback

Sempre que possível, ações devem oferecer `undo` ou rollback transacional.

## Segurança

Nunca executar sem confirmação:

- exclusões críticas;
- pagamentos;
- movimentações financeiras;
- permissões;
- usuários.

## Permissões

Cada ferramenta possui ACL. Exemplos:

| Ferramenta | Perfil mínimo |
| --- | --- |
| Navigate | Todos |
| Fill Form | Funcionário |
| Delete | Administrador |

## Observabilidade

Métricas:

- tempo médio;
- sucesso;
- falhas;
- cliques evitados;
- onboarding completo;
- abandono;
- ações automatizadas.

## Analytics

Medir:

- componentes difíceis;
- fluxos abandonados;
- campos confusos;
- erros recorrentes;
- tempo por tela.

## Benefícios

- Redução de suporte.
- Menor curva de aprendizado.
- Menos erros.
- Automação.
- Adoção mais rápida.
- Melhor experiência.
- Maior acessibilidade.

## Arquitetura

```text
Usuário
  ↓
Chat
  ↓
LLM
  ↓
ADUI Runtime
  ↓
Permission Layer
  ↓
Frontend Tools
  ↓
React
  ↓
UI
```

## Arquitetura de auditoria

```text
User
  ↓
Solicitação
  ↓
Agent Session
  ↓
Tool
  ↓
Frontend
  ↓
Audit Log
  ↓
Observability
```

## Roadmap

### Fase 1

- Navegação.
- Highlight.
- Onboarding.
- Fill Form.
- Click.

### Fase 2

- Execução completa.
- Sessão do agente.
- Auditoria.
- Rollback.

### Fase 3

- Automações complexas.
- Fluxos reutilizáveis.
- Tutoriais inteligentes.
- Analytics.

### Fase 4

- Aprendizado dos fluxos.
- Sugestões proativas.
- Onboarding personalizado.
- Assistente contextual permanente.

## KPIs

- Reduzir o tempo de onboarding de novos usuários em 60%.
- Reduzir chamados de suporte relacionados ao uso da interface em 50%.
- Permitir que 100% das ações executadas pelo agente sejam auditáveis.
- Garantir que 100% das ações críticas exijam confirmação explícita.
- Disponibilizar ferramentas reutilizáveis para qualquer tela do sistema,
  tornando o ADUI uma infraestrutura transversal e não uma solução específica da
  barbearia.
