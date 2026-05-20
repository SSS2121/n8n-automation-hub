# Documentación de Flujos: n8n Automation Hub

Este documento detalla la lógica operativa de los flujos automatizados presentes en este repositorio.

## 1. Flujo: N8n-list of printers
**Propósito:** Automatización de la extracción de ventas y gestión de documentos para impresión.

### Lógica de ejecución:
1.  **Ingreso (Trigger):** Conexión vía API a **Siigo POS** mediante el endpoint `invoices`.
2.  **Parámetros:** Se aplica un filtro de `document_type: FV` (Factura de Venta) y un rango de fecha dinámico `created_start` que toma los últimos 4 días automáticamente.
3.  **Autenticación:** Utiliza un nodo de `Login` previo para inyectar el `access_token` en el header de la petición HTTP.
4.  **Procesamiento:** * Los datos obtenidos pasan por una fase de mapeo contra una base de datos local (`DB-Product`).
    * Se generan archivos base64 para documentos guardados en Google Drive (`Drive-Caja`).
    * Finalmente, el flujo comunica el resultado a un servicio externo llamado `PrintNote`.
5.  **Persistencia:** Todos los eventos exitosos se registran en la base de datos principal (`DB`) para auditoría.

---

## 2. Orquestación de Notificaciones (Estructura general)
Los flujos de comunicación masiva siguen este patrón de diseño:
* **Filtro de Datos:** Se obtienen los contactos de la BD.
* **Nodo de Decisión (If/Switch):** Evalúa si el contacto tiene WhatsApp configurado o si debe recibir el aviso por Gmail.
* **Nodo de Envio:** Ejecución de la API correspondiente.
* **Gestor de Errores:** Todos los nodos tienen habilitada la opción `retryOnFail` con espera de 500ms entre reintentos para asegurar la entrega.

---

## 🛠️ Notas para el despliegue
* Asegúrese de que las variables de entorno `SIIGO_API_URL` y `WHATSAPP_TOKEN` estén configuradas en su instancia de n8n.
* El flujo `list of printers` está diseñado para correr en modo *Scheduled* (por ejemplo, cada 24 horas).