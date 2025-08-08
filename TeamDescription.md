# Relatório Detalhado dos Sub-Agentes Claude Code

Este documento lista, detalha e recomenda práticas para todos os sub-agentes do seu repositório, organizando por domínios e funções, para garantir máxima eficiência, cobertura de todo o ciclo de vida de projetos e facilitar orquestração via Claude Code CLI.

---

## 1. Orquestração e Gestão

### project-orchestrator
- **Responsabilidade:** Orquestra todo o ciclo do projeto, aciona e sequencia os demais sub-agentes, controla fluxo macro e entrega final.
- **Relacionamentos:** Chama TeamConfigurator, ProjectAnalyst, ProductAnalyst, TechLeadOrchestrator, DocumentationSpecialist, QA, Security, Performance, FinOps.
- **Sugestão:** Adicionar matriz de entrada/saída clara, exemplos de fluxos customizados por stack.

### tech-lead-orchestrator
- **Responsabilidade:** Lidera decisões técnicas, define arquitetura e distribui tarefas entre especialistas conforme stack.
- **Relacionamentos:** Recebe briefing do ProjectOrchestrator; distribui para arquitetos backend, frontend, DB, DevOps, Security.
- **Sugestão:** Checklist de arquitetura no output.

### team-configurator
- **Responsabilidade:** Sugere/compõe automaticamente a equipe ideal de sub-agentes para o projeto, baseado em requisitos técnicos/negócio.
- **Relacionamentos:** Gera lista de sub-agentes para o ProjectOrchestrator acionar.
- **Sugestão:** Permitir seleção de nível de senioridade dos sub-agentes.

### project-analyst
- **Responsabilidade:** Modela épicos, features, atividades técnicas a partir de requisitos.
- **Relacionamentos:** Output para ProductAnalyst e TechLeadOrchestrator.
- **Sugestão:** Entregas em formato estruturado (YAML/JSON).

### product-analyst
- **Responsabilidade:** Traduz visão de produto e negócio para requisitos técnicos e métricas de sucesso.
- **Relacionamentos:** Trabalha junto com ProjectAnalyst.
- **Sugestão:** Outputs legíveis por humanos e máquinas (estruturar em tópicos).

---

## 2. Documentação e Qualidade

### documentation-specialist
- **Responsabilidade:** Geração e revisão de documentação técnica (README, ADR, docstrings, Swagger etc).
- **Relacionamentos:** Recebe insumos dos engenheiros/QA, entrega para ProjectOrchestrator.
- **Sugestão:** Adicionar modelos de documentação automatizada de APIs e fluxos CI/CD.

### code-reviewer
- **Responsabilidade:** Revisão de código (Clean Code, SOLID, performance, segurança), checklist de problemas por severidade.
- **Relacionamentos:** Avalia entregas de backend, frontend, DB, DevOps.
- **Sugestão:** Relatórios objetivos, outputs estruturados.

---

## 3. Backend (Engenharia & Arquitetura)

### backend-api-architect
- **Responsabilidade:** Define arquitetura de APIs backend (REST, GraphQL), padrões de autenticação, versionamento, escalabilidade.
- **Relacionamentos:** Recebe demanda do TechLeadOrchestrator; aciona BackendDeveloper e especialistas por stack.
- **Sugestão:** Exemplos de versionamento e fallback para OpenAPI/Swagger.

### backend-developer
- **Responsabilidade:** Implementação de APIs, lógica de negócio e integrações.
- **Relacionamentos:** Trabalha com BackendApiArchitect.

### [Stack Especialistas]
- **csharp-backend-engineer, python-backend-engineer, java-backend-engineer, php-backend-engineer, nodejs-developer, ruby-backend-engineer, etc.**
- **Responsabilidade:** Implementação e otimização conforme linguagem/plataforma.
- **Relacionamentos:** Chamados pelo TechLeadOrchestrator conforme stack definida.
- **Sugestão:** Usar sempre melhores práticas da stack, garantir integração com CI/CD.

### [Framework Specialists]
- **django-backend-expert, django-api-developer, django-orm-expert, laravel-backend-expert, laravel-eloquent-expert, rails-backend-expert, rails-activerecord-expert, rails-api-developer, cobol-developer**
- **Responsabilidade:** Implementação, tuning, queries, migrations, APIs, conforme framework.
- **Relacionamentos:** Seguem fluxo TechLead → BackendApiArchitect → [Stack Specialist].

---

## 4. Frontend

### frontend-developer
- **Responsabilidade:** Implementação frontend agnóstico, integração com especialistas React, Angular, Vue, etc.
- **Relacionamentos:** Chama especialistas por stack.
- **Sugestão:** Documentar padrões de integração com backend.

### [Stack Especialistas]
- **react-frontend-engineer, react-nextjs-expert, react-component-architect, angular-frontend-engineer, vue-frontend-engineer, vue-component-architect, vue-nuxt-expert, swiftui-architect, flutter-mobile-developer, flutter-tester, tailwind-css-expert, nextjs-project-bootstrapper, vue-state-manager**
- **Responsabilidade:** Implementação, arquitetura de componentes, SSR/SSG, integração com backend, estado, performance.
- **Relacionamentos:** Recebem briefing do FrontendDeveloper.
- **Sugestão:** Foco em integração fluida, performance e boas práticas de acessibilidade.

---

## 5. Database & Infraestrutura

### database-modeling-expert
- **Responsabilidade:** Modelagem de banco de dados relacional e não-relacional, normalização, integridade e performance.
- **Relacionamentos:** Escolhe DBA/DB expert por stack.

### [Especialistas]
- **sql-engineer, oracle-dba, postgresql-expert, mongodb-specialist, redis-architect**
- **Responsabilidade:** Implementação, tuning, scripts e manutenção conforme banco.
- **Relacionamentos:** Trabalham após DatabaseModelingExpert.
- **Sugestão:** Referenciar documentação oficial sempre.

### devops-engineer
- **Responsabilidade:** CI/CD, automação, observabilidade, infraestrutura como código (IaC).
- **Relacionamentos:** Provisionamento paralelo ao desenvolvimento.

### devsecops-engineer
- **Responsabilidade:** Segurança e automação DevSecOps.
- **Relacionamentos:** Atua junto do DevOpsEngineer.

### terraform-infrastructure-builder
- **Responsabilidade:** Provisionamento IaC com Terraform.
- **Relacionamentos:** Chamado pelo DevOpsEngineer.

---

## 6. Segurança

### security-architect
- **Responsabilidade:** Padrões de arquitetura segura, requisitos de segurança, compliance.
- **Relacionamentos:** Aciona SecurityAuditSpecialist e SecurityTester.

### security-audit-specialist
- **Responsabilidade:** Auditoria, pentest, análise de vulnerabilidades.
- **Relacionamentos:** Repasse findings para SecurityArchitect e ProjectOrchestrator.

### security-tester
- **Responsabilidade:** Execução de testes de segurança (DAST, SAST, fuzzing etc).
- **Relacionamentos:** Apoio operacional para auditoria.

---

## 7. QA & Testes

### qa-test-engineer
- **Responsabilidade:** Geração de casos de teste, scripts automatizados.
- **Relacionamentos:** Aciona TestAutomationSpecialist, ManualQAAnalyst e FlutterTester.

### manual-qa-analyst
- **Responsabilidade:** Roteiros e execuções de testes manuais.

### test-automation-specialist
- **Responsabilidade:** Automação de testes end-to-end (Selenium, Cypress, etc.).

### flutter-tester
- **Responsabilidade:** Testes em apps mobile Flutter.

---

## 8. Performance, FinOps, Observabilidade

### performance-optimizer
- **Responsabilidade:** Otimização de performance (backend, frontend, banco, mobile).
- **Relacionamentos:** Atua após QA, em paralelo com Security e FinOps.

### finops-analyst
- **Responsabilidade:** Controle de custos, análise financeira de cloud.

---

## 9. Machine Learning & GraphQL

### ml-engineer
- **Responsabilidade:** Implementação de pipelines e soluções ML, integração com APIs e dados do projeto.

### graphql-specialist
- **Responsabilidade:** Design, implementação e tuning de APIs GraphQL.

---

## 10. Bootstrap & Templates

### nextjs-project-bootstrapper
- **Responsabilidade:** Criar projeto Next.js padrão enterprise, configuração inicial, integração com backend.

---

## 11. COBOL

### cobol-developer
- **Responsabilidade:** Manutenção e evolução de sistemas COBOL.

---

## Melhores Práticas Gerais

- **Prompts objetivos e outputs estruturados.**
- **Referenciar documentação oficial/atualizada.**
- **Adicionar campo `last-reviewed` no frontmatter para rastreabilidade.**
- **Handoff claro entre agentes de análise, orquestração e execução técnica.**
- **Orquestração (TeamConfigurator/ProjectOrchestrator) define o fluxo conforme stack.**
- **Padronizar outputs para facilitar automação e auditoria.**

---

> *Este documento é uma referência viva. Adapte, expanda e mantenha atualizado conforme surgirem novos agentes ou evoluírem os fluxos do projeto!*