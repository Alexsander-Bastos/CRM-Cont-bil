# Semana 3: Design Técnico e Detalhamento
## Projeto Integrador — Jornada da Engenharia de Software: Da Ideia ao Modelo

---

## 1. Diagrama de Classes Refinado

Classes com atributos, métodos, visibilidade e multiplicidade completas.

### Classe: Cliente
- `- id: int`
- `- nome: string`
- `- tipoPessoa: enum {PF, PJ}`
- `- documento: string` (CPF ou CNPJ)
- `- telefone: string`
- `- email: string`
- `+ cadastrar(): void`
- `+ atualizarDados(): void`
- `+ listarHistorico(): List<Atendimento>`

### Classe: Colaborador
- `- id: int`
- `- nome: string`
- `- email: string`
- `- perfilAcesso: enum {Gerente, Colaborador}`
- `+ autenticar(): boolean`
- `+ listarProcessosAtribuidos(): List<ProcessoFiscal>`

### Classe: Lead
- `- id: int`
- `- nomeContato: string`
- `- origem: enum {Instagram, Facebook, WhatsApp}`
- `- status: enum {Novo, Qualificado, Convertido, Descartado}`
- `- dataCaptura: date`
- `+ qualificar(): void`
- `+ converterEmCliente(): Cliente`

### Classe: Atendimento
- `- id: int`
- `- dataHora: datetime`
- `- descricao: string`
- `- status: enum {Aberto, EmAndamento, Concluído}`
- `+ registrar(): void`
- `+ atualizarStatus(novoStatus): void`

### Classe: ProcessoFiscal
- `- id: int`
- `- tipo: string`
- `- status: enum {Aguardando, EmAndamento, Concluído}`
- `- prazoVencimento: date`
- `+ atualizarStatus(): void`
- `+ verificarPrazo(): boolean`

### Classe: Documento
- `- id: int`
- `- nomeArquivo: string`
- `- dataUpload: datetime`
- `- tipo: string`
- `+ upload(): void`
- `+ excluir(): void`

### Classe: Notificacao
- `- id: int`
- `- mensagem: string`
- `- dataEnvio: datetime`
- `- lida: boolean`
- `+ enviar(): void`
- `+ marcarComoLida(): void`

**Multiplicidade das relações:**
- Cliente `1` — `0..*` Atendimento
- Cliente `1` — `0..*` ProcessoFiscal
- Cliente `1` — `0..*` Documento
- Colaborador `1` — `0..*` Atendimento
- Colaborador `1` — `0..*` ProcessoFiscal
- Lead `0..1` — `0..1` Cliente (relação de conversão)
- ProcessoFiscal `1` — `0..*` Notificacao

> 💬 **Nota minha (não faz parte do entregável):** os tipos como `enum` e a sintaxe `List<T>` são só pra deixar claro a ideia pra você — quando for desenhar no draw.io, use a notação UML padrão (atributo: tipo, sem `<>` ou chaves), e visibilidade `-` (privado) e `+` (público) já está correta pro padrão UML.

---

## 2. Caso de Uso de Maior Risco: Registrar e Acompanhar Processo Fiscal

**Justificativa da escolha:** este é o caso de uso de maior risco porque envolve prazos legais (multas e penalidades em caso de atraso), depende de atualização constante de status por múltiplos colaboradores, e é o núcleo do valor de negócio do sistema — errar aqui compromete a confiança do cliente na assessoria.

**Ator principal:** Colaborador
**Ator secundário:** Sistema (gera alertas automáticos), Gerente (supervisiona)

**Pré-condições:**
- O colaborador deve estar autenticado no sistema
- O cliente relacionado ao processo já deve estar cadastrado

**Fluxo principal:**
1. O colaborador acessa a tela "Novo Processo Fiscal"
2. O colaborador seleciona o cliente vinculado
3. O colaborador informa o tipo de processo e o prazo de vencimento
4. O sistema salva o processo com status "Aguardando"
5. O sistema atribui automaticamente o colaborador como responsável
6. O colaborador atualiza o status do processo conforme ele avança (ex: "Em andamento")
7. O sistema verifica diariamente os prazos e envia notificação quando faltarem 5 dias ou menos para o vencimento
8. O colaborador marca o processo como "Concluído" ao finalizá-lo

**Fluxos alternativos:**
- **A1 (prazo já vencido ao cadastrar):** Se a data informada já passou, o sistema exibe um aviso e solicita confirmação antes de salvar.
- **A2 (processo sem responsável):** Se o colaborador não for definido automaticamente (ex: cadastro pelo gerente), o gerente deve atribuir manualmente um responsável antes que o processo saia do status "Aguardando".
- **A3 (reatribuição):** O gerente pode reatribuir o processo a outro colaborador a qualquer momento, mantendo o histórico da mudança.

**Pós-condições:**
- O processo fiscal está registrado com status atualizado e responsável definido
- Notificações de prazo são geradas automaticamente enquanto o processo não for concluído

**Regras de negócio:**
- RN01: Todo processo fiscal deve ter um responsável definido em até 24h após o cadastro.
- RN02: Alertas de prazo são enviados aos 5, 3 e 1 dia(s) antes do vencimento.
- RN03: Um processo só pode ser marcado como "Concluído" se todos os documentos obrigatórios estiverem anexados.

---

## 3. Diagrama de Sequência — Registrar e Acompanhar Processo Fiscal

Participantes: **Colaborador**, **Interface**, **ProcessoFiscal**, **Sistema (verificador de prazos)**, **Notificacao**

Fluxo representado (correspondente ao fluxo principal acima):
1. Colaborador → Interface: preencherDadosProcesso()
2. Interface → ProcessoFiscal: criar(cliente, tipo, prazo)
3. ProcessoFiscal → ProcessoFiscal: status = "Aguardando"
4. ProcessoFiscal → Interface: confirmação de criação
5. Interface → Colaborador: exibirProcessoCriado()
6. *(assíncrono, disparado diariamente)* Sistema → ProcessoFiscal: verificarPrazo()
7. ProcessoFiscal → Notificacao: enviar(mensagem, colaboradorResponsável)
8. Notificacao → Colaborador: notificar()
9. Colaborador → Interface: atualizarStatus("Concluído")
10. Interface → ProcessoFiscal: atualizarStatus()

*(Diagrama de sequência visual gerado abaixo como referência.)*

---

## 4. Backlog do Produto (Priorizado)

| Prioridade | História | Esforço (relativo) |
|---|---|---|
| Alta | Cadastrar cliente | P |
| Alta | Registrar processo fiscal e atribuir responsável | M |
| Alta | Alertar prazos de vencimento | M |
| Alta | Registrar atendimento vinculado a cliente | P |
| Média | Registrar lead via redes sociais | P |
| Média | Acompanhar status do processo | P |
| Média | Visualizar dashboard com indicadores | G |
| Média | Upload de documentos por cliente | M |
| Baixa | Gerar relatório de produtividade | M |
| Baixa | Exportar relatórios em PDF | P |
| Baixa | Converter lead em cliente | P |

*(Esforço: P = Pequeno, M = Médio, G = Grande — estimativa relativa, sem número de horas, conforme sugerido para backlog ágil inicial.)*

---

## 5. Repositório GitLab

**README.md (estrutura sugerida):**
```
# CRM Contábil — Moura Assessoria Contábil

Projeto integrador da disciplina Jornada da Engenharia de Software.
Sistema de gestão de relacionamento com clientes para assessoria contábil,
com foco em centralizar atendimento, captação de leads e acompanhamento
de processos fiscais.

## Escopo
Projeto de análise e modelagem (sem implementação de código).

## Estrutura de pastas
- /docs/requisitos → documentos de requisitos (v1.0, v2.0)
- /docs/modelos → diagramas UML (casos de uso, classes, sequência)
- /docs/historias → histórias de usuário e critérios de aceitação

## Decisões técnicas
- Escolhemos modelar um CRM contábil porque os problemas relatados pelo
  cliente fictício (captação de clientes e sobrecarga de trabalho) são
  diretamente resolvidos por esse tipo de sistema.
```

**Estrutura de pastas:** `/docs/requisitos`, `/docs/modelos`, `/docs/historias`

> 💬 **Nota minha (não faz parte do entregável):** crie o repositório no GitLab, adicione esse README, e vá commitando os documentos das semanas anteriores nas pastas certas — isso conta como entrega junto com os artefatos.

---

*Documento gerado como parte da Semana 3 do projeto integrador.*
