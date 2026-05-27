# Conteúdo para colar no Google Doc

**Destino:** https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit?tab=t.0

**Metodologia desta execução (2026-05-27, janela ~1h até 14:02 UTC):**

- **E-mail (Gemini Notes):** não foi possível verificar a caixa de entrada — não há integração Gmail/MCP disponível neste agente.
- **Documento Google:** não editável a partir daqui (a página exige login).
- **Fonte usada:** mensagem pública no Slack `#nupay-engineering` marcada como gerada pelo Gemini (`(by Gemini)`), com carimbo de data dentro da janela solicitada (equivalente a ~13:57 UTC, 27/05/2026).

---

## Entrada 1 (cole abaixo no doc, no padrão pedido)

**2026-05-27**

**Estabilidade da tokenização do NuPay**

**Resume**

Resumo automático (Gemini) dos trade-offs discutidos na conversa sobre o crash IRC-24303 e o rollout da 99 Food:

- **Contrato Authlete (200→300 RPS) vs. causa raiz:** aumentar RPS pode servir como “seguro”, mas não resolve o padrão de uso do parceiro; há receio de escalar capacidade sem necessidade clara.
- **Rate limit imediato vs. solução estrutural:** ajuste no Abaddon como mitigação rápida de risco; cache visto como mitigação mais estrutural para reduzir chamadas e estabilizar o fluxo.
- **Rate limit por merchant/refresh token:** limitar parceiros que consomem capacidade compartilhada vs. complexidade de desenho e governança da capacidade.
- **Cache rápido vs. cache robusto/seguro:** debate entre implementação mais rápida para estabilidade imediata e solução mais segura em arquitetura; priorização de evitar interrupções, com entendimento de que proteção básica de tokens em cache seria viável.
- **Impacto merchant/customer vs. tempo de entrega:** rate limit mais simples entrega mais rápido; cache leva mais tempo para produção com segurança — trade-off entre velocidade da mitigação e robustez final.
- **Dependência de infra externa vs. controle NuPay:** depender só do parceiro/infra externa é insuficiente; decisão de assumir mais controle do lado NuPay para evitar recorrência.

*(Contexto adicional na thread, fora do bloco Gemini: 99Food com Payment Conditions chamando token de forma duplicada; discussão de segurança do cache vs. rate limit/429; ADR em elaboração.)*

**Link to gemini note complete**

https://nubank.enterprise.slack.com/archives/C02DGCNJE4X/p1779890237664609?thread_ts=1779883017.591259&cid=C02DGCNJE4X

*(Obs.: link aponta para a mensagem no Slack que contém o texto integral gerado pelo Gemini nesta thread. O URL oficial do artefato “Notes by Gemini” do Google Meet não foi recuperável sem acesso ao e-mail ou ao Drive do usuário.)*

---

## Padrão compacto (copiar/colar linha a linha no Doc)

```
2026-05-27
Estabilidade da tokenização do NuPay
[Resume em texto corrido ou bullets conforme acima]
https://nubank.enterprise.slack.com/archives/C02DGCNJE4X/p1779890237664609?thread_ts=1779883017.591259&cid=C02DGCNJE4X
```
