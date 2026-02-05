# Documento de Planificación del Proyecto: E-commerce Electrodomésticos

## 1. Visión General
Este proyecto consiste en el desarrollo de una plataforma web de E-commerce especializada en electrodomésticos, construida con un enfoque en el **Ciclo de Vida de Desarrollo de Software (SDLC)** y el cumplimiento de estándares de seguridad basados en la **ISO 27001**.

## 2. Metodología de Trabajo (SDLC)
Se utilizará la metodología **Ágil (Kanban)** para gestionar el flujo de trabajo de forma visual y continua:
- **Herramienta de Gestión:** Monday.com.
- **Flujo Kanban:** Se implementarán tableros con estados: `Backlog`, `En Diseño`, `En Desarrollo (Seguro)`, `QA/Testing` y `Desplegado`.
- **Trazabilidad (ISO 27001):** Cada tarea en Monday contará con un responsable y descripción detallada para mantener el registro de cambios y la integridad del proceso de desarrollo.
- **Control de Versiones:** GitFlow integrado mediante disparadores de estado.

## 3. Requerimientos del Producto (MVP)

### Requerimientos Funcionales (RF)
| ID | Requerimiento | Descripción |
|:---|:---|:---|
| RF-01 | Gestión de Usuarios | Registro, inicio de sesión y perfiles de cliente. |
| RF-02 | Catálogo de Productos | Visualización dinámica por categorías (Refrigeración, Lavado, Cocina). |
| RF-03 | Carrito de Compras | Gestión de artículos (añadir, editar cantidad, eliminar). |
| RF-04 | Pasarela de Pagos | Integración con la API de Mercado Pago para transacciones. |
| RF-05 | Panel de Administración | CRUD (Crear, Leer, Actualizar, Borrar) de inventario para el administrador. |

### Requerimientos No Funcionales e ISO 27001 (RNF)
| ID | Tipo | Estándar / Control |
|:---|:---|:---|
| RNF-01 | Seguridad | Cifrado de contraseñas con `bcrypt` (ISO 27001: Control de Cifrado). |
| RNF-02 | Autenticación | Uso de JWT para manejo de sesiones seguras. |
| RNF-03 | Disponibilidad | Despliegue en Azure VM mediante contenedores Docker. |
| RNF-04 | Integridad | Validación de esquemas de datos con `Joi/Zod` para evitar Inyecciones NoSQL. |

## 4. Historias de Usuario (Backlog Inicial)
1. **Como cliente**, quiero crear una cuenta para guardar mis direcciones y métodos de pago.
2. **Como cliente**, quiero filtrar productos por rango de precio para ajustarme a mi presupuesto.
3. **Como administrador**, quiero recibir notificaciones de stock bajo para gestionar el inventario.
4. **Como sistema**, quiero cerrar sesiones inactivas automáticamente para proteger la información del usuario (ISO 27001).

## 5. Análisis de Riesgos Inicial (ISO 27001)
* **Riesgo:** Acceso no autorizado a bases de datos.
    * *Mitigación:* Implementar Políticas de Control de Acceso y limitar conexiones a la DB solo desde la IP de la App.
* **Riesgo:** Pérdida de disponibilidad del servicio.
    * *Mitigación:* Configurar monitoreo con **Zabbix** y realizar backups periódicos.

---
*Última actualización: 4 de Febrero de 2026*