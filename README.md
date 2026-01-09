# Introduccion y arquitectura Filezilla Server



###Esquema activo de flujo de conexión entre clinte y servidor

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
