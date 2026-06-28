# Ferramentas do Frontend

## Contrato

Toda ferramenta do frontend é uma função declarada, validada por schema,
registrada no UI Registry e auditável.

Uma ferramenta deve declarar:

- `name`
- `description`
- `input_schema`
- `result_schema`
- `required_permissions`
- `risk_level`
- `confirmation_policy`
- `audit_event_type`
- `rollback_strategy`

## Ferramentas iniciais

| Ferramenta | Descrição | Risco inicial |
| --- | --- | --- |
| `navigate` | Troca de rota ou abre página. | Baixo |
| `highlight` | Destaca componente. | Baixo |
| `fillForm` | Preenche campos declarados. | Médio |
| `click` | Aciona ação de componente. | Médio |
| `submit` | Submete formulário validado. | Alto |
| `scroll` | Move viewport. | Baixo |
| `openModal` | Abre diálogo declarado. | Baixo |
| `closeModal` | Fecha diálogo declarado. | Baixo |
| `search` | Executa busca de UI. | Baixo |
| `select` | Seleciona opção em campo controlado. | Médio |
| `drag` | Inicia arrasto controlado. | Médio |
| `drop` | Conclui arrasto controlado. | Médio |
| `upload` | Solicita upload. | Alto |
| `download` | Baixa arquivo permitido. | Médio |
| `copy` | Copia dado permitido. | Médio |
| `paste` | Cola valor em campo permitido. | Médio |

## Exemplo de tool call

```json
{
  "tool": "navigate",
  "input": {
    "page": "/clients"
  }
}
```

## Exemplo de resultado

```json
{
  "status": "OK",
  "screen": "/clients",
  "component_id": "clients.index",
  "message": "Página de clientes aberta."
}
```

## Component capabilities

Componentes registram capacidades, não detalhes internos.

```json
{
  "id": "customer.form",
  "role": "form",
  "description": "Formulário de cliente",
  "actions": ["fill", "validate", "submit", "clear"],
  "permissions": ["customer:write"],
  "visibility": "VISIBLE",
  "enabled": true
}
```

## Regras de implementação futura

- Uma ferramenta não deve aceitar seletores CSS arbitrários.
- Inputs devem apontar para componentes registrados.
- Campos preenchíveis precisam ter identificador estável.
- Erros devem retornar códigos estruturados.
- Toda chamada deve gerar evento de auditoria, inclusive bloqueios.
