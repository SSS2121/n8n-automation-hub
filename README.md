# n8n Automation Hub 🚀

Este repositorio contiene una colección de flujos de trabajo (*workflows*) diseñados en n8n para automatizar tareas repetitivas, gestionar datos y centralizar comunicaciones.

## Funcionalidades principales
- **ETL de Datos:** Extracción desde APIs externas, transformación y carga en bases de datos (SQL/NoSQL).
- **Orquestación de Notificaciones:** Sistema de envíos automáticos para comunicación masiva mediante Gmail (SMTP/API) y WhatsApp (Cloud API/Business).
- **Sincronización:** Automatización de tareas programadas (cron jobs) para mantener la integridad de los datos en tiempo real.

## Uso del Repositorio
Cada archivo `.json` es un flujo independiente. Para implementarlos:
1. Abre tu instancia de n8n.
2. Crea un nuevo flujo.
3. Importa el archivo `.json` desde tu ordenador.
4. Configura tus credenciales (API Keys, tokens de WhatsApp y credenciales de BD).

## Advertencia de seguridad
Este repositorio no incluye credenciales ni datos sensibles. Se recomienda el uso de variables de entorno para manejar las claves de acceso de las APIs conectadas.
