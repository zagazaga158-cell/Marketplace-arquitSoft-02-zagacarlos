
# Arquitectura inicial del sistema

## Diagrama de arquitectura

```mermaid
flowchart TD

    %% ACTORES
    subgraph ACTORES["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    %% PRESENTACIÓN
    subgraph PRESENTACION["PRESENTACIÓN"]
        Web["Aplicación Web"]
        API["API REST"]
    end

    %% LÓGICA DE NEGOCIO
    subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
        Integraciones["Integraciones externas"]
    end

    %% DATOS
    subgraph DATOS["DATOS"]
        BD["Base de datos"]
    end

    %% SISTEMAS EXTERNOS
    subgraph EXTERNOS["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        Envio["Servicio de envío"]
    end

    %% FLUJO PRINCIPAL
    Cliente --> Web
    Seller --> Web
    Admin --> Web

    Web --> API
    API --> Usuarios
    API --> Sellers
    API --> Catalogo
    API --> Carrito
    API --> Pedidos

    %% ACCESO A DATOS
    Usuarios --> BD
    Sellers --> BD
    Catalogo --> BD
    Carrito --> BD
    Pedidos --> BD

    %% INTEGRACIONES
    Pedidos --> Integraciones
    Integraciones --> Pago
    Integraciones --> Envio

    %% ESTILOS
    style ACTORES fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style PRESENTACION fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style NEGOCIO fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style DATOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff
    style EXTERNOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff
```

## Descripción

La arquitectura inicial se organiza en tres capas principales:

- **Presentación:** permite la interacción de los usuarios mediante la aplicación web y la API REST.
- **Lógica de negocio:** contiene los módulos de usuarios, sellers, catálogo, carrito y pedidos, responsables de procesar las funcionalidades del marketplace.
- **Datos:** permite almacenar y consultar la información del sistema mediante una base de datos.

Además, el módulo de **Pedidos** se comunica con un módulo de **Integraciones externas**, que permite conectar el sistema con la pasarela de pago y el servicio de envío.

Esta organización facilita la separación de responsabilidades y permite considerar los atributos de calidad de rendimiento, escalabilidad, seguridad y mantenibilidad.