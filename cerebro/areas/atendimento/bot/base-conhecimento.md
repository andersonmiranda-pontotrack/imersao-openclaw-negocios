# Base de Conhecimento — OpenClawzinho

> Tudo que o bot sabe responder. Cresce automaticamente via cron.
> Última atualização: 2026-03-26

---

## 🚀 PRIMEIROS PASSOS

**P: Como acesso o OpenClaw depois de comprar?**
R: Após a confirmação do pagamento, você recebe um email com o link de instalação e o token de acesso. O processo leva menos de 10 minutos. Se não recebeu em até 15 minutos, verifique spam ou fale com a gente pelo Telegram: @openclawsuporte.

**P: O OpenClaw funciona no Windows, Mac e Linux?**
R: Sim, funciona nos três sistemas operacionais. Precisa do Node.js instalado (versão 18 ou superior). O guia completo de instalação está em docs.openclaw.ai.

**P: Precisa saber programar para usar o OpenClaw?**
R: Não. O OpenClaw foi desenhado para empreendedores não-técnicos. Você configura tudo em linguagem natural — descreve o que quer, o agente faz. Não precisa escrever código.

**P: Quanto tempo leva para ter o primeiro agente funcionando?**
R: Em média 30 minutos do zero ao primeiro agente respondendo. Se seguir o tutorial do Minicurso, você tem o assistente básico configurado em menos de 1 tarde.

---

## 💳 PLANOS E PAGAMENTO

**P: Quais são os planos disponíveis?**
R: Temos três opções: **TechFlow Starter** (R$97 — curso gravado de 4h, do zero à primeira automação), **TechFlow Pro** (R$297/mês — plataforma SaaS completa + suporte), **TechFlow Enterprise** (R$1.497/mês — tudo do Pro + onboarding dedicado + SLA). Veja detalhes em techflow.ai/planos.

**P: Tem garantia?**
R: Sim. 7 dias de garantia incondicional em todos os produtos. Se não gostar por qualquer motivo, devolvemos 100% do valor. Basta enviar email para financeiro@techflow.ai.

**P: Posso parcelar?**
R: Sim. Aceitamos parcelamento em até 12x no cartão de crédito. No PIX tem 10% de desconto. O link de pagamento já mostra as opções.

**P: Qual a diferença entre o Pro e o Enterprise?**
R: O Pro dá acesso à plataforma completa com suporte via chat. O Enterprise inclui tudo do Pro + onboarding personalizado, gerente de sucesso dedicado, SLA de 4h e integrações customizadas com ERPs e CRMs.

---

## 🤖 USO DA PLATAFORMA

**P: O que é uma skill?**
R: Uma skill é uma receita de automação — você descreve o processo em linguagem natural (o que fazer, com quais dados, qual o formato de saída) e o agente executa sempre que você chamar. É como uma função, mas escrita em português.

**P: O que é o Cérebro?**
R: O Cérebro é o repositório GitHub que serve como memória persistente do seu agente. Enquanto o agente "pensa" em tempo real, o Cérebro guarda tudo que importa: contexto da empresa, skills, rotinas, learnings. Sem o Cérebro, o agente esquece tudo ao fechar a sessão.

**P: Como conecto o OpenClaw ao Telegram?**
R: Crie um bot no BotFather do Telegram, copie o token, e configure no OpenClaw com o comando `openclaw channels add telegram --token SEU_TOKEN`. Em 2 minutos seu agente está respondendo no Telegram.

**P: Posso ter mais de um agente?**
R: Sim. O OpenClaw suporta múltiplos agentes, cada um com personalidade, escopo e canal diferentes. Um assistente geral, um agente de marketing, um bot de suporte — cada um configurado separadamente.

**P: O que é um cron?**
R: Cron é um agendamento. Você define que uma skill roda em horário específico — por exemplo, todo dia às 9h gera e envia o relatório de vendas. O agente executa sozinho, sem você precisar pedir.

---

## 🔧 TÉCNICO

**P: O OpenClaw funciona com o Claude, GPT e outros modelos?**
R: Sim. O OpenClaw é compatível com os principais modelos de IA: Claude (Anthropic), GPT-4 (OpenAI), Gemini (Google) e modelos locais via Ollama. Você escolhe qual usar em cada agente.

**P: Meus dados ficam seguros? O modelo de IA vê meus dados?**
R: O OpenClaw roda localmente na sua máquina ou servidor. Seus arquivos ficam no seu repositório GitHub (privado). O modelo processa os dados durante a execução, mas não armazena. Nenhum dado fica em servidor da OpenClaw.

**P: Meu agente parou de responder. O que fazer?**
R: Verifique: (1) serviço rodando — execute `openclaw status`; (2) chave de API do modelo configurada e com crédito; (3) token do Telegram válido. Se o problema persistir, mande print do erro pelo Telegram @openclawsuporte.

**P: Como faço backup do meu Cérebro?**
R: O Cérebro é um repositório GitHub — o backup é automático a cada `git push`. Se o agente faz commits automaticamente (configuração padrão), você já tem histórico completo de toda evolução.

---

## 📦 COMUNIDADE E SUPORTE

**P: Como acesso a comunidade?**
R: A comunidade está no Telegram. Após a compra, você recebe o link de acesso por email. Grupo principal + canais por área (marketing, produto, atendimento, etc.).

**P: Posso pedir suporte para configurar meu Cérebro?**
R: Sim. No TechFlow Pro tem suporte via chat em horário comercial. No TechFlow Enterprise tem suporte prioritário com SLA de 4h + gerente de sucesso dedicado.

---

## 🔄 RESPOSTAS ADICIONADAS VIA CRON

*(novas entradas são adicionadas aqui automaticamente pelo cron consolidar-kb)*
