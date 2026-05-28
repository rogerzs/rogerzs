# Paste into Google Doc
# Target: https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit?tab=t.0
# Source: Glean-Prod Daily Meeting Recap posted 2026-05-28 11:02 UTC (meetings held 2026-05-27)
# Email: not verified (no Gmail MCP)

---

28/05/2026
Identity Fraud - Platform - Eng Daily
Resume
Daily de engenharia da plataforma Identity Fraud (27/05, 14:00–14:15 BRT). Cerimônia de sincronização padrão (status, bloqueios, próximos passos). Não havia transcript ou notas Gemini detalhadas disponíveis no recap — conteúdo individual por participante não foi recuperado.
Link to gemini note complete
Transcript não encontrado (reunião de 27/05/2026)

---

28/05/2026
Nikolas / Luis
Resume
1:1 entre Nikolas Casanova e Luis Ost (27/05, 14:15–14:30 BRT). Sincronização rápida sem transcript ou notas capturadas; tópicos exatos não documentados na fonte disponível.
Link to gemini note complete
Transcript não encontrado (reunião de 27/05/2026)

---

28/05/2026
[Identity Fraud Defenses] Weekly Monitoring
Resume
Revisão semanal de métricas operacionais e de performance de fraudes (BR, CO, MX). Novos membros Matias Roqueta e Igor Amaral apresentados. No Brasil, queda na captura automática (Psyduck): fraudadores criam conta e fazem cross-sell imediato para crédito com score baixo. Colômbia/México: alerta de calibração na estimativa de idade (AWS Rekognition) — monitorar distribuição de idades. Perdas no BR caíram com New Pay, mas cartão e Pix seguem altos (possível migração de modus operandi). Debate sobre separar políticas de conta vs. cartão no BR e limpar backlog de auditoria no MX. Outputs: requisito de monitorar distribuição de previsões de idade do provedor externo. Próximos passos: Matias/Igor em 1:1s de onboarding; Julio atualiza visões com true precision, filas dos detectores e 3 exemplos do erro de idade; time adiciona monitoramento de distribuição de idades e melhorias rápidas na política de cartão.
Link to gemini note complete
https://docs.google.com/document/d/16WGUYUjy5Yoj7FHC_hOkPnZmPJEkMjxcchotMsnIEVk/edit

---

28/05/2026
Incode & Nubank
Resume
Alinhamento técnico com Incode sobre DeepSite e documentos digitais. Diferença iOS (imagem de profundidade real) vs. Android (camera trust). Incode oferece Multimodal Intelligence para rodar checagens de profundidade/vídeo em shadow mode sem alterar score final imediato. Configurações compartilhadas BR+CO exigem cuidado ao ativar. CNH digital: PDF sem assinatura verificável; QR Code via Serpro; validação depende de face matching e base governamental. Pendências Colômbia (faturas) e evolução SDK UXP2. Decisão: ativar DeepSite em produção com checagens em shadow mode. Próximos passos: Luis revisar casos em que liveness passou e DeepSite falharia; Héctor analisar vídeos e roadmap anti-doc IA; May confirmar UXP2 com Issa e pagamento fixed fee CO.
Link to gemini note complete
https://docs.google.com/document/d/1XHfcuG3w326JP6D_ldEzy54SMkMev3iIo-8vwnehCwE/edit
