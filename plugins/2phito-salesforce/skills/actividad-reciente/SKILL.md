---
name: actividad-reciente
description: Lista tareas y eventos recientes de una cuenta, contacto, oportunidad o del propio usuario. Usar cuando preguntan qué pasó, qué actividad hubo o qué está pendiente.
---

1. Período por defecto: últimos 7 días. Respetá el período que indique el usuario.
2. Si mencionan una cuenta, contacto u oportunidad, buscala con `find` y filtrá por `WhatId` o `WhoId`. Si dicen "mis", filtrá por `OwnerId` del usuario actual (`getUserInfo`).
3. Consultá con `soqlQuery`:
   - Task: Subject, Status, ActivityDate, Who.Name, What.Name, Owner.Name.
   - Event: Subject, StartDateTime, Who.Name, What.Name, Owner.Name.
   - Ordená por fecha descendente, `LIMIT 50`.
4. Mostrá una tabla única ordenada por fecha (tipo, fecha, asunto, relacionado con, responsable) y, aparte, las **tareas pendientes vencidas**.
