# Introduccion y arquitectura Filezilla Server  



### Esquema activo de flujo de conexión entre clinte y servidor  

      CLIENTE                                 SERVIDOR
      +------------------+                    +------------------+
      |                  |   1. Petición      |                  |
      | Puerto Aleatorio |------------------->| Puerto 21        | (CANAL DE CONTROL)
      | (N)              |                    |                  |
      |                  |   2. Comando PORT  |                  |
      |                  |------------------->|                  |
      |                  |                    |                  |
      |                  |   3. Conexión      | Puerto 20        |
      | Puerto Aleatorio |<-------------------| (Data Port)      | (CANAL DE DATOS)
      | (N+1)            |                    |                  |
      +------------------+                    +------------------+


### Esquema pasivo de flujo de conexión entre clinte y servidor  
      
      CLIENTE                                 SERVIDOR
      +------------------+                    +------------------+
      |                  |   1. Petición      |                  |
      | Puerto Aleatorio |------------------->| Puerto 21        | (CANAL DE CONTROL)
      | (N)              |                    |                  |
      |                  |   2. Comando PASV  |                  |
      |                  |------------------->|                  |
      |                  |   Respuesta:       |                  |
      |                  |   "Usa puerto Y"   |                  |
      |                  |<-------------------|                  |
      |                  |                    |                  |
      | Puerto Aleatorio |   3. Conexión      | Puerto Aleatorio |
      | (N+1)            |------------------->| (Y)              | (CANAL DE DATOS)
      |                  |                    |                  |
      +------------------+                    +------------------+



| Característica | Modo Activo (Active) | Modo Pasivo (Passive) |
| :--- | :--- | :--- |
| **Canal de Control** | Lo inicia el **Cliente** (al puerto 21). | Lo inicia el **Cliente** (al puerto 21). |
| **Canal de Datos** | Lo inicia el **Servidor** (desde el puerto 20). | Lo inicia el **Cliente** (a un puerto aleatorio del servidor). |
| **Comando Clave** | `PORT` (El cliente dice: "conéctate a mí"). | `PASV` (El cliente dice: "dime dónde me conecto"). |
| **Puertos en Servidor** | Usa puerto 21 (mando) y 20 (datos). | Usa puerto 21 (mando) y puertos altos (>1023). |
| **Firewall / NAT** | **Problemático** (el firewall del cliente suele bloquear al servidor). | **Ideal** (funciona bien porque todo lo inicia el cliente). |
