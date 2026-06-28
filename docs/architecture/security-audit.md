# Segurança e Auditoria

## Modelo de atores

| Actor Type | Uso |
| --- | --- |
| `USER` | Usuário humano executando diretamente. |
| `AGENT` | Agente ADUI executando ferramenta com autorização. |
| `SYSTEM` | Processo interno ou automação não interativa. |

O ADUI sempre executa como `AGENT`.

## Política de confirmação

| Política | Comportamento |
| --- | --- |
| `NEVER` | Ação informativa ou reversível sem impacto. |
| `BEFORE_SUBMIT` | Exige resumo antes de submeter. |
| `ALWAYS` | Exige confirmação explícita antes da execução. |
| `STEP_UP` | Exige confirmação forte, MFA ou novo consentimento. |

## Níveis de risco

| Risco | Exemplos |
| --- | --- |
| `LOW` | Navegar, destacar, rolar tela. |
| `MEDIUM` | Preencher formulário, selecionar opção, copiar valor permitido. |
| `HIGH` | Submeter formulário, upload, download sensível, cancelar agendamento. |
| `CRITICAL` | Pagamentos, permissões, exclusões críticas, usuários, financeiro. |

## Bloqueios iniciais

Ações críticas ficam bloqueadas até existir desenho específico de política:

- pagamentos;
- movimentações financeiras;
- alteração de permissões;
- criação, exclusão ou elevação de usuários;
- exclusões críticas;
- operações em lote irreversíveis.

## Evento de auditoria

Todo evento registra:

- `event_id`
- `tenant_id`
- `requesting_user_id`
- `agent_id`
- `actor_type`
- `session_id`
- `screen`
- `component_id`
- `tool_name`
- `action`
- `parameters`
- `risk_level`
- `confirmation`
- `result`
- `timestamp`

## Dados sensíveis

Parâmetros podem conter CPF, telefone, endereço ou dados comerciais. A
auditoria deve suportar mascaramento por campo:

```json
{
  "name": "João",
  "cpf": "***.***.***-**",
  "phone": "+55******0000"
}
```

## Observabilidade

Além da auditoria, o ADUI deve emitir métricas agregadas:

- taxa de sucesso por ferramenta;
- falhas por componente;
- tempo médio por fluxo;
- confirmações recusadas;
- cliques evitados;
- abandono de onboarding;
- campos com erro recorrente.

Auditoria explica o que aconteceu. Observabilidade mede padrões de uso e
fricção.
