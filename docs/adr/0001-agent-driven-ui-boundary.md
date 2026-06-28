# ADR 0001: ADUI executa por ferramentas declaradas

Status: Aceita

Data: 2026-06-27

## Contexto

O ADUI precisa permitir que agentes de IA naveguem, expliquem, preencham e
executem ações na interface. Uma alternativa simples seria permitir que o agente
inspecione e manipule DOM diretamente, usando seletores, eventos sintéticos ou
automação de navegador.

Esse caminho reduz o custo inicial, mas cria riscos de segurança, fragilidade de
UI, baixa auditabilidade e acoplamento a detalhes internos do frontend.

## Decisão

O ADUI não manipula DOM diretamente. Toda ação deve passar por ferramenta
declarada, registrada e validada pelo frontend.

Cada ferramenta deve possuir:

- schema de entrada;
- schema de resultado;
- permissões;
- política de confirmação;
- nível de risco;
- evento de auditoria;
- estratégia de rollback quando aplicável.

## Consequências

### Positivas

- Ações ficam auditáveis.
- Permissões são aplicadas antes da execução.
- Componentes podem evoluir internamente sem quebrar o agente.
- O produto evita automações frágeis baseadas em seletores.
- A mesma infraestrutura pode ser reutilizada por múltiplas telas.

### Negativas

- Cada tela precisa registrar metadados e capabilities.
- O custo inicial de instrumentação é maior.
- Funcionalidades novas exigem contrato explícito antes de serem agenticas.

## Alternativas consideradas

### Manipulação direta do DOM

Rejeitada por fragilidade, baixo controle de permissão e auditoria insuficiente.

### Automação externa de navegador

Rejeitada para runtime de produto. Pode ser usada em testes, mas não como
mecanismo de execução do ADUI.

### Ferramentas server-side apenas

Rejeitada como única abordagem porque o ADUI precisa ensinar e acompanhar a
interface em tempo real. A execução pode acionar serviços no futuro, mas a
superfície inicial é o frontend.
