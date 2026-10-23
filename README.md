
# CASSA | Agente Comercial Inmobiliario

**Checkpoint 1 — IA Automation Avanzada | Coderhouse**

**Desarrollado por:** Julieta Canzio Otero

## Descripción del proyecto

Este proyecto consiste en un agente de inteligencia artificial desarrollado en n8n para automatizar la recepción, calificación y registro de consultas comerciales inmobiliarias.

El agente atiende consultas relacionadas con la compra y el alquiler de propiedades, recopila información relevante de los interesados y registra los datos en Airtable para facilitar su posterior seguimiento comercial.

Además, incorpora memoria conversacional, límites de ejecución y notificaciones automáticas por correo electrónico.

## Objetivos

- Automatizar la atención inicial de consultas inmobiliarias.
- Identificar los datos necesarios para calificar a un potencial cliente.
- Registrar consultas comerciales en una base estructurada.
- Mantener el contexto de la conversación.
- Notificar las ejecuciones del agente para permitir su supervisión.

## Arquitectura del workflow

**01 — Recepción de consultas:** Chat Trigger que recibe los mensajes del usuario.

**02 — Agente Comercial CASSA:** AI Agent que interpreta las consultas, solicita información faltante y decide cuándo utilizar la herramienta de registro.

**03 — Modelo IA Groq:** modelo GPT-OSS 20B utilizado para procesar las conversaciones.

**04 — Memoria conversacional:** Simple Memory con ventana de contexto de 4 interacciones.

**05 — Registrar Lead:** herramienta de Airtable conectada lateralmente al AI Agent para crear registros comerciales.

**06 — Notificación comercial:** Gmail conectado a la salida principal del agente para enviar un reporte automático de ejecución.

## Datos registrados en Airtable

La herramienta registra los siguientes campos:

- Nombre del cliente.
- Contacto.
- Canal de ingreso.
- Operación: Venta o Alquiler.
- Tipo de propiedad.
- Zona de interés.
- Presupuesto.
- Resumen de la consulta.

La fecha de creación se genera automáticamente en Airtable.

## Reglas del agente

El agente cuenta con un System Message estructurado que establece su rol, ámbito de actuación, objetivos, uso de herramientas, restricciones y criterios de escalamiento.

Solo debe registrar una consulta cuando dispone del nombre, un medio de contacto, el tipo de operación y al menos un criterio de búsqueda.

Para normalizar los registros, utiliza exclusivamente los valores `Venta` y `Alquiler`.

La cantidad máxima de iteraciones está configurada en **6**.

## Observabilidad

El workflow incorpora un nodo Gmail que envía una notificación al finalizar correctamente la ejecución del agente.

El correo contiene la fecha, la respuesta generada y el canal de origen. Este mecanismo permite supervisar el resultado de la ejecución, aunque no constituye un registro técnico completo de todas las operaciones internas.

## Prueba funcional

Se realizó una prueba con un cliente ficticio interesado en alquilar un departamento de dos dormitorios en el centro de Bahía Blanca.

**Resultados verificados:**

- El Chat Trigger recibió la consulta.
- El AI Agent procesó la información.
- La herramienta Airtable creó el registro.
- El campo Operación se almacenó correctamente como `Alquiler`.
- El nodo Gmail envió la notificación automática.

La ejecución finalizó correctamente.

## Tecnologías utilizadas

- n8n
- Groq — GPT-OSS 20B
- Airtable
- Gmail
- Simple Memory

## Archivo entregable

`checkpoint1_julieta_canzio.json`

El archivo contiene la configuración exportada del workflow de n8n. Para utilizarlo en otra instancia, es necesario importar el JSON y configurar las credenciales y los recursos externos correspondientes.

---

**Autora:** Julieta Canzio Otero

**Curso:** IA Automation Avanzada — Coderhouse

**Fecha:** Octubre de 2026
