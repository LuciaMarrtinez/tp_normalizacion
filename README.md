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

### TECNOLOGIAS
-MySQL: creación y gestión de la base de datos.

-SQL: definición de tablas, carga de datos, consultas y vistas.

-Dataset Hotel Booking: fuente de datos utilizada para el proceso de normalización.


### REQUISITOS
Para ejecutar el proyecto, se requiere:
 - Un sistema gestor de bases de datos compatible con la sintaxis SQL utilizada, como MySQL o MariaDB.
 - Una herramienta para administrar y ejecutar consultas SQL, como HeidiSQL, MySQL Workbench o phpMyAdmin.
 - Los archivos presentados dentro de este repositorio.
***

### PROCESO
**Primera Forma Normal (1FN)**: organización de los datos en valores atómicos.

**Segunda Forma Normal (2FN)**: análisis de las dependencias funcionales respecto de las claves primarias.

**Tercera Forma Normal** (3FN): separación de los datos para evitar dependencias transitivas entre atributos que no son clave.

### DIAGRAMA ENTIDAD RELACION 
<img width="2662" height="914" alt="Hotel Booking Diagrama (2)" src="https://github.com/user-attachments/assets/07cb0a5a-9027-4d9a-b1c6-c84573b4dd5b" />





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
 
 ### PROCESO DE RECREACIÓN
 
 1_ Descagar el csv de este link 
    https://www.kaggle.com/datasets/mojtaba142/hotel-booking
    
 2_ Abrir, en este caso, HeidiSQL y conectarse al servidor de base de datos.
 
 3_Crear la base de datos 
```sql
CREATE DATABASE reserva_hotel;
USE reserva_hotel;
```
 4_ Copiar y pegar las siguiente sentencias: 
 ### Hotel

```sql
CREATE TABLE hotel (
    cod_hotel TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(20) NOT NULL
);
```

### País

```sql
CREATE TABLE pais (
    cod_pais SMALLINT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```

### Tipo de cliente

```sql
CREATE TABLE tipo_cliente (
    cod_tipocliente TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```

### Comida

```sql
CREATE TABLE comida (
    cod_comida TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(10) NOT NULL
);
```

### Segmento de mercado

```sql
CREATE TABLE segmento_mercado (
    cod_segme TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```

### Canal de distribución

```sql
CREATE TABLE canal_distribucion (
    cod_canal TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```

### Tipo de depósito

```sql
CREATE TABLE tipo_deposito (
    cod_deposito TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```

### Tipo de habitación

```sql
CREATE TABLE tipo_habitacion (
    cod_habitacion TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```

### Estado de reserva

```sql
CREATE TABLE estado_reserva (
    cod_estado TINYINT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    descrip VARCHAR(20) NOT NULL
);
```
### Cliente

```sql
CREATE TABLE cliente (
    cod_cliente INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(20) NOT NULL,
    apellido VARCHAR(20) NOT NULL,
    num_tel VARCHAR(20) NOT NULL,
    email VARCHAR(50) NOT NULL,
    tar_cred VARCHAR(20) NOT NULL,
    c_pais SMALLINT NOT NULL,
    FOREIGN KEY (c_pais) REFERENCES pais(cod_pais)
);
```

Se agrega una restricción `UNIQUE` al teléfono:

```sql
ALTER TABLE cliente
ADD CONSTRAINT tele_cliente UNIQUE (num_tel);
```


## 3. Insertar datos en las tablas de referencia

Las sentencias `SELECT DISTINCT` recuperan valores únicos del dataset original.

### Hotel

```sql
INSERT INTO hotel (nombre)
SELECT DISTINCT hotel
FROM hotel_booking_original;
```

### País

```sql
INSERT INTO pais (descrip)
SELECT DISTINCT country
FROM hotel_booking_original;
```

### Tipo de cliente

```sql
INSERT INTO tipo_cliente (descrip)
SELECT DISTINCT customer_type
FROM hotel_booking_original;
```

### Comida

```sql
INSERT INTO comida (descrip)
SELECT DISTINCT meal
FROM hotel_booking_original;
```

### Segmento de mercado

```sql
INSERT INTO segmento_mercado (descrip)
SELECT DISTINCT market_segment
FROM hotel_booking_original;
```

### Canal de distribución

```sql
INSERT INTO canal_distribucion (descrip)
SELECT DISTINCT distribution_channel
FROM hotel_booking_original;
```

### Tipo de depósito

```sql
INSERT INTO tipo_deposito (descrip)
SELECT DISTINCT deposit_type
FROM hotel_booking_original;
```

### Tipo de habitación

Se reúnen los tipos de habitación reservada y asignada en una misma tabla.

```sql
INSERT INTO tipo_habitacion (descrip)
SELECT DISTINCT reserved_room_type
FROM hotel_booking_original
UNION
SELECT DISTINCT assigned_room_type
FROM hotel_booking_original;
```

### Estado de reserva

```sql
INSERT INTO estado_reserva (descrip)
SELECT DISTINCT reservation_status
FROM hotel_booking_original;
````
 ### Insertar clientes

```sql
INSERT INTO cliente (nombre, apellido, num_tel, email, tar_cred, c_pais)
SELECT DISTINCT
    SUBSTRING_INDEX(`name`, ' ', 1),
    SUBSTRING_INDEX(`name`, ' ', -1),
    phone_number,
    email,
    credit_card,
    cod_pais
FROM hotel_booking_original
JOIN pais
    ON pais.descrip = hotel_booking_original.country;
```

## CREAR INDICES ALTERNATIVOS

Los índices se crean sobre columnas descriptivas utilizadas en búsquedas y relaciones con el dataset original.

```sql
CREATE INDEX nombre_hotel
ON hotel(nombre);

CREATE INDEX descrip_comida
ON comida(descrip);

CREATE INDEX descrip_segmento
ON segmento_mercado(descrip);

CREATE INDEX descrip_canal
ON canal_distribucion(descrip);

CREATE INDEX descrip_habitacion
ON tipo_habitacion(descrip);

CREATE INDEX descrip_estado
ON estado_reserva(descrip);

CREATE INDEX descrip_cliente
ON tipo_cliente(descrip);

CREATE INDEX descrip_deposito
ON tipo_deposito(descrip);
```

## 6. CREAR TABLA RESERVA

### Crear tabla

```sql
CREATE TABLE reserva (
    cod_reserva INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    cancelado BOOLEAN NOT NULL,
    dias_anticipacion SMALLINT NOT NULL,
    anio_llegada SMALLINT NOT NULL,
    mes_llegada VARCHAR(20) NOT NULL,
    semana_llegada TINYINT NOT NULL,
    dia_llegada TINYINT NOT NULL,
    noche_finde SMALLINT NOT NULL,
    noche_semana SMALLINT NOT NULL,
    adultos TINYINT NOT NULL,
    ninios INT NOT NULL,
    bebes TINYINT NOT NULL,
    huesped_repetido BOOLEAN NOT NULL,
    cancel_anteriores TINYINT NOT NULL,
    no_cancel_reserva TINYINT NOT NULL,
    cambio_reserva TINYINT NOT NULL,
    agente VARCHAR(10),
    compania VARCHAR(10),
    dias_lista_espera SMALLINT NOT NULL,
    adr DECIMAL(6,2) NOT NULL,
    estacionamiento SMALLINT NOT NULL,
    requisitos_esp TINYINT NOT NULL,
    fecha_estado_reserva DATE NOT NULL,
    rsv_cliente INT NOT NULL,
    FOREIGN KEY (rsv_cliente) REFERENCES cliente(cod_cliente),
    rsv_hotel TINYINT NOT NULL,
    FOREIGN KEY (rsv_hotel) REFERENCES hotel(cod_hotel),
    rsv_comida TINYINT NOT NULL,
    FOREIGN KEY (rsv_comida) REFERENCES comida(cod_comida),
    rsv_segme TINYINT NOT NULL,
    FOREIGN KEY (rsv_segme) REFERENCES segmento_mercado(cod_segme),
    rsv_canal TINYINT NOT NULL,
    FOREIGN KEY (rsv_canal) REFERENCES canal_distribucion(cod_canal),
    rsv_hab_r TINYINT NOT NULL,
    FOREIGN KEY (rsv_hab_r) REFERENCES tipo_habitacion(cod_habitacion),
    rsv_hab_a TINYINT NOT NULL,
    FOREIGN KEY (rsv_hab_a) REFERENCES tipo_habitacion(cod_habitacion),
    rsv_estado TINYINT NOT NULL,
    FOREIGN KEY (rsv_estado) REFERENCES estado_reserva(cod_estado),
    rsv_tipocliente TINYINT NOT NULL,
    FOREIGN KEY (rsv_tipocliente) REFERENCES tipo_cliente(cod_tipocliente),
    rsv_deposito TINYINT NOT NULL,
    FOREIGN KEY (rsv_deposito) REFERENCES tipo_deposito(cod_deposito)
);
```

### Insertar reservas

```sql
INSERT INTO reserva (
    cancelado, dias_anticipacion, anio_llegada, mes_llegada,
    semana_llegada, dia_llegada, noche_finde, noche_semana,
    adultos, ninios, bebes, huesped_repetido, cancel_anteriores,
    no_cancel_reserva, cambio_reserva, agente, compania,
    dias_lista_espera, adr, estacionamiento, requisitos_esp,
    fecha_estado_reserva, rsv_cliente, rsv_hotel, rsv_comida,
    rsv_segme, rsv_canal, rsv_hab_r, rsv_hab_a, rsv_estado,
    rsv_tipocliente, rsv_deposito
)
SELECT
    is_canceled, lead_time, arrival_date_year, arrival_date_month,
    arrival_date_week_number, arrival_date_day_of_month,
    stays_in_weekend_nights, stays_in_week_nights, adults, children,
    babies, is_repeated_guest, previous_cancellations,
    previous_bookings_not_canceled, booking_changes, agent, company,
    days_in_waiting_list, adr, required_car_parking_spaces,
    total_of_special_requests, reservation_status_date,
    c.cod_cliente, h.cod_hotel, cm.cod_comida, sm.cod_segme,
    cd.cod_canal, thr.cod_habitacion, tha.cod_habitacion,
    er.cod_estado, tc.cod_tipocliente, td.cod_deposito
FROM hotel_booking_original hbo
JOIN cliente c
    ON c.num_tel = hbo.phone_number
JOIN hotel h
    ON h.nombre = hbo.hotel
JOIN comida cm
    ON cm.descrip = hbo.meal
JOIN segmento_mercado sm
    ON sm.descrip = hbo.market_segment
JOIN canal_distribucion cd
    ON cd.descrip = hbo.distribution_channel
JOIN tipo_habitacion thr
    ON thr.descrip = hbo.reserved_room_type
JOIN tipo_habitacion tha
    ON tha.descrip = hbo.assigned_room_type
JOIN estado_reserva er
    ON er.descrip = hbo.reservation_status
JOIN tipo_cliente tc
    ON tc.descrip = hbo.customer_type
JOIN tipo_deposito td
    ON td.descrip = hbo.deposit_type;
```

### INSTRUCCIONES PARA IMPORTAR EL PROYECTO
   **Paso 1:**  Descargar o clonar el repositorio en el equipo y verificar que se encuentren los archivos necesarios.                         
**Paso 2:**  Iniciar el servicio de MySQL o MariaDB y comprobar que funcione correctamente.                                                     
**Paso 3:**  Ingresar a la herramienta de preferencia y establecer una conexión con el servidor.                                                
**Paso 4:**  Abrir el archivo SQL que contiene la estructura de la base de datos normalizada y ejecutar las sentencias en el orden establecido.                     
**Paso 5:**  Importar los datos incluidos en los scripts SQL, ejecutarlas después de crear las tablas y sus relaciones.                         
**Paso 6:**   Comprobar que las tablas se hayan creado correctamente, que las relaciones y los índices estén definidos y que los datos se hayan cargado de manera adecuada.
***

### VISTAS
**vista_cancelaciones_hotel:** cantidad de reservas canceladas por hotel.

**vista_estadias_largas:** reservas con estadías de cinco noches o más.

**vista_reservas_por_mes:** cantidad de reservas agrupadas por año y mes.

**vista_reservas:** información de las reservas junto con el hotel, estado, habitación asignada e importe.

**vista_reservas_adr_alto:** reservas con un ADR superior a 100.



***
***Trabajo práctico final: Base de datos libre***                                                                      
*Martinez Lucia, Quiroz Ornella*                                                                                
*3° - Base de Datos II – Gestión de Proyectos de Software*                                                           
*Ariel Nardelli, Matias Nardelli*                                                                           
15 de octubre, 2026                                                          

