---
name: ganadas-perdidas
description: Resultado de oportunidades cerradas (ganadas y perdidas) en un período, con montos, tasa de éxito y motivos de pérdida. Usar cuando preguntan cuánto se ganó o perdió, la tasa de cierre o por qué se pierden negocios.
---

1. Período por defecto: mes actual (`CloseDate = THIS_MONTH`). Respetá el que indique el usuario (`THIS_QUARTER`, `LAST_MONTH`, `THIS_YEAR`, fechas).
2. Totales con `soqlQuery`, nunca sumando a mano:
   `SELECT IsWon, COUNT(Id) cantidad, SUM(Amount) monto FROM Opportunity WHERE IsClosed = true AND <período> GROUP BY IsWon`
   Si lo piden por vendedor, agregá `Owner.Name` al `GROUP BY`.
3. Tasa de éxito = ganadas / cerradas (por cantidad y por monto).
4. Motivo de pérdida: Salesforce no tiene un campo estándar. Revisá con `getObjectSchema` de Opportunity si existe uno propio (por ejemplo `Loss_Reason__c` o `Motivo_Perdida__c`) y agrupá las perdidas por ese campo. Si no existe, decilo en una línea; no lo inventes.
5. Mostrá una tabla (resultado, cantidad, monto), la tasa de éxito y, si se pide, las 10 ganadas o perdidas de mayor monto (oportunidad, cuenta, monto, fecha de cierre, responsable).
