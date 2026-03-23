# Permissionamento — Pessoas & Agentes

> Quem pode o quê, tanto para pessoas quanto para agentes.

---

## Visão Geral

O sistema tem duas camadas de permissão:

1. **Pessoas** → quais agentes podem acionar + quais dados podem pedir
2. **Agentes** → quais pastas do cérebro acessam + qual tópico operam

```
┌─────────────────────────────────────────────────┐
│                    PESSOAS                       │
│  Ricardo (tudo), Felipe (tudo), André (tudo)     │
│  Camila (marketing), Juliana (vendas+atend.)     │
├─────────────────────────────────────────────────┤
│                    AGENTES                       │
│  Assistente Geral  →  empresa/ + todas as áreas │
│  Marcos (Vendas)   →  empresa/ + vendas/        │
│  Beatriz (Mkt)     →  empresa/ + marketing/     │
│  Clara (Atend.)    →  empresa/ + atendimento/   │
├─────────────────────────────────────────────────┤
│                    CÉREBRO                       │
│  empresa/ │ areas/ │ dados/ │ agentes/           │
└─────────────────────────────────────────────────┘
```

---

## Permissões de Pessoas

### Quem aciona qual agente

| Pessoa | Papel | Agentes que aciona | Pode ver dados de |
|--------|-------|-------------------|-------------------|
| Ricardo Mendes | Fundador | Todos | Tudo |
| Felipe Santos | CEO | Todos | Tudo |
| André Costa | COO | Todos | Tudo |
| Camila | Social media | Assistente Geral, Beatriz (Mkt) | Marketing, métricas gerais |
| Juliana | Suporte + vendas | Assistente Geral, Marcos (Vendas), Clara (Atend.) | Vendas, atendimento, métricas gerais |
| Lucas / Patrícia | Tráfego pago | Beatriz (Mkt) | Marketing (ads), métricas gerais |
| Marcos (designer) | Freelancer | Beatriz (Mkt) | Marketing (briefings), métricas gerais |

### O que cada nível de acesso significa

**Acesso total (liderança):**
- Pode pedir qualquer relatório, de qualquer área
- Pode ver dados financeiros, pipeline de leads, métricas de todas as áreas
- Pode alterar configurações de agentes e permissões
- `allowFrom: ["ricardo", "felipe", "andre"]`

**Acesso à área (equipe):**
- Pode pedir relatórios e dados da sua área
- Pode interagir com o agente da sua área
- Pode pedir métricas gerais da empresa (sem financeiro detalhado)
- NÃO pode ver pipeline de leads de vendas (se for de marketing)
- NÃO pode alterar configurações de agentes

### Configuração no OpenClaw

```json
{
  "agents": {
    "defaults": {
      "allowFrom": {
        "users": [
          { "id": "ricardo_id", "name": "Ricardo", "level": "admin" },
          { "id": "felipe_id", "name": "Felipe", "level": "admin" },
          { "id": "andre_id", "name": "André", "level": "admin" },
          { "id": "camila_id", "name": "Camila", "level": "area", "areas": ["marketing"] },
          { "id": "juliana_id", "name": "Juliana", "level": "area", "areas": ["vendas", "atendimento"] }
        ]
      }
    }
  }
}
```

---

## Permissões de Agentes

### Qual agente acessa o quê

| Agente | Persona | Acesso ao cérebro | Tópico Telegram | topic_id |
|--------|---------|-------------------|-----------------|----------|
| Assistente Geral | Generalista | `empresa/` + todas as `areas/` + `dados/` + `seguranca/` | General + qualquer tópico | 1 |
| Marcos Viana | Vendas consultivas | `empresa/` + `areas/vendas/` + `dados/vendas.csv` + `dados/leads.csv` | 💰 Vendas | 4 |
| Beatriz Almeida | Marketing digital | `empresa/` + `areas/marketing/` | 📢 Marketing | 3 |
| Clara Souza | Customer success | `empresa/` + `areas/atendimento/` | 🎧 Atendimento | 5 |

### Por que o Assistente Geral tem acesso total?

O Assistente Geral é o "gerente" dos outros agentes. Ele:
- Responde perguntas cross-área (que envolvem mais de uma área)
- Roda o heartbeat (precisa ver tudo pra checar saúde)
- Gerencia o repositório (sync, consolidação de memória)
- Faz o relatório de rotinas (monitora todos os crons)
- É o fallback quando um agente de área não está configurado

### Escopo limitado na prática

O agente de vendas (Marcos), por exemplo:
- ✅ Pode ler `empresa/contexto/empresa.md` (precisa saber os produtos)
- ✅ Pode ler `empresa/contexto/equipe.md` (precisa saber quem é quem)
- ✅ Pode ler `areas/vendas/` inteiro (é a área dele)
- ✅ Pode ler e escrever `dados/vendas.csv` e `dados/leads.csv`
- ❌ NÃO lê `areas/marketing/` (não é da conta dele)
- ❌ NÃO lê `areas/atendimento/` (mesmo que seja sobre um cliente)
- ❌ NÃO lê `seguranca/permissoes.md` (não precisa saber as regras globais)

Se um agente de área precisa de informação de outra área, ele pede ao Assistente Geral.

---

## Matriz Completa: Pessoa × Agente × Área

| Pessoa | Agente Geral | Marcos (Vendas) | Beatriz (Mkt) | Clara (Atend.) |
|--------|:---:|:---:|:---:|:---:|
| Ricardo (Fundador) | ✅ | ✅ | ✅ | ✅ |
| Felipe (CEO) | ✅ | ✅ | ✅ | ✅ |
| André (COO) | ✅ | ✅ | ✅ | ✅ |
| Camila (Social) | ✅ | ❌ | ✅ | ❌ |
| Juliana (Suporte) | ✅ | ✅ | ❌ | ✅ |
| Lucas (Tráfego) | ❌ | ❌ | ✅ | ❌ |
| Marcos (Design) | ❌ | ❌ | ✅ | ❌ |

---

## Modo Ask (Ações Sensíveis)

Independente do nível de acesso, algumas ações SEMPRE pedem confirmação:

| Ação | Quem pode aprovar |
|------|-------------------|
| Enviar email para cliente | Ricardo, Felipe, André |
| Publicar em rede social | Ricardo, Camila |
| Aprovar reembolso > R$ 200 | André |
| Alterar preço de produto | Ricardo, Felipe |
| Criar campanha de ads | Ricardo, Lucas/Patrícia |
| Alterar permissões de agentes | Ricardo, Felipe |

Configuração:
```
Modo: ask (pede confirmação antes de executar)
Ações em modo ask: envio de email, post público, reembolso, alteração de preço
```

---

## Evolução: Quando Adicionar Mais Agentes

A estrutura de permissionamento é escalável:

1. **Fase 1 (início):** Só o Assistente Geral → acesso total, uma pessoa configura
2. **Fase 2 (equipe de 5+):** Adicionar 1-2 agentes de área → menos gargalo
3. **Fase 3 (equipe de 10+):** Agente por área + sub-agentes especializados
   - Ex: Beatriz (Mkt) pode spawnar sub-agente só pra copywriting
   - Ex: Marcos (Vendas) pode spawnar sub-agente só pra qualificação de leads

Para adicionar um novo agente:
1. Criar pasta em `agentes/[nome-do-agente]/`
2. Criar `SOUL.md` com a persona especialista
3. Criar `AGENTS.md` com escopo e permissões
4. Atualizar este arquivo com as novas permissões
5. Configurar no OpenClaw apontando pro tópico correto

---

*Atualizado: março 2026*
