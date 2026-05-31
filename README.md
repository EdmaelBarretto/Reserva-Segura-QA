<div align="center">

<img src="https://img.shields.io/badge/QA-Quality%20Assurance-2D6A4F?style=for-the-badge&logoColor=white"/>
<img src="https://img.shields.io/badge/Status-Em%20Progresso-F4A261?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Cobertura%20Auth-100%25-52B788?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Sprint-1-457B9D?style=for-the-badge"/>

# 🛡️ Reserva Segura — QA Repository

**Repositório oficial de Qualidade de Software do projeto Reserva Segura**

*Residência Tecnológica Take Off · Squad 29 · Bradesco 2026.1*

[🌐 Produção](https://projeto-reserva-segura-front-end.vercel.app/) · [📦 Back-End](https://github.com/EdmaelBarretto/ProjetoReservaSegura_Back-End) · [🎨 Front-End](https://github.com/EdmaelBarretto/Projeto-Reserva-Segura_Take-Off) · [🛡️ QA](https://github.com/EdmaelBarretto/Reserva-Segura-QA)

</div>

---

## 👥 Equipe — Squad 29

**Código/Sigla:** RS · **Nome do Projeto:** RESERVA SEGURA

| Nome | Papel |
|------|-------|
| Agnes Letícia Soares Ribeiro | Front-End |
| Allan Harrison Lemos de Barros Falcão | Front-End |
| Ana Carolina da Silva Santos | Dados |
| Arthur Henrique Silveira de Paula | Design |
| Edmael Paulo Ribeiro Barreto | Back-End / QA |
| Gabriel Gleydson Lima dos Santos | Dados / Gestão |

---

## 📋 Índice

- [Sobre este Repositório](#-sobre-este-repositório)
- [Visão Geral do Produto](#-visão-geral-do-produto)
- [Arquitetura do Sistema](#-arquitetura-do-sistema)
- [Ambientes de Teste](#-ambientes-de-teste)
- [Estratégia de Testes](#-estratégia-de-testes)
- [Plano de Testes](#-plano-de-testes)
- [Cenários de Teste — Resultados](#-cenários-de-teste--resultados)
- [Como Executar os Testes](#-como-executar-os-testes)
- [Estrutura de Evidências](#-estrutura-de-evidências)
- [Rastreabilidade de Bugs](#-rastreabilidade-de-bugs)
- [Métricas de Qualidade](#-métricas-de-qualidade)
- [Definição de Pronto (DoD)](#-definição-de-pronto-dod)
- [Roadmap de Automação](#-roadmap-de-automação)
- [Convenções e Contribuição](#-convenções-e-contribuição)

---

## 📌 Sobre este Repositório

Este repositório centraliza todos os artefatos de **Quality Assurance** do sistema Reserva Segura. O objetivo é garantir a rastreabilidade completa entre requisitos, casos de teste, execuções e evidências, promovendo a qualidade de forma contínua ao longo do desenvolvimento.

**O que você encontra aqui:**

| Artefato | Descrição |
|---|---|
| 📄 Plano de Testes | Estratégia, escopo, critérios de entrada/saída |
| 🧪 Casos de Teste | CTs documentados por módulo com pré-condições e passos |
| 📸 Evidências | Screenshots e logs organizados por CT |
| 🐛 Bug Report | Rastreamento de defeitos com severidade e status |
| 📊 Métricas | Cobertura, taxa de aprovação e indicadores de qualidade |
| ⚙️ Scripts `.http` | Requisições versionadas para o HTTP Client do IntelliJ |

---

## 🎯 Visão Geral do Produto

O **Reserva Segura** é uma plataforma gamificada de educação financeira e poupança. O sistema permite que usuários criem metas de poupança ("caixinhas"), realizem depósitos, acompanhem seu progresso e sejam recompensados por meio de um sistema de XP, badges, missões diárias e ligas — tornando o hábito de poupar uma jornada motivadora.

**Principais módulos funcionais sob teste:**

- 🔐 Autenticação (registro, login, JWT)
- 🎯 Metas de poupança — Goals (CRUD completo)
- 💸 Transações e depósitos
- 👤 Perfil do usuário (XP, pontos, nível)

---

## 🏗️ Arquitetura do Sistema

```
┌─────────────────────────────────────────────────────────┐
│                    RESERVA SEGURA                       │
├──────────────────┬──────────────────┬───────────────────┤
│    FRONT-END     │    BACK-END      │   BANCO DE DADOS  │
│                  │                  │                   │
│  React + Vite    │  Java 17         │  PostgreSQL       │
│  Tailwind CSS    │  Spring Boot     │  Railway          │
│                  │  3.2.5           │                   │
│  Vercel          │  Railway         │  turntable.proxy  │
│                  │                  │  .rlwy.net:18662  │
└──────────────────┴──────────────────┴───────────────────┘
```

**Repositórios:**

| Camada | Repositório | Deploy |
|---|---|---|
| 🎨 Front-End | [Projeto-Reserva-Segura_Take-Off](https://github.com/EdmaelBarretto/Projeto-Reserva-Segura_Take-Off) | [Vercel](https://projeto-reserva-segura-front-end.vercel.app/) |
| ⚙️ Back-End | [ProjetoReservaSegura_Back-End](https://github.com/EdmaelBarretto/ProjetoReservaSegura_Back-End) | Railway |
| 🛡️ QA | [Reserva-Segura-QA](https://github.com/EdmaelBarretto/Reserva-Segura-QA) | — |

**Estrutura de pacotes — Back-End:**

```
br.com.reservasegura
├── controller/
│   ├── AuthController.java         ← /auth/register, /auth/login
│   ├── GoalController.java         ← /metas (CRUD)
│   └── TransactionController.java  ← /movimentacoes
├── dto/                            ← Request/Response objects
├── entity/                         ← User, Goal, Transaction
├── exception/                      ← GlobalExceptionHandler
├── repository/                     ← Spring Data JPA interfaces
├── security/                       ← JwtFilter, JwtService, SecurityConfig
└── service/                        ← Regras de negócio
```

**Modelo de dados:**

| Entidade | Tabela | Campos principais |
|---|---|---|
| `User` | `usuario` | id, nome, email, cpf, senha, xp_total, pontos_premio |
| `Goal` | `meta_reserva` | id, nome, valor_alvo, valor_atual, user_id (FK) |
| `Transaction` | `movimentacoes` | id, valor, tipo, criado_em, goal_id (FK), user_id (FK) |

**Fluxo de autenticação JWT:**

```
Cliente → POST /auth/register ou /auth/login
       → JwtFilter (verifica Bearer token no header)
       → SecurityConfig (rotas públicas: /auth/**)
       → AuthController (valida body da requisição)
       → UserRepository (consulta/persiste no PostgreSQL)
       → JwtService (gera token assinado)
       → AuthResponse: { token, userId, nome } — 200 OK
```

---

## 🌍 Ambientes de Teste

| Ambiente | Front-End | Back-End | Banco |
|---|---|---|---|
| **Desenvolvimento** | `localhost:5173` | `localhost:8080` | Railway (PostgreSQL) |
| **Produção** | [projeto-reserva-segura-front-end.vercel.app](https://projeto-reserva-segura-front-end.vercel.app/) | Railway | Railway (PostgreSQL) |

---

## 🧠 Estratégia de Testes

### Pirâmide de Testes

```
              ╱▔▔▔▔╲
             ╱   E2E    ╲          🔲 Planejado (Cypress / Playwright)
            ╱────────────╲
           ╱  Integração  ╲       🔲 Planejado (Spring Boot Test)
          ╱────────────────╲
         ╱  Funcionais / API╲    ✅ Em execução (IntelliJ HTTP Client)
        ╱────────────────────╲
       ╱      Unitários       ╲   🔲 Planejado (JUnit 5 + Mockito)
      ╱────────────────────────╲
```

### Tipos de teste aplicados

| Tipo | Técnica | Módulos cobertos |
|---|---|---|
| Caixa-preta | Validação de entradas/saídas da API | Auth, Goals, Transactions |
| Particionamento de equivalência | Cenários positivos e negativos por endpoint | Todos |
| Análise de valor limite | Campos obrigatórios, duplicatas, body vazio | Auth |
| Teste de segurança básico | Acesso a rotas protegidas sem/com token | Goals, Transactions |
| Teste de integração manual | Front-end ↔ Back-end ↔ Banco | Fluxo completo |

### Ferramentas

| Ferramenta | Finalidade | Status |
|---|---|---|
| IntelliJ HTTP Client | Execução manual de testes de API | ✅ Em uso |
| Arquivos `.http` | Scripts de requisição versionados no repositório | ✅ Em uso |
| Railway Dashboard | Verificação do estado do banco em produção | ✅ Em uso |
| GitHub Issues | Rastreamento de bugs e pendências | ✅ Em uso |
| Postman / Newman | Automação e CI dos testes de API | 🔲 Planejado |
| JUnit 5 + Mockito | Testes unitários de services e repositories | 🔲 Planejado |
| Cypress | Testes E2E no front-end (Vercel) | 🔲 Planejado |

---

## 📝 Plano de Testes

### Escopo

**Incluído:**
- API REST — todos os endpoints documentados
- Fluxo de autenticação completo (registro → login → token → acesso)
- CRUD de Goals e Transactions com autorização JWT
- Validações de campos e tratamento de erros (4xx)
- Acesso ao ambiente de produção (Vercel + Railway)

**Excluído (sprint atual):**
- Testes de performance e carga
- Testes de segurança avançados (pentest)
- Testes de acessibilidade no front-end

### Critérios de entrada

- [ ] Back-end rodando em `localhost:8080` ou Railway
- [ ] Banco PostgreSQL acessível via Railway
- [ ] Variável `{{token}}` configurada no ambiente HTTP Client para CTs autenticados

### Critérios de saída

- [ ] 100% dos CTs de autenticação executados
- [ ] 100% dos CTs de rotas autenticadas executados com token válido
- [ ] Zero bugs de severidade **Alta** em aberto
- [ ] Evidências anexadas para todos os CTs executados

---

## 🧪 Cenários de Teste — Resultados

> **Legenda de status:** ✅ Passou · ⚠️ Parcial / Pendente · ❌ Falhou · 🔲 Não executado

---

### Módulo: Autenticação — `/auth`

**Ferramenta:** IntelliJ HTTP Client · **Ambiente:** `localhost:8080` · **Data:** 10/05/2026

| CT | Tipo | Endpoint | Método | Pré-condição | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|---|---|---|
| CT01 | Positivo | `/auth/register` | POST | Usuário não cadastrado | 200 OK + `{ token, userId, nome }` | 200 OK + token JWT | ✅ |
| CT02 | Negativo | `/auth/register` | POST | Email já existente no banco | 400 Bad Request + mensagem de erro | 400 + "Email já cadastrado" | ✅ |
| CT03 | Negativo | `/auth/register` | POST | CPF já existente no banco | 400 Bad Request + mensagem de erro | 400 + "CPF duplicado" | ✅ |
| CT04 | Negativo | `/auth/register` | POST | Body com campos vazios (`""`) | 400 Bad Request — validação de campos | 400 + erros de validação | ✅ |
| CT05 | Negativo | `/auth/register` | POST | Body ausente na requisição | 400 Bad Request — campos obrigatórios | 400 + campos obrigatórios | ✅ |
| CT06 | Positivo | `/auth/login` | POST | Usuário cadastrado, credenciais corretas | 200 OK + `{ token, userId, nome }` | 200 OK + token JWT | ✅ |
| CT07 | Negativo | `/auth/login` | POST | Senha incorreta para email existente | 401 Unauthorized | 403 / 401 | ✅ |
| CT08 | Negativo | `/auth/login` | POST | Email não cadastrado | 404 Not Found | 401 / 404 | ✅ |
| CT09 | Negativo | `/auth/login` | POST | Body ausente na requisição | 400 Bad Request — campos obrigatórios | 400 + campos obrigatórios | ✅ |

**Resultado do módulo:** `9/9 aprovados — 100% ✅`

---

### Módulo: Usuário — `/auth/usuario`

| CT | Tipo | Endpoint | Método | Pré-condição | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|---|---|---|
| CT10 | Positivo | `/auth/usuario/{id}` | GET | Token JWT válido no header | 200 OK + dados do usuário autenticado | A validar | ⚠️ |

---

### Módulo: Metas — `/metas`

| CT | Tipo | Endpoint | Método | Pré-condição | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|---|---|---|
| CT11 | Positivo | `/metas` | POST | Token válido + body com nome e valorAlvo | 200 Created + meta criada | A validar | ⚠️ |
| CT12 | Positivo | `/metas?userId={id}` | GET | Token JWT válido no header | 200 OK + lista de metas do usuário | 403 sem token | ⚠️ |
| CT15 | Positivo | `/metas/{id}` | PUT | Token válido + ID de meta existente | 200 OK + meta atualizada | A validar | ⚠️ |
| CT16 | Positivo | `/metas/{id}` | DELETE | Token válido + ID de meta existente | 204 No Content | A validar | ⚠️ |

---

### Módulo: Transações — `/movimentacoes`

| CT | Tipo | Endpoint | Método | Pré-condição | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|---|---|---|
| CT13 | Positivo | `/movimentacoes` | POST | Token válido + body com valor e goalId | 200 Created + transação registrada | A validar | ⚠️ |
| CT14 | Positivo | `/movimentacoes?userId={id}` | GET | Token JWT válido no header | 200 OK + lista de transações | 403 sem token | ⚠️ |

---

### Módulo: Deploy e Integração

| CT | Tipo | Descrição | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|---|
| CT17 | Integração | Deploy backend no Railway | Serviço online | Online ✅ | ✅ |
| CT18 | Integração | CORS bloqueando frontend Vercel | CORS configurado | Corrigido | ✅ |
| CT19 | Integração | VITE_API_URL apontando para produção | URL do Railway | Corrigido | ✅ |
| CT20 | Integração | Login funcionando em produção | 200 OK + token | Funcionando | ✅ |

> ⚠️ **Observação:** Os CTs 10–16 aguardam a configuração da variável `{{token}}` no HTTP Client do IntelliJ. Os retornos 403 observados são comportamento esperado de segurança.

---

## ▶️ Como Executar os Testes

### Pré-requisitos

- IntelliJ IDEA com suporte ao HTTP Client
- Back-end clonado e rodando em `localhost:8080`
- Conexão com o banco Railway configurada no `application.properties`

### Setup do ambiente

```bash
# 1. Clone o back-end
git clone https://github.com/EdmaelBarretto/ProjetoReservaSegura_Back-End
cd ProjetoReservaSegura_Back-End

# 2. Configure as credenciais no application.properties

# 3. Suba a aplicação
./mvnw spring-boot:run
```

### Scripts de referência

**CT01 — Cadastro com sucesso:**
```http
### CT01 - Registrar novo usuário
POST http://localhost:8080/auth/register
Content-Type: application/json

{
  "nome": "Edmael Barreto",
  "email": "edmael@teste.com",
  "cpf": "12345678901",
  "senha": "123456"
}
```

**CT06 — Login com sucesso:**
```http
### CT06 - Login com credenciais válidas
POST http://localhost:8080/auth/login
Content-Type: application/json

{
  "email": "edmael@teste.com",
  "senha": "123456"
}
```

**CT12 — Listar metas (autenticado):**
```http
### CT12 - Buscar todas as metas do usuário
GET http://localhost:8080/metas?userId={{userId}}
Authorization: Bearer {{token}}
```

**CT11 — Criar meta:**
```http
### CT11 - Criar nova meta de poupança
POST http://localhost:8080/metas
Content-Type: application/json
Authorization: Bearer {{token}}

{
  "nome": "Viagem para Europa",
  "valorAlvo": 20000.00,
  "userId": "{{userId}}"
}
```

---

## 📸 Estrutura de Evidências

```
evidencias/
├── auth/
│   ├── CT01_cadastro_sucesso.png         ✅ 200 OK + token JWT
│   ├── CT02_email_duplicado.png          ✅ 400 + "Email já cadastrado"
│   ├── CT03_cpf_duplicado.png            ✅ 400 + "CPF duplicado"
│   ├── CT04_campos_vazios.png            ✅ 400 + erros de validação
│   ├── CT05_sem_body.png                 ✅ 400 + campos obrigatórios
│   ├── CT06_login_sucesso.png            ✅ 200 OK + token + userId
│   ├── CT07_senha_invalida.png           ✅ 403/401 Unauthorized
│   ├── CT08_usuario_nao_encontrado.png   ✅ 401/404
│   └── CT09_login_sem_body.png           ✅ 400 + campos obrigatórios
├── metas/
│   └── CT12_get_sem_token.png            ⚠️ 403 Forbidden
└── movimentacoes/
    └── CT14_get_sem_token.png            ⚠️ 403 Forbidden
```

---

## 🐛 Rastreabilidade de Bugs

| ID | CT Relacionado | Descrição | Severidade | Status |
|---|---|---|---|---|
| BUG-01 | CT10–CT16 | Rotas autenticadas retornam 403 por ausência de Bearer token no ambiente de teste | Alta | 🔲 Em aberto |
| BUG-02 | CT07 | Retornou HTTP 403 em vez de 401 para senha inválida | Baixa | 🔲 Em análise |
| BUG-03 | CT08 | Retornou HTTP 401 em vez de 404 para e-mail inexistente | Baixa | 🔲 Em análise |

### Classificação de severidade

| Severidade | Critério |
|---|---|
| 🔴 Crítica | Sistema inoperante, perda de dados, falha de segurança grave |
| 🟠 Alta | Funcionalidade principal bloqueada, sem workaround |
| 🟡 Média | Funcionalidade degradada, workaround disponível |
| 🟢 Baixa | Comportamento diverge da spec, impacto mínimo ao usuário |

---

## 📊 Métricas de Qualidade

| Métrica | Valor atual |
|---|---|
| Total de CTs planejados | 20 |
| CTs executados | 13 |
| CTs aprovados (✅) | 13 |
| CTs com pendência (⚠️) | 7 |
| CTs com falha (❌) | 0 |
| Taxa de aprovação geral | 65% *(13/20)* |
| Taxa de aprovação — módulo Auth | **100%** *(9/9)* |
| Taxa de aprovação — Deploy/Integração | **100%** *(4/4)* |
| Bugs abertos | 3 |
| Bugs críticos | 0 |

---

## ✅ Definição de Pronto (DoD)

Um caso de teste é considerado **concluído** quando:

- [x] CT documentado com: ID, tipo, endpoint, método, pré-condição, resultado esperado e obtido
- [x] Evidência salva na pasta `/evidencias` com nomenclatura correta
- [x] Status atualizado na tabela de resultados
- [x] Bug registrado na tabela de rastreabilidade, se aplicável
- [ ] Cenário coberto por script automatizado *(meta futura)*
- [ ] CT revisado por outro membro do squad *(meta futura)*

---

## 🚀 Roadmap de Automação

| Fase | Objetivo | Ferramenta | Sprint |
|---|---|---|---|
| ✅ Fase 1 | Testes manuais de API — Auth | IntelliJ HTTP Client | Sprint 1 |
| 🔲 Fase 2 | Testes manuais — Goals e Transactions com token | IntelliJ HTTP Client | Sprint 2 |
| 🔲 Fase 3 | Automação dos CTs de API | Postman + Newman | Sprint 3 |
| 🔲 Fase 4 | Testes unitários de services | JUnit 5 + Mockito | Sprint 3 |
| 🔲 Fase 5 | Testes E2E no front-end | Cypress / Playwright | Sprint 4 |
| 🔲 Fase 6 | Integração dos testes ao CI/CD | GitHub Actions | Sprint 4 |

---

## 🤝 Convenções e Contribuição

### Nomenclatura de artefatos

| Artefato | Padrão | Exemplo |
|---|---|---|
| Caso de teste | `CT` + número (2 dígitos) | `CT17` |
| Bug | `BUG-` + número | `BUG-04` |
| Evidência | `CT[num]_[descricao].[ext]` | `CT17_create_goal_success.png` |

---

<div align="center">

**Links do projeto**

[🌐 Aplicação em Produção](https://projeto-reserva-segura-front-end.vercel.app/) · [⚙️ Repositório Back-End](https://github.com/EdmaelBarretto/ProjetoReservaSegura_Back-End) · [🎨 Repositório Front-End](https://github.com/EdmaelBarretto/Projeto-Reserva-Segura_Take-Off) · [🛡️ Repositório QA](https://github.com/EdmaelBarretto/Reserva-Segura-QA)

---

*Documentação de QA — Reserva Segura · Squad 29 · Bradesco 2026.1*

</div>
