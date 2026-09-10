# Semana 2: Modelagem e Análise
## Projeto Integrador — Jornada da Engenharia de Software: Da Ideia ao Modelo

---

## 1. Documento de Requisitos v1.0


### Requisitos Funcionais
| ID | Descrição |
|---|---|
| RF01 | O sistema deve permitir o cadastro de clientes (pessoa física e jurídica). |
| RF02 | O sistema deve permitir o cadastro de colaboradores com diferentes níveis de acesso. |
| RF03 | O sistema deve permitir o registro de solicitações/atendimentos vinculados a um cliente. |
| RF04 | O sistema deve exibir o histórico de interações de cada cliente. |
| RF05 | O sistema deve permitir atribuir um colaborador responsável a cada processo ou atendimento. |
| RF06 | O sistema deve permitir o acompanhamento do status de cada processo fiscal. |
| RF07 | O sistema deve emitir alertas de prazos fiscais próximos do vencimento. |
| RF08 | O sistema deve permitir o registro manual de leads captados via redes sociais. |
| RF09 | O sistema deve exibir um painel (dashboard) com indicadores gerais. |
| RF10 | O sistema deve permitir o upload e organização de documentos por cliente. |
| RF11 | O sistema deve permitir gerar relatórios de produtividade por colaborador. |
| RF12 | O sistema deve permitir exportar relatórios em PDF. |

### Requisitos Não-Funcionais
| ID | Descrição |
|---|---|
| RNF01 | Segurança dos dados fiscais e pessoais (criptografia e controle de acesso). |
| RNF02 | Interface simples e intuitiva. |
| RNF03 | Tempo de resposta ≤ 2 segundos em operações comuns. |
| RNF04 | Disponibilidade (uptime) ≥ 99%. |
| RNF05 | Acesso via navegador web. |
| RNF06 | Logs de auditoria de alterações em dados sensíveis. |

---

## 2. Diagrama de Casos de Uso

**Atores:**
- **Gerente** (perfil administrativo, acesso total)
- **Colaborador** (atende clientes, gerencia processos atribuídos a ele)
- **Sistema** (ator secundário — dispara alertas automáticos)

**Casos de uso e relações:**

- **Cadastrar Cliente** — Ator: Gerente, Colaborador
- **Registrar Lead** — Ator: Colaborador
  - `<<extend>>` Qualificar Lead (transformar lead em cliente)
- **Registrar Atendimento** — Ator: Colaborador
  - `<<include>>` Vincular Cliente
  - `<<include>>` Registrar Histórico de Interação
- **Atribuir Responsável** — Ator: Gerente
- **Acompanhar Processo Fiscal** — Ator: Colaborador, Gerente
  - `<<include>>` Atualizar Status do Processo
- **Emitir Alerta de Prazo** — Ator: Sistema (caso de uso automático, disparado por regra de negócio)
- **Upload de Documento** — Ator: Colaborador
  - `<<include>>` Vincular Cliente
- **Gerar Relatório de Produtividade** — Ator: Gerente
- **Visualizar Dashboard** — Ator: Gerente, Colaborador

**Observação para montagem no draw.io:** representar atores como bonecos-palito à esquerda, casos de uso como elipses dentro do retângulo "Sistema CRM Contábil", com linhas de associação simples e as relações `<<include>>`/`<<extend>>` tracejadas conforme notação UML padrão.

---

## 3. Modelo Conceitual (Diagrama de Classes Inicial)

Classes identificadas a partir do domínio, com atributos principais (sem métodos ainda — isso será refinado na Semana 3):

- **Cliente**: id, nome, tipoPessoa (PF/PJ), CPF/CNPJ, telefone, email
- **Colaborador**: id, nome, email, perfilAcesso
- **Lead**: id, nomeContato, origem (Instagram/Facebook/WhatsApp), status, dataCaptura
- **Atendimento**: id, dataHora, descricao, status
- **ProcessoFiscal**: id, tipo, status, prazoVencimento
- **Documento**: id, nomeArquivo, dataUpload, tipo
- **Notificação**: id, mensagem, dataEnvio, lida (booleano)

**Relações principais:**
- Cliente `1 — *` Atendimento (um cliente tem vários atendimentos)
- Cliente `1 — *` ProcessoFiscal
- Cliente `1 — *` Documento
- Colaborador `1 — *` Atendimento (um colaborador é responsável por vários atendimentos)
- Colaborador `1 — *` ProcessoFiscal (responsável)
- Lead `0..1 — 0..1` Cliente (um lead pode se converter em cliente)
- ProcessoFiscal `1 — *` Notificação (gera alertas)

*(Diagrama de classes visual gerado abaixo, como referência inicial — será refinado na Semana 3 com métodos, visibilidade e multiplicidade completas.)*

---

## 4. Histórias de Usuário

1. Como **gerente**, quero cadastrar novos clientes no sistema para manter um registro centralizado da carteira.
2. Como **colaborador**, quero registrar um novo lead vindo do Instagram ou WhatsApp para não perder oportunidades de captação.
3. Como **colaborador**, quero registrar um atendimento vinculado a um cliente para manter o histórico de interações organizado.
4. Como **gerente**, quero atribuir um colaborador responsável a cada processo para reduzir a centralização do trabalho em mim.
5. Como **colaborador**, quero acompanhar o status de um processo fiscal para saber em que etapa ele está.
6. Como **gerente**, quero visualizar um dashboard com indicadores gerais para ter uma visão rápida da operação.
7. Como **colaborador**, quero receber um alerta quando um prazo fiscal estiver próximo do vencimento para evitar atrasos.
8. Como **gerente**, quero gerar relatórios de produtividade por colaborador para acompanhar o desempenho da equipe.

---

## 5. Critérios de Aceitação (Given-When-Then)

**História 2 — Registrar lead**
- **Dado** que o colaborador está na tela de novo lead
- **Quando** ele preenche nome, origem e telefone de contato e salva
- **Então** o lead deve aparecer na lista de leads com status "novo" e data de captura registrada automaticamente

**História 4 — Atribuir responsável**
- **Dado** que o gerente está visualizando um processo sem responsável definido
- **Quando** ele seleciona um colaborador e confirma a atribuição
- **Então** o processo deve passar a exibir o colaborador como responsável e este deve visualizá-lo em sua lista de tarefas

**História 7 — Alerta de prazo**
- **Dado** que um processo fiscal possui uma data de vencimento cadastrada
- **Quando** a data atual estiver a 5 dias ou menos do vencimento
- **Então** o sistema deve gerar automaticamente uma notificação visível ao colaborador responsável e ao gerente
