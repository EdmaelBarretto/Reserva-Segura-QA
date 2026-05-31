<div align="center">

# Reserva Segura — QA

**Repositório de Qualidade de Software**
Residência Tecnológica Take Off · Squad 29 · Bradesco 2026.1

[![Status](https://img.shields.io/badge/Status-Em%20Progresso-F4A261?style=flat-square)](.)
[![Auth](https://img.shields.io/badge/Auth-100%25%20aprovado-52B788?style=flat-square)](.)
[![Sprint](https://img.shields.io/badge/Sprint-1-457B9D?style=flat-square)](.)
[![JMeter](https://img.shields.io/badge/JMeter-Executado-E25C2C?style=flat-square)](.)

[Produção](https://projeto-reserva-segura-front-end.vercel.app/) · [Back-End](https://github.com/EdmaelBarretto/ProjetoReservaSegura_Back-End) · [Front-End](https://github.com/EdmaelBarretto/Projeto-Reserva-Segura_Take-Off)

</div>

---

## Equipe

| Nome | Papel |
|------|-------|
| Agnes Letícia Soares Ribeiro | Front-End |
| Allan Harrison Lemos de Barros Falcão | Front-End |
| Ana Carolina da Silva Santos | Dados |
| Arthur Henrique Silveira de Paula | Design |
| Edmael Paulo Ribeiro Barreto | Back-End / QA |
| Gabriel Gleydson Lima dos Santos | Dados / Gestão |

---

## Sobre

Este repositório centraliza os artefatos de QA do sistema **Reserva Segura** — plataforma gamificada de educação financeira e poupança. Cobre testes funcionais de API, testes de integração e testes de performance com Apache JMeter.

**Stack testada:** React + Vite (Vercel) · Java 17 / Spring Boot 3.2.5 (Railway) · PostgreSQL (Railway)

---

## Estratégia

| Tipo | Ferramenta | Escopo | Status |
|------|-----------|--------|--------|
| Testes de API (caixa-preta) | IntelliJ HTTP Client | Auth, Goals, Transactions | ✅ Em execução |
| Testes de carga | Apache JMeter | Front-end (Vercel) | ✅ Executado |
| Testes de stress | Apache JMeter | Front-end (Vercel) | ✅ Executado |
| Testes unitários | JUnit 5 + Mockito | Services, Repositories | 🔲 Planejado |
| Testes E2E | Cypress / Playwright | Front-end | 🔲 Planejado |
| Automação de API | Postman + Newman | Todos os endpoints | 🔲 Planejado |

---

## Resultados — Testes Funcionais de API

> ✅ Passou · ⚠️ Pendente · ❌ Falhou · 🔲 Não executado

### Autenticação `/auth`

| CT | Cenário | Método | Status |
|----|---------|--------|--------|
| CT01 | Registro com dados válidos → 200 + token JWT | POST `/auth/register` | ✅ |
| CT02 | Registro com e-mail duplicado → 400 | POST `/auth/register` | ✅ |
| CT03 | Registro com CPF duplicado → 400 | POST `/auth/register` | ✅ |
| CT04 | Registro com campos vazios → 400 | POST `/auth/register` | ✅ |
| CT05 | Registro sem body → 400 | POST `/auth/register` | ✅ |
| CT06 | Login com credenciais válidas → 200 + token JWT | POST `/auth/login` | ✅ |
| CT07 | Login com senha incorreta → 401/403 | POST `/auth/login` | ✅ |
| CT08 | Login com e-mail inexistente → 401/404 | POST `/auth/login` | ✅ |
| CT09 | Login sem body → 400 | POST `/auth/login` | ✅ |

**9/9 aprovados · 100%**

### Usuário `/auth/usuario`

| CT | Cenário | Método | Status |
|----|---------|--------|--------|
| CT10 | Buscar dados do usuário autenticado → 200 | GET `/auth/usuario/{id}` | ⚠️ |

### Metas `/metas`

| CT | Cenário | Método | Status |
|----|---------|--------|--------|
| CT11 | Criar meta com token válido → 201 | POST `/metas` | ⚠️ |
| CT12 | Listar metas do usuário → 200 | GET `/metas?userId={id}` | ⚠️ |
| CT15 | Atualizar meta existente → 200 | PUT `/metas/{id}` | ⚠️ |
| CT16 | Deletar meta existente → 204 | DELETE `/metas/{id}` | ⚠️ |

### Transações `/movimentacoes`

| CT | Cenário | Método | Status |
|----|---------|--------|--------|
| CT13 | Registrar transação com token válido → 201 | POST `/movimentacoes` | ⚠️ |
| CT14 | Listar transações do usuário → 200 | GET `/movimentacoes?userId={id}` | ⚠️ |

### Deploy e Integração

| CT | Cenário | Status |
|----|---------|--------|
| CT17 | Back-end online no Railway | ✅ |
| CT18 | CORS configurado para o front-end Vercel | ✅ |
| CT19 | `VITE_API_URL` apontando para produção | ✅ |
| CT20 | Login funcionando em produção (Vercel + Railway) | ✅ |

> Os CTs 10–16 aguardam configuração do `{{token}}` no ambiente HTTP Client. Os retornos 403 observados são comportamento esperado de segurança (rotas protegidas por JWT).

---

## Resultados — Testes de Performance (Apache JMeter)

**Alvo:** `https://projeto-reserva-segura-front-end.vercel.app/` · **Data:** 31/05/2026

### Teste de Carga — 100 usuários

| Parâmetro | Valor |
|-----------|-------|
| Threads | 100 |
| Iterações | 10 |
| Total de requisições | 1.000 |
| Método | GET HTTPS |

| Métrica | Resultado | Status |
|---------|-----------|--------|
| % de Erro | 0,00% | ✅ |
| Tempo médio | 251 ms | ✅ |
| Tempo mínimo | 71 ms | ✅ |
| Tempo máximo | 2.117 ms | ✅ |
| Desvio padrão | 485,24 ms | ⚠️ |
| Throughput | 340,3 req/s | ✅ |

**✅ APROVADO** — Sistema estável para até 100 usuários simultâneos com 0% de erro.

---

### Teste de Stress — 10.000 usuários

| Parâmetro | Valor |
|-----------|-------|
| Threads | 10.000 |
| Iterações | 10 |
| Total de requisições | 100.000 |
| Método | GET HTTPS |

| Métrica | Resultado | Status |
|---------|-----------|--------|
| % de Erro | 88,08% | 🔴 |
| Tempo médio | 787 ms | ⚠️ |
| Tempo mínimo | 60 ms | — |
| Tempo máximo | 42.869 ms | 🔴 |
| Desvio padrão | 3.327,50 ms | 🔴 |
| Throughput | 1.884,2 req/s | ⚠️ |
| Tipo de erro | HTTP 403 Forbidden | 🔴 |

A Vercel ativou proteção automática contra abuso (`X-Vercel-Mitigated: deny`) após o volume de requisições ultrapassar o limite do plano gratuito, retornando 403 para 88% das requisições. O site ficou temporariamente inacessível no navegador para todos os usuários durante o teste.

**🔴 REPROVADO** — Ponto de ruptura entre 100 e 10.000 usuários simultâneos.

---

### Comparativo

| Métrica | Carga (100) | Stress (10.000) | Δ |
|---------|-------------|-----------------|---|
| Tempo médio | 251 ms | 787 ms | +213% |
| Tempo máximo | 2.117 ms | 42.869 ms | +1.925% |
| % de Erro | 0,00% | 88,08% | — |
| Throughput | 340,3 req/s | 1.884,2 req/s* | *88% erros |
| Resultado | ✅ Aprovado | 🔴 Reprovado | — |

---

## Bugs

| ID | CT | Descrição | Severidade | Status |
|----|----|-----------|------------|--------|
| BUG-01 | CT10–CT16 | Rotas autenticadas retornam 403 por ausência de Bearer token no ambiente de teste | Alta | 🔲 Em aberto |
| BUG-02 | CT07 | Retornou HTTP 403 em vez de 401 para senha inválida | Baixa | 🔲 Em análise |
| BUG-03 | CT08 | Retornou HTTP 401 em vez de 404 para e-mail inexistente | Baixa | 🔲 Em análise |
| BUG-04 | CT-PERF-02 | Rate limiting da Vercel bloqueia IP após ~10.000 req simultâneas (comportamento esperado da plataforma) | Média | ℹ️ Aceito |

---

## Métricas

| Métrica | Valor |
|---------|-------|
| CTs planejados | 22 |
| CTs executados | 15 |
| CTs aprovados | 15 |
| CTs pendentes | 7 |
| CTs com falha | 0 |
| Taxa de aprovação geral | 68% |
| Taxa de aprovação — Auth | **100%** |
| Taxa de aprovação — Deploy | **100%** |
| Bugs abertos | 3 |
| Bugs críticos | 0 |

---

## Como Executar

### Testes de API

```bash
# 1. Suba o back-end
git clone https://github.com/EdmaelBarretto/ProjetoReservaSegura_Back-End
cd ProjetoReservaSegura_Back-End
./mvnw spring-boot:run
# Disponível em localhost:8080
```

Abra os arquivos `.http` no IntelliJ IDEA e execute os CTs na ordem. Configure `{{token}}` com o JWT retornado pelo CT06 para executar os CTs autenticados (10–16).

```http
### CT06 - Login
POST http://localhost:8080/auth/login
Content-Type: application/json

{ "email": "usuario@teste.com", "senha": "123456" }
```

### Testes de Performance (JMeter)

1. Instale o [Apache JMeter 5.x](https://jmeter.apache.org/download_jmeter.cgi)
2. Crie um Plano de Teste com: **Grupo de Usuários → Requisição HTTP → Ouvintes**
3. Configure a requisição: `HTTPS · GET · projeto-reserva-segura-front-end.vercel.app`
4. Ajuste as threads conforme o teste e execute

> ⚠️ O teste de stress (10.000 threads) causa bloqueio temporário do IP pela Vercel. O site se recupera automaticamente em 15–60 minutos.

---

## Estrutura de Evidências

```
evidencias/
├── Reserva-Segura-QA/
│   ├── Relatorio_Edmael_ReservaSeguraBack-End.pdf
│   ├── Relatorio_JMeter_ReservaSegura.pdf


```

---

## Roadmap

| Fase | Entregável | Ferramenta | Sprint |
|------|-----------|-----------|--------|
| ✅ 1 | Testes manuais de API — Auth | HTTP Client | 1 |
| ✅ 1b | Testes de carga e stress | Apache JMeter | 1 |
| 🔲 2 | Testes manuais — Goals e Transactions | HTTP Client | 2 |
| 🔲 3 | Automação de API | Postman + Newman | 3 |
| 🔲 4 | Testes unitários | JUnit 5 + Mockito | 3 |
| 🔲 5 | Testes E2E | Cypress | 4 |
| 🔲 6 | CI/CD com testes | GitHub Actions | 4 |

---

<div align="center">
<sub>Reserva Segura · Squad 29 · Bradesco 2026.1</sub>
</div>
