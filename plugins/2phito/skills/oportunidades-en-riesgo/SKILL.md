---
name: oportunidades-en-riesgo
description: Detecta oportunidades abiertas en riesgo (cierre vencido o próximo, sin actividad reciente o que retrocedieron de etapa). Usar cuando preguntan qué oportunidades están trabadas, atrasadas, frenadas o en riesgo.
---

1. Criterios por defecto (respetá los que indique el usuario): cierre vencido (`CloseDate < TODAY`), cierre en los próximos 14 días (`CloseDate = NEXT_N_DAYS:14`) o sin actividad en 30 días (`LastActivityDate < LAST_N_DAYS:30 OR LastActivityDate = null`). Si dicen "mis", agregá `OwnerId` del usuario actual (`getUserInfo`).
2. Consultá con `soqlQuery`:
   `SELECT Name, Account.Name, StageName, Amount, CloseDate, LastActivityDate, Owner.Name FROM Opportunity WHERE IsClosed = false AND (<criterios>) ORDER BY CloseDate LIMIT 50`
3. Solo si preguntan por retrocesos de etapa: `SELECT OpportunityId, StageName, CreatedDate FROM OpportunityHistory WHERE CreatedDate = LAST_N_DAYS:30 ORDER BY OpportunityId, CreatedDate LIMIT 200` y marcá las que pasaron a una etapa anterior.
4. Mostrá una tabla (oportunidad, cuenta, etapa, monto, cierre, última actividad, responsable) con una columna **Motivo** (vencida, cierra pronto, sin actividad, retrocedió). Ordená primero las vencidas y cerrá con el monto total en riesgo.
