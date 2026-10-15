---
name: explorar-objeto
description: Describe un objeto de Salesforce (campos, tipos y valores de listas) antes de consultarlo. Usar cuando preguntan qué datos tiene un objeto, qué campos existen o qué valores puede tomar un campo, y antes de consultar objetos o campos propios (terminados en __c) o un campo que no conocés.
---

1. Identificá el objeto. Si el usuario usa un nombre de negocio ("oportunidad", "caso", "proyecto"), buscá el nombre de API: los estándar son en inglés (Opportunity, Case) y los propios terminan en `__c`. Si no estás seguro, usá `find` o preguntá.
2. Usá `getObjectSchema` del objeto. Nunca inventes nombres de campos: si un campo no aparece en el esquema, no existe o el usuario no tiene acceso.
3. Si piden la lista de campos, mostrá una tabla (etiqueta, nombre de API, tipo) con los más relevantes primero (nombre, estado/etapa, montos, fechas, responsable, relaciones). Para listas de selección, mostrá sus valores.
4. Si el esquema se pidió para armar una consulta, usalo para escribir el `soqlQuery` correcto y respondé la pregunta original; no muestres el esquema salvo que lo pidan.
