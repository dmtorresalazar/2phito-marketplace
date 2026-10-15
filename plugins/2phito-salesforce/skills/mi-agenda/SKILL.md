---
name: mi-agenda
description: Agenda del usuario actual - tareas pendientes o vencidas y reuniones de hoy o de la semana. Usar cuando preguntan qué tengo hoy, mis pendientes, mi agenda o mis reuniones.
---

1. Obtené el Id del usuario actual con `getUserInfo`. Período por defecto: hoy para reuniones; respetá "esta semana", "mañana", etc.
2. Consultá con `soqlQuery`:
   - Tareas abiertas vencidas o de hoy: `SELECT Subject, Status, Priority, ActivityDate, Who.Name, What.Name FROM Task WHERE OwnerId = '<Id>' AND IsClosed = false AND (ActivityDate <= TODAY OR ActivityDate = null) ORDER BY ActivityDate LIMIT 50`
   - Reuniones: `SELECT Subject, StartDateTime, EndDateTime, Location, Who.Name, What.Name FROM Event WHERE OwnerId = '<Id>' AND StartDateTime = TODAY ORDER BY StartDateTime LIMIT 50` (o `THIS_WEEK`, `TOMORROW`).
3. Respondé con secciones: **Reuniones** (hora, asunto, con quién, lugar), **Tareas vencidas** (fecha, asunto, relacionado con, prioridad) y **Tareas de hoy**. Si una sección está vacía, decilo en una línea.
4. Esta agenda es solo del usuario actual. Si piden la de otra persona, consultá por su `OwnerId` solo si la nombran explícitamente; Salesforce aplica sus permisos.
