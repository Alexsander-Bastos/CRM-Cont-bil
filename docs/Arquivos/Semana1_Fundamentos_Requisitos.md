# Semana 1: Fundamentos e Requisitos
**solo:** [Alexsander bastos da silva]

---

## 1. Cliente Fictício

**Empresa:** Moura Assessoria Contábil Ltda.
**Perfil:** Microempresa em atividade desde 17/10/2008, composta por 1 sócio e 4 colaboradores.

**Contexto:** Oferece assessoria fiscal, contábil e trabalhista, além de serviços de imposto de renda de pessoa física (incluindo processos de isenção por doenças graves). A divulgação é feita por Instagram, Facebook (conteúdo educativo) e WhatsApp corporativo (relacionamento com clientes).

**Missão:** Oferecer soluções contábeis personalizadas, pautadas em responsabilidade, ética e agilidade, garantindo segurança fiscal e tranquilidade aos clientes.

**Visão:** Consolidar-se como referência na área contábil do Rio Grande do Norte.

**Valores:** Integridade, transparência, empatia, agilidade, precisão e valorização do contato humano.

**Objetivo de negócio do sistema:** Resolver os principais problemas enfrentados pela empresa:
- Dificuldade de captar novos clientes
- Sobrecarga e centralização do trabalho na figura da gerente
- Comunicação fragmentada entre WhatsApp, Instagram e Facebook
- Necessidade de acompanhar processos e prazos fiscais de forma organizada

**Sistema proposto:** CRM Contábil — plataforma de gestão de relacionamento com clientes e atendimento, que centraliza solicitações, organiza a carteira de clientes, distribui tarefas entre colaboradores e apoia a captação de leads.

---

## 2. Entrevista Simulada

**Entrevistado:** Sócia/gerente da Moura Assessoria Contábil (perfil fictício baseado no contexto real da empresa)

**P1: Como funciona hoje o atendimento aos clientes?**
R: "Recebemos mensagens pelo WhatsApp, Instagram e Facebook. Cada colaborador acaba respondendo do seu jeito, sem um histórico centralizado. Muita coisa passa por mim porque sou eu que sei onde cada processo está."

**P2: Qual é a maior dificuldade da empresa hoje?**
R: "Captar novos clientes é difícil, porque não temos um controle claro de quem já demonstrou interesse e não foi atendido a tempo. Além disso, fico sobrecarregada porque tudo depende de mim para não se perder."

**P3: Como é feito o acompanhamento dos processos fiscais e prazos?**
R: "Hoje é bem manual, em planilhas e anotações separadas. Às vezes um prazo passa perto e a gente só percebe em cima da hora."

**P4: Os colaboradores têm autonomia para atender sozinhos?**
R: "Deveriam ter, mas como não existe um sistema que mostre o que cada um está fazendo, tudo acaba voltando pra mim pra decidir ou aprovar."

**P5: O que a senhora gostaria que um sistema resolvesse primeiro?**
R: "Gostaria de conseguir ver, em um lugar só, todos os clientes, o status de cada processo e quem está responsável por cada um. E que os leads que chegam pelas redes sociais não se percam."

**P6: Existe alguma preocupação com segurança dos dados dos clientes?**
R: "Sim, lidamos com informações fiscais e pessoais sensíveis, então isso é fundamental."

---

## 3. Brainstorming de Funcionalidades (15+ ideias)

1. Cadastro de clientes (pessoa física e jurídica)
2. Cadastro de colaboradores com perfis de acesso
3. Registro centralizado de solicitações/atendimentos
4. Histórico de interações por cliente
5. Atribuição de responsável por atendimento/processo
6. Painel de acompanhamento de status dos processos fiscais
7. Alertas de prazos fiscais próximos do vencimento
8. Integração/registro manual de contatos vindos de Instagram, Facebook e WhatsApp
9. Funil de captação de leads (novo contato → qualificação → cliente)
10. Dashboard com indicadores (clientes ativos, processos em andamento, taxa de conversão de leads)
11. Agenda de compromissos e reuniões com clientes
12. Upload e organização de documentos fiscais por cliente
13. Módulo de anotações internas por processo
14. Relatórios de produtividade por colaborador
15. Notificações automáticas para clientes sobre status do processo
16. Controle de permissões (o que cada colaborador pode ver/editar)
17. Histórico de mudanças/log de auditoria em processos sensíveis
18. Área de FAQ/base de conhecimento interna para dúvidas frequentes
19. Exportação de relatórios em PDF

---

## 4. Benchmarking (Sistemas Similares)

| Critério | Sistema A — RD Station CRM | Sistema B — Sage/Domínio Sistemas (gestão contábil) |
|---|---|---|
| **Foco principal** | Funil de vendas e captação de leads, genérico para qualquer negócio | Gestão contábil completa (fiscal, folha, processos) |
| **Centralização de atendimento** | Integra WhatsApp, e-mail e redes sociais em um só painel | Foco mais operacional/fiscal, pouca integração com redes sociais |
| **Distribuição de tarefas entre equipe** | Possui atribuição de responsáveis e funil visual (kanban) | Possui controle de processos por responsável, mas com interface mais técnica/administrativa |

**Conclusão do benchmarking:** O sistema ideal para a Moura Assessoria une o melhor dos dois mundos — a centralização de atendimento e funil de captação (como no RD Station) com o acompanhamento de processos fiscais e prazos (como nos sistemas de gestão contábil), mas em uma versão simplificada, pensada para uma microempresa com poucos colaboradores.

---

## 5. Lista de Requisitos

### Requisitos Funcionais (RF)
1. O sistema deve permitir o cadastro de clientes (pessoa física e jurídica).
2. O sistema deve permitir o cadastro de colaboradores com diferentes níveis de acesso.
3. O sistema deve permitir o registro de solicitações/atendimentos vinculados a um cliente.
4. O sistema deve exibir o histórico de interações de cada cliente.
5. O sistema deve permitir atribuir um colaborador responsável a cada processo ou atendimento.
6. O sistema deve permitir o acompanhamento do status de cada processo fiscal (ex: em andamento, aguardando documentação, concluído).
7. O sistema deve emitir alertas de prazos fiscais próximos do vencimento.
8. O sistema deve permitir o registro manual de leads captados via redes sociais.
9. O sistema deve exibir um painel (dashboard) com indicadores gerais (clientes ativos, processos em andamento, leads em funil).
10. O sistema deve permitir o upload e organização de documentos por cliente.
11. O sistema deve permitir gerar relatórios de produtividade por colaborador.
12. O sistema deve permitir exportar relatórios em PDF.

### Requisitos Não-Funcionais (RNF)
1. O sistema deve garantir a segurança dos dados fiscais e pessoais dos clientes (criptografia e controle de acesso).
2. O sistema deve ter interface simples e intuitiva, adequada a usuários com baixo nível de familiaridade tecnológica.
3. O sistema deve responder às ações do usuário em no máximo 2 segundos em operações comuns.
4. O sistema deve estar disponível (uptime) em pelo menos 99% do tempo.
5. O sistema deve permitir acesso via navegador web, sem necessidade de instalação local.
6. O sistema deve manter logs de auditoria de alterações em dados sensíveis.

---

## 6. Contrato de Colaboração (Adaptado — Trabalho Individual)

> Observação: como o projeto está sendo realizado individualmente (e não em dupla, conforme originalmente sugerido), este "contrato" foi adaptado para servir como um planejamento pessoal de trabalho.

- **Ferramentas de organização:** Google Docs (documentação), draw.io (diagramas UML), GitLab (versionamento)
- **Frequência de trabalho:** Sessões dedicadas ao projeto pelo menos 2x por semana, alinhadas ao cronograma de 4 sprints
- **Critério de divisão de tarefas:** Não se aplica (trabalho individual) — todas as etapas são de responsabilidade única
- **Processo de decisão:** Decisões técnicas registradas no README do repositório, com justificativa breve (ex: "Escolhi X porque Y")
- **Comunicação com o professor:** Em caso de dificuldade, registrar no relatório semanal e buscar orientação no encontro semanal

