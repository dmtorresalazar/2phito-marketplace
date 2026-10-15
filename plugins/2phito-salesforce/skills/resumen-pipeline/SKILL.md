---
name: resumen-pipeline
description: Resumen del pipeline de oportunidades abiertas por etapa, propietario o período. Usar cuando el usuario pregunta por pipeline, forecast, totales por etapa o cuánto hay en juego.
---

1. Definí el período: si el usuario no lo indica, usá el trimestre actual (`CloseDate = THIS_QUARTER`).
2. Calculá los totales en Salesforce, nunca sumando a mano:
   - Por etapa: `SELECT StageName, COUNT(Id) cantidad, SUM(Amount) monto FROM Opportunity WHERE IsClosed = false AND <período> GROUP BY StageName`
   - Por propietario (si lo pide): `GROUP BY Owner.Name`.
3. Mostrá una tabla con Etapa, Cantidad y Monto, y una fila final con el **total general**.
4. Agregá 1–2 observaciones breves (por ejemplo, la etapa con más monto o las oportunidades sin monto cargado). No inventes tendencias que los datos no muestren.
