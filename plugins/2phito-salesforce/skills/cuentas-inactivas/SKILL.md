---
name: cuentas-inactivas
description: Lista cuentas sin actividad reciente y sin oportunidades abiertas. Usar cuando preguntan qué clientes no se contactaron, cuentas abandonadas, dormidas o a reactivar.
---

1. Período por defecto: 90 días. Respetá el que indique el usuario. Si dicen "mis", agregá `OwnerId` del usuario actual (`getUserInfo`).
2. Consultá con `soqlQuery`:
   `SELECT Name, Industry, Type, Owner.Name, LastActivityDate FROM Account WHERE (LastActivityDate < LAST_N_DAYS:90 OR LastActivityDate = null) AND Id NOT IN (SELECT AccountId FROM Opportunity WHERE IsClosed = false) ORDER BY LastActivityDate NULLS FIRST LIMIT 50`
3. Si el usuario quiere incluir cuentas con oportunidades abiertas, quitá la condición `Id NOT IN (...)`.
4. Mostrá una tabla (cuenta, rubro, tipo, responsable, última actividad; "nunca" si está vacía) y la cantidad total. Si hay más de 50, decilo y sugerí filtrar por responsable, rubro o tipo.
