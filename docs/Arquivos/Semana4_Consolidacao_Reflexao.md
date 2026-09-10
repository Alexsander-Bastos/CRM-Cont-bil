# Semana 4: Consolidação e Reflexão
## Projeto Integrador — Jornada da Engenharia de Software: Da Ideia ao Modelo

---

## 1. Documento de Requisitos v2.0


### Requisitos Funcionais

| ID | Descrição | Caso de Uso relacionado | Classe(s) envolvida(s) |
|---|---|---|---|
| RF01 | Cadastrar clientes (PF/PJ) | Cadastrar Cliente | Cliente |
| RF02 | Cadastrar colaboradores com níveis de acesso | Autenticar / Gerenciar Colaborador | Colaborador |
| RF03 | Registrar solicitações/atendimentos vinculados a cliente | Registrar Atendimento | Atendimento, Cliente |
| RF04 | Exibir histórico de interações do cliente | Registrar Atendimento | Atendimento, Cliente |
| RF05 | Atribuir colaborador responsável a processo | Atribuir Responsável | ProcessoFiscal, Colaborador |
| RF06 | Acompanhar status de processo fiscal | Registrar e Acompanhar Processo Fiscal | ProcessoFiscal |
| RF07 | Emitir alertas de prazos fiscais | Emitir Alerta de Prazo | ProcessoFiscal, Notificacao |
| RF08 | Registrar leads captados via redes sociais | Registrar Lead | Lead |
| RF09 | Exibir dashboard com indicadores | Visualizar Dashboard | Cliente, ProcessoFiscal, Lead |
| RF10 | Upload e organização de documentos por cliente | Upload de Documento | Documento, Cliente |
| RF11 | Gerar relatórios de produtividade | Gerar Relatório de Produtividade | Colaborador, Atendimento |
| RF12 | Exportar relatórios em PDF | Gerar Relatório de Produtividade | — (funcionalidade de exportação) |

### Requisitos Não-Funcionais

| ID | Descrição | Justificativa |
|---|---|---|
| RNF01 | Segurança dos dados (criptografia, controle de acesso) | Dados fiscais/pessoais são sensíveis (mencionado na entrevista) |
| RNF02 | Interface simples e intuitiva | Cliente relatou baixa familiaridade tecnológica da equipe |
| RNF03 | Tempo de resposta ≤ 2s | Garantir fluidez no atendimento em tempo real |
| RNF04 | Disponibilidade ≥ 99% | Sistema crítico para operação diária da assessoria |
| RNF05 | Acesso via navegador web | Facilitar uso sem instalação em múltiplos dispositivos |
| RNF06 | Logs de auditoria | Rastreabilidade em caso de erro em dados fiscais |

---

## 2. Matriz de Rastreabilidade (Resumo)

| Requisito | Caso de Uso | Diagrama de Classes | História de Usuário |
|---|---|---|---|
| RF03, RF04 | Registrar Atendimento | Atendimento, Cliente | História 3 |
| RF05, RF06 | Registrar e Acompanhar Processo Fiscal (maior risco) | ProcessoFiscal, Colaborador | Histórias 4 e 5 |
| RF07 | Emitir Alerta de Prazo | ProcessoFiscal, Notificacao | História 7 |
| RF08 | Registrar Lead | Lead | História 2 |
| RF09 | Visualizar Dashboard | Cliente, ProcessoFiscal, Lead | História 6 |
| RF11 | Gerar Relatório de Produtividade | Colaborador, Atendimento | História 8 |

---

## 3. Pacote de Modelos UML — Checklist de Entrega

- [x] Diagrama de Casos de Uso (especificado na Semana 2 — montar no draw.io e exportar em PDF + arquivo .drawio editável)
- [x] Diagrama de Classes (Modelo Conceitual da Semana 2 + versão refinada da Semana 3 — exportar PDF + .drawio)
- [x] Diagrama de Sequência do Caso de Uso de Maior Risco (Semana 3 — exportar PDF + .drawio)

---

## 4. Relatório Final (máx. 3 páginas)

### Resumo do escopo e decisões técnicas principais

O projeto desenvolveu a análise e modelagem de um sistema de CRM contábil para a Moura Assessoria Contábil Ltda, microempresa que enfrenta dificuldades de captação de clientes e sobrecarga de trabalho centralizada na gerente. A solução proposta centraliza o atendimento (hoje fragmentado entre WhatsApp, Instagram e Facebook), organiza a carteira de clientes, distribui responsabilidades entre colaboradores e acompanha prazos fiscais com alertas automáticos.

Optou-se por modelar o caso de uso "Registrar e Acompanhar Processo Fiscal" como o de maior risco, por envolver prazos legais e ser o núcleo de valor do sistema. As sete classes centrais do modelo (Cliente, Colaborador, Lead, Atendimento, ProcessoFiscal, Documento, Notificacao) foram definidas a partir dos requisitos levantados na entrevista simulada e no benchmarking com sistemas de CRM e gestão contábil existentes.

### Principais desafios e como foram superados

- **Desafio 1 — Escopo amplo demais no início:** o brainstorming inicial gerou muitas ideias (19 funcionalidades). Foi necessário priorizar via backlog (MoSCoW simplificado: Alta/Média/Baixa) para manter o foco nas funcionalidades que realmente resolvem as dores do cliente fictício.
- **Desafio 2 — Trabalho individual em uma atividade pensada para duplas:** o Contrato de Colaboração e a divisão de responsabilidades precisaram ser adaptados para um planejamento pessoal de trabalho, mantendo o rigor de documentação e commits organizados.
- **Desafio 3 — Garantir rastreabilidade entre os artefatos:** para evitar inconsistência entre requisitos, casos de uso e classes, foi construída a matriz de rastreabilidade na Semana 4, conectando cada requisito ao(s) artefato(s) que o implementam.

### Reflexão

**Aprendizado técnico:** Ficou evidente como a qualidade dos requisitos levantados na Semana 1 impacta diretamente a consistência dos modelos das semanas seguintes — um requisito mal especificado se propaga como ambiguidade nos casos de uso e nas classes.

**Aprendizado sobre trabalho (adaptado para contexto individual):** Mesmo sem uma dupla, a disciplina de documentar decisões técnicas (por que escolher este caso de uso como de maior risco, por que esta estrutura de classes) se mostrou essencial — funcionou como uma forma de "prestar contas" ao processo, similar ao que a colaboração em dupla exigiria.

---

## 5. Repositório Git Atualizado — Checklist

- [ ] Commits com mensagens descritivas e frequência regular ao longo das 4 semanas
- [ ] README final atualizado com status do projeto e links para os artefatos
- [ ] Pastas `/docs/requisitos`, `/docs/modelos`, `/docs/historias` preenchidas com as versões finais
- [ ] Matriz de rastreabilidade incluída em `/docs/requisitos`
