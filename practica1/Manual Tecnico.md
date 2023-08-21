# Manual Tecnico

## Tabla de configuracion de VPC

| Nombre  | Ip | Mascara de subred  |  Area | Nivel  |
|---|---|---|---|---|
| Almacenamiento_1  |   192.168.3.1|   255.255.255.0| Almacenamiento  |  1 |
|  Almacenamiento_2 |  192.168.3.2 |  255.255.255.0 | Almacenamiento  |  1 |
| Recepcion_1  |  192.168.3.3  |  255.255.255.0 | Recepcion  |  1 |
| Recepcion_2  |  192.168.3.4  |  255.255.255.0 | Recepcion  |  1 |
| Atencion_1 |  192.168.3.5  |  255.255.255.0 | Atencion al cliente |  2 |
| Atencion_2 |  192.168.3.6  |  255.255.255.0 | Atencion al cliente |  2 |
| Atencion_3 |  192.168.3.7  |  255.255.255.0 | Atencion al cliente |  2 |
| Atencion_4 |  192.168.3.8  |  255.255.255.0 | Atencion al cliente |  2 |
| Admin_1 |  192.168.3.9  |  255.255.255.0 | Administracion|  2 |
| Admin_2 |  192.168.3.10  |  255.255.255.0 | Administracion|  2 |
| Admin_3 |  192.168.3.11  |  255.255.255.0 | Administracion|  2 |
| Gerencia_1 |  192.168.3.12  |  255.255.255.0 | Gerencia | 3
| Gerencia_2 |  192.168.3.13  |  255.255.255.0 | Gerencia | 3
| Op_1 |  192.168.3.14  |  255.255.255.0 | Operaciones | 3
| Op_2 |  192.168.3.15  |  255.255.255.0 | Operaciones | 3
| Op_3 |  192.168.3.16  |  255.255.255.0 | Operaciones | 3

## Listado de Hardware

| Nombre                  | Modelo             | Descripción                                                                           | Cantidad | Precio unidad |
|-------------------------|--------------------|---------------------------------------------------------------------------------------|----------|---------------|
| D-Link PoE+ Switch      | DGS-1210-10P       | Switch Gigabit ethernet con 10 puertos. Estos switch van en el primer y tercer nivel. | 2        | Q1302.32      |
| Managed Network Switch  | QSW-M2116P-2T2S-US | Switch Gigabit ethernet con 20 puertos. Este switch va en el segundo nivel.           | 1        | Q6272.15      |
| Laptop de oficina DELL  | DELL E6420         | Computadora correspondiente a los diferentes niveles y áreas.                         | 16       | Q1,795.00     |

## Configuracion de las VPC
### Nivel 1
Almacenamiento_1:

    ip 192.168.3.1/24
    save

### Nivel 2
Admin_2:

    ip 192.168.3.10/24
    save

### Nivel 3
Op_3:

    ip 192.168.3.16/24
    save



## Pcapng

### Primera captura (Ping entre areas y ARP)
Recepcion1 a Admin3

### Segunda captura (Ping entre areas)
Atencion4 a Op_3

### Tercera captura (Ping entre areas)
Gerencia_2 a Almacenamiento_2
