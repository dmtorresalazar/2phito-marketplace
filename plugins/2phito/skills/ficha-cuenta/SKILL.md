---
name: ficha-cuenta
description: Arma la ficha completa de una cuenta de Salesforce (datos, contactos, oportunidades abiertas y actividad reciente). Usar cuando el usuario pide "ficha", "resumen" o "todo sobre" una cuenta o cliente.
---

1. Encontrá la cuenta con `find` por nombre. Si hay varias coincidencias, mostrá las opciones y pedí que elija.
2. Con el Id de la cuenta:
   - Datos: `soqlQuery` sobre Account con Name, Industry, Type, BillingCity, BillingCountry, Phone, Website, Owner.Name.
   - Contactos: `getRelatedRecords` (Contacts), hasta 10, con nombre, cargo, email y teléfono.
   - Oportunidades abiertas: `soqlQuery` sobre Opportunity con `AccountId = <Id> AND IsClosed = false`, con Name, StageName, Amount, CloseDate y Owner.Name, ordenado por CloseDate.
   - Actividad: últimas 5 Task y 5 Event de la cuenta, ordenadas por fecha.
3. Respondé con secciones: **Datos**, **Contactos**, **Oportunidades abiertas** (con total del monto), **Actividad reciente**. Si una sección está vacía, decilo en una línea.
