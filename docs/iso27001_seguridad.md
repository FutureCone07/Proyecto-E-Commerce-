# Documento de Seguridad de la Información (Basado en ISO 27001)

## 1. Introducción
Este documento detalla los controles de seguridad implementados en el E-commerce de Electrodomésticos, siguiendo los estándares de la norma **ISO 27001**. El objetivo es garantizar la **Confidencialidad, Integridad y Disponibilidad (CID)** de los activos de información.

## 2. Inventario de Activos de Información
Identificamos los activos críticos del sistema para aplicar controles específicos:

| Activo | Descripción | Clasificación |
|:---|:---|:---|
| **Datos de Usuario** | Nombres, correos y direcciones de envío. | Confidencial |
| **Credenciales** | Contraseñas de acceso al sistema. | Crítico |
| **Datos de Pago** | Tokens de transacción (Mercado Pago). | Crítico |
| **Inventario** | Precios y stock de electrodomésticos. | Integridad Alta |

## 3. Análisis de Riesgos y Mitigación
Basado en el Control **A.12.6** (Gestión de vulnerabilidades técnicas):

| Amenaza | Impacto | Control de Mitigación |
|:---|:---|:---|
| **Inyección NoSQL** | Robo o borrado de base de datos. | Validación estricta de esquemas con `Joi/Zod`. |
| **Ataque de Fuerza Bruta** | Acceso no autorizado a cuentas. | Implementación de `express-rate-limit` y bloqueo de IP. |
| **Exposición de Secretos** | Robo de API Keys en GitHub. | Uso de variables de entorno `.env` (incluido en `.gitignore`). |

## 4. Controles de Seguridad Implementados

### A.9 Control de Acceso
- **Autenticación:** Implementación de **JWT (JSON Web Tokens)** con tiempo de expiración de 2 horas.
- **Autorización (RBAC):** Diferenciación de roles mediante middleware en Node.js para restringir rutas de `/admin`.

### A.10 Criptografía
- **Hashing:** Las contraseñas se almacenan utilizando el algoritmo **bcrypt** con un factor de costo (salt) de 10.
- **Tránsito:** Se requiere el uso de **TLS/SSL (HTTPS)** para toda la comunicación entre el frontend (Tailwind) y el backend (Node.js).

### A.14 Adquisición, Desarrollo y Mantenimiento de Sistemas
- **Entorno de Pruebas:** Uso de **Docker** para asegurar que el entorno de desarrollo sea idéntico al de producción.
- **Gestión de Dependencias:** Ejecución periódica de `npm audit` para identificar y corregir librerías vulnerables.

## 5. Monitoreo y Disponibilidad (A.17)
- **Monitoreo:** Uso de **Zabbix** para supervisar el estado de la **Azure VM** y la disponibilidad del servicio de base de datos.
- **Recuperación:** Estrategia de despliegue con contenedores para permitir una recuperación rápida ante fallos del sistema.

---
*Este documento es parte del cumplimiento del ciclo de vida de desarrollo seguro (S-SDLC).*