# Onboarding e Highlight

## Highlight Engine

O Highlight Engine torna a explicação do agente visível na interface.

Recursos planejados:

- borda animada;
- máscara de tela;
- seta;
- tooltip;
- spotlight;
- scroll automático para componente;
- restauração visual após conclusão.

## Regras de UX

- O destaque não deve esconder o componente relevante.
- Tooltips não devem cobrir campos ou botões necessários.
- O usuário deve conseguir cancelar o guia.
- O guia deve respeitar acessibilidade e navegação por teclado.
- Em telas pequenas, o highlight deve preferir scroll e tooltip compacto.

## Onboarding Engine

Um fluxo guiado é uma sequência de etapas com critérios de avanço.

```json
{
  "id": "create-client-onboarding",
  "steps": [
    {
      "id": "open-clients",
      "tool": "navigate",
      "target": "/clients",
      "wait": "WAIT_NAVIGATION"
    },
    {
      "id": "click-new-client",
      "tool": "highlight",
      "target": "clients.new-button",
      "wait": "WAIT_CLICK"
    }
  ]
}
```

## Tipos de espera

| Espera | Quando usar |
| --- | --- |
| `WAIT_CLICK` | Usuário deve clicar no elemento destacado. |
| `WAIT_INPUT` | Usuário deve digitar ou revisar um campo. |
| `WAIT_CONFIRM` | Usuário deve aprovar uma ação. |
| `WAIT_UPLOAD` | Usuário deve escolher arquivo. |
| `WAIT_NAVIGATION` | UI deve concluir transição de rota. |

## Critérios de sucesso

- Fluxo concluído.
- Etapas abandonadas identificadas.
- Tempo por etapa medido.
- Componentes difíceis mapeados.
- Usuário consegue retomar ou reiniciar o tutorial.
