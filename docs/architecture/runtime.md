# Runtime ADUI

## Responsabilidade

O runtime transforma intenções do usuário em planos executáveis por ferramentas
do frontend. Ele também controla modo de operação, sessão do agente, esperas por
interação, confirmação e rollback.

## Entradas

- Mensagem do usuário.
- Snapshot de interface.
- Catálogo de ferramentas disponíveis.
- Permissões do solicitante.
- Estado da sessão agentica.
- Histórico recente de tool calls.

## Saídas

- Resposta textual.
- Plano de execução.
- Tool calls.
- Pedidos de confirmação.
- Eventos de auditoria.
- Métricas de observabilidade.

## Sessão agentica

Toda tarefa executada pelo ADUI cria ou reutiliza uma sessão com:

```json
{
  "id": "adui_session_01",
  "tenant_id": "tenant_01",
  "requesting_user_id": "user_01",
  "agent_id": "adui",
  "actor_type": "AGENT",
  "mode": "ASSIST",
  "status": "ACTIVE"
}
```

`actor_type` identifica o executor técnico. O usuário continua sendo o
solicitante, mas a execução auditada é do agente.

## Planejamento

O plano deve ser composto por etapas pequenas:

```text
1. Navegar para /barbers.
2. Abrir formulário de novo barbeiro.
3. Preencher nome.
4. Validar formulário.
5. Exibir resumo.
6. Aguardar confirmação.
7. Submeter.
```

Cada etapa precisa declarar:

- ferramenta;
- input;
- permissão requerida;
- risco;
- necessidade de confirmação;
- evento de auditoria esperado.

## Esperas

O runtime deve suportar estados de espera:

- `WAIT_CLICK`
- `WAIT_INPUT`
- `WAIT_CONFIRM`
- `WAIT_UPLOAD`
- `WAIT_NAVIGATION`
- `WAIT_VALIDATION`

## Falhas

Falhas devem ser explícitas e recuperáveis quando possível:

- ferramenta indisponível;
- componente invisível;
- permissão negada;
- schema inválido;
- validação do formulário falhou;
- usuário cancelou;
- ação crítica sem confirmação;
- rollback indisponível.

## Rollback

Cada ferramenta pode declarar estratégia de reversão:

| Estratégia | Uso |
| --- | --- |
| `NONE` | Ação não altera estado ou rollback não existe. |
| `UNDO_TOOL` | Existe ferramenta de undo. |
| `COMPENSATING_ACTION` | Uma ação compensatória reverte o efeito. |
| `TRANSACTION` | Operação deve ser confirmada ou abortada em bloco. |

## Controle de autonomia

Autonomia não significa ausência de consentimento. Sessões autônomas têm escopo,
duração, permissões e limites definidos antes da execução.
