# Rotina: Follow-up de Leads Esfriando

## O que faz
Identifica leads sem contato há mais de 7 dias, classifica por urgência (valor do deal × tempo sem contato) e prepara lista priorizada com sugestão de abordagem pra cada um.

## Frequência
1x/dia — 03:00 BRT (06:00 UTC), seg a sex

## Skill utilizada
`areas/vendas/skills/leads-esfriando/SKILL.md`

## Entrega
- Alerta no tópico **💰 Vendas** do Telegram (topic_id: 4) às 08:30
- Notificação individual pro vendedor responsável se lead é crítico

## Exemplo de saída

```
🎯 Leads Esfriando — 27/03/2026

14 leads sem follow-up há +7 dias
💰 R$ 22.756 em risco

🔴 Críticos (ação hoje):
• Empresa X — R$ 8.500 — 12 dias sem contato — Vendedor: Felipe
  → Sugestão: ligar direto, mencionar case do setor dele
• Startup Y — R$ 4.200 — 9 dias — Vendedor: Ana
  → Sugestão: enviar material técnico, estava com dúvida de integração

🟡 Atenção (ação até amanhã):
• João — R$ 3.100 — 8 dias — Vendedor: Felipe
• Maria — R$ 2.956 — 7 dias — Vendedor: Ana
```

## Dados necessários
- `dados/leads.csv` (planilha de leads)
- `dados/vendas.csv` (pra cruzar conversão)

## Configuração do Cron

```
Nome: leads-esfriando-diario
Schedule: 0 6 * * 1-5  (3h BRT, seg-sex)
Prompt: "Roda a skill leads-esfriando e envia alerta no tópico de Vendas às 8:30"
Tópico: 💰 Vendas (topic_id: 4)
```

---

*Atualizado: março 2026*
