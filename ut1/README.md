# UT1. Servidores Web I - Nginx en AWS

**Autor:** percy  
**Repositorio:** sri-percy  

---

## Esquema de Arquitectura de Red (AWS)

* **VPC:** `vpc-percy` (`10.6.0.0/16`)
* **Subred Pública:** `subnet-pub-percy` (`10.6.1.0/24`)
* **Internet Gateway:** `igw-percy`
* **Tabla de Rutas:** `rt--pub-percy` (Ruta `0.0.0.0/0` hacia `igw-percy`)
* **Grupo de Seguridad:** `web-percy`
  * **SSH (22):** Permitido únicamente desde la IP del administrador (`81.9.192.66/32`).
  * **HTTP (80):** Permitido desde cualquier origen (`0.0.0.0/0`).
  * **Custom TCP (8080):** Permitido desde cualquier origen (`0.0.0.0/0`).
* **Instancia EC2:** `web-percy` (`t3.medium`, Ubuntu 24.04 LTS, Clave `vockey`).

---

## Apartado 1. Tu red y tu instancia en AWS (CE 3.b)

### Acciones realizadas:
1. Se ha creado una VPC propia (`vpc-percy`) con el bloque CIDR `10.6.0.0/16`, omitiendo la VPC por defecto de AWS.
2. Se ha configurado una subred pública (`subnet-pub-percy`) en el bloque `10.6.1.0/24` con la asignación automática de IP pública habilitada.
3. Se ha creado un Internet Gateway (`igw-percy`), se ha asociado a la VPC y se ha configurado la tabla de rutas pública (`rt--pub-percy`) para enrutar el tráfico hacia `0.0.0.0/0`.
4. Se ha creado el grupo de seguridad `web-percy` aplicando el principio de mínimo privilegio (restringiendo SSH a la IP de trabajo y abriendo los puertos 80 y 8080 al público).
5. Se ha desplegado una instancia EC2 `t3.medium` con Ubuntu Server 24.04 LTS, vinculada a la subred pública y al par de claves `vockey`.
6. Se ha actualizado el sistema operativo mediante los repositorios oficiales y se ha configurado la zona horaria a `Europe/Madrid`.

### Evidencias:
* **Mapa de recursos de la VPC:**  
  ![Mapa VPC](evidencias/mapa-vpc.png)

* **Reglas de entrada del Grupo de Seguridad:**  
  ![Grupo de Seguridad](evidencias/grupo-seguridad.png)

* **Detalle de la Instancia EC2:**  
  ![Detalle Instancia](evidencias/detalle-instancia.png)

* **Comprobación de la zona horaria (`timedatectl`):**  
  ![Timedatectl](evidencias/timedatectl.png)
