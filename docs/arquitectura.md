# Documento de Arquitectura de Software

## 1. Vista General del Sistema
El sistema sigue una arquitectura de **N-Capas** (Client-Server) para separar las responsabilidades de interfaz de usuario, lógica de negocio y persistencia de datos.


## 2. Stack Tecnológico
- **Frontend:** React.js con **Tailwind CSS** (Interfaz responsiva y moderna).
- **Backend:** **Node.js** con el framework **Express**.
- **Base de Datos:** **MongoDB** (Persistencia NoSQL).
- **Infraestructura:** Contenedores **Docker** sobre una **Azure Virtual Machine**.
- **Seguridad:** JSON Web Tokens (JWT) y TLS/SSL.


El siguiente diagrama muestra cómo interactúan los componentes dentro de la **Azure VM** utilizando **Docker**.

graph TD
    subgraph Cliente
        A[Frontend: React + Tailwind CSS]
    end

    subgraph "Nube Azure (Docker Containers)"
        B[Backend: Node.js + Express]
        C{Middleware de Seguridad: ISO 27001}
        D[(Base de Datos: MongoDB)]
    end

    subgraph "Servicios Externos"
        E[API Mercado Pago]
    end

    A -->|Peticiones HTTPS/JWT| B
    B --> C
    C -->|Consulta Validada| D
    B -->|Procesar Pago| E



## 3. Diagrama de la Base de Datos (Modelo de Datos)
Para el e-commerce de electrodomésticos, utilizaremos un modelo de documentos en MongoDB.

El sistema sigue una estructura lógica para asegurar la integridad de la información conforme a la ISO 27001.

erDiagram
    USUARIO ||--o{ ORDEN : "genera"
    USUARIO {
        string id PK
        string email UK
        string password_hash
        string role "admin | cliente"
    }
    PRODUCTO ||--o{ ORDEN_ITEM : "incluido en"
    PRODUCTO {
        string id PK
        string nombre
        float precio
        int stock
        string categoria
    }
    ORDEN ||--|{ ORDEN_ITEM : "contiene"
    ORDEN {
        string id PK
        string status "pendiente | pagado"
        float total
        string mercadoPagoId
    }




### Colecciones Principales:
- **Users:** Almacena perfiles, direcciones y roles (RBAC).
- **Products:** Detalle de electrodomésticos (marca, modelo, frigorías/watts, stock).
- **Orders:** Transacciones vinculadas al ID de Mercado Pago.



## 4. Diseño del Backend (Patrón MVC)
La lógica del servidor se organiza bajo el patrón **Modelo-Vista-Controlador** para facilitar el mantenimiento y las auditorías de seguridad:
- **Routes:** Define los puntos de acceso (endpoints).
- **Controllers:** Contiene la lógica de negocio y validaciones.
- **Models:** Define la estructura de los datos con Mongoose.
- **Middlewares:** Implementa los controles de la **ISO 27001** (Autenticación y manejo de errores).

## 5. Flujo de Datos Seguro
1. El usuario solicita acceso mediante el frontend.
2. La solicitud viaja cifrada via **HTTPS**.
3. El **Middleware de Autenticación** verifica el JWT.
4. El **Controller** valida los datos de entrada (Anti-Inyección NoSQL).
5. Se realiza la consulta a **MongoDB**.
6. La respuesta se devuelve en formato JSON.



## 6. Infraestructura y Despliegue (DevOps)
El despliegue se automatiza mediante Docker para garantizar la disponibilidad (**Control A.17 de ISO 27001**).



- **Container 1:** Web App (Node.js + Express).
- **Container 2:** Base de Datos (MongoDB).
- **Proxy Inverso:** Nginx para manejo de certificados SSL y balanceo de carga básico.

*Última actualización: 8 de Febrero de 2026*