# Hotel Booking 
***
### INTRODUCCIÓN
  El presente proyecto tiene como objetivo documentar el proceso de normalización de un dataset, cuya contenido se relaciona con las reservas de un hotel, transformando dicha información en una base de datos relacional estructurada.
  El trabajo incluye el análisis del dataset original, el diseño de tablas normalizadas, la definición de relaciones entre entidades y la implementación de sentencias SQL para la creación y administración de la base de datos.

 > #### Dataset: ***Hotel Booking*** - *Mojtaba*
  ```bash
https://www.kaggle.com/datasets/mojtaba142/hotel-booking
```
***
### CONTENIDO
El repositorio contiene:
- **Base de datos normalizada:** Estructura relacional para la normalización, con sus respectivas tablas, relaciones e índices.
- **Dataset original:** Contiene los datos de origen utilizados para desarrollar este proyecto.
- **Documento institucional:** Documentación del trabajo que incluye los diagramas, las sentencias de creación de tablas, las inserciones de datos, los índices y las explicaciones que corresponden al funcionamiento de la base de datos.
- **Diagrama Entidad-relación**: Diagrama que muestra todas las tablas creadas con sus atributos, tipos de dato, multiplicidades y llaves primarias y secundarias.
***
### REQUISITOS
Para ejecutar el proyecto, se requiere:
 - Un sistema gestor de bases de datos compatible con la sintaxis SQL utilizada, como MySQL o MariaDB.
 - Una herramienta para administrar y ejecutar consultas SQL, como HeidiSQL, MySQL Workbench o phpMyAdmin.
 - Los archivos presentados dentro de este repositorio.
***
### INSTRUCCIONES PARA IMPORTAR EL PROYECTO
   **Paso 1:**  Descargar o clonar el repositorio en el equipo y verificar que se encuentren los archivos necesarios.                         
**Paso 2:**  Iniciar el servicio de MySQL o MariaDB y comprobar que funcione correctamente.                                                     
**Paso 3:**  Ingresar a la herramienta de preferencia y establecer una conexión con el servidor.                                                
**Paso 4:**  Abrir el archivo SQL que contiene la estructura de la base de datos normalizada y ejecutar las sentencias en el orden establecido.                     
**Paso 5:**  Importar los datos incluidos en los scripts SQL, ejecutarlas después de crear las tablas y sus relaciones.                         
**Paso 6:**   Comprobar que las tablas se hayan creado correctamente, que las relaciones y los índices estén definidos y que los datos se hayan cargado de manera adecuada.
***
### Tablas creadas


| NOMBRE     | FUNCIÓN     |
|------ |------ |
|Hotel      | Contiene los hoteles disponibles y permite identificar en que hotel se realiza cada reserva. |
| Cliente | Guarda los datos personales y de contacto de cada cliente, como nombre, apellido, teléfono, e-mail y país. |
| Pais | Almacena los países asociados a lo clientes, evitando repetir la descripción del país en cada registro. |
| Comida | Contiene los diferentes tipos de comida disponible y permite asociarlos a cada alojamiento. |
| Segmento_mercado | Almacena los diferentes segmentos de mercado a los que pertenecen las reservas. |
| Canal_distribucion | Identifica el canal mediante el cual se realizó cada reserva. |
| Tipo_habitacion | Almacena los distintos tipos de habitación. Se utiliza tanto para indicar la habitación reservada como la habitación finalmente asignada.|
| Tipo_cliente | Clasifica a los clientes según el tipo correspondiente. |
| Tipo_deposito | Contiene los diferentes tipos de depósito utilizados y permite indicar cual corresponde a cada alojamiento. |
| Estado_reserva | Contiene los diferentes estados que puede tener una reserva, permitiendo identificar la situación de cada una. |
| Reserva | Registra y guarda todos los datos relacionados a la contratación de habitaciones del hotel, tales como: fechas de reserva, cantidad de huéspedes, precios promedio, estacionamiento, etc. |

***
***Trabajo práctico final: Base de datos libre***                                                                      
*Martinez Lucia, Quiroz Ornella*                                                                                
*3° - Base de Datos II – Gestión de Proyectos de Software*                                                           
*Ariel Nardelli, Matias Nardelli*                                                                           
15 de octubre, 2026                                                          

