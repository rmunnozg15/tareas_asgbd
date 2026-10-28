# Práctica: Instalación y Prueba de Clientes para SGBD (Oracle, PostgreSQL y MariaDB)

Este repositorio contiene la documentación y evidencias del despliegue y configuración de clientes de consola, gráficos y web para conectarse a **Oracle Database 23ai Free**, **PostgreSQL** y **MariaDB** en un entorno **Linux Mint / Debian**.

## Datos de la práctica

* **Nombre y Apellidos:** Robertoo Muñoz Galán

* **Grupo:** ASIR 2

* **Asignatura:** ASGBD

* **Fecha:** 19/10/2026

---

## Índice de Contenidos

1. [Tabla de Clientes Instalados](#1-tabla-de-clientes-instalados)

2. [Datos de la Máquina Virtual y Servidores](#2-datos-de-la-máquina-virtual-y-servidores)

3. [Instalación y Configuración Paso a Paso](#3-instalación-y-configuración-paso-a-paso)

   * [3.1. Clientes para Oracle Database](#31-clientes-para-oracle-database)

     * [SQL Developer (Gráfico)](#sql-developer-gráfico)

     * [Visual Studio Code + Extensión Oracle (Gráfico)](#visual-studio-code--extensión-oracle-gráfico)

     * [SQL\*Plus (Consola)](#sqlplus-consola)

     * [SQLcl (Consola)](#sqlcl-consola)

   * [3.2. Clientes para PostgreSQL](#32-clientes-para-postgresql)

     * [`psql` (Consola)](#psql-consola)

     * [`pgAdmin 4` (Gráfico)](#pgadmin-4-gráfico)

   * [3.3. Clientes para MariaDB](#33-clientes-para-mariadb)

     * [`mariadb` (Consola)](#mariadb-consola)

     * [`phpMyAdmin` (Web)](#phpmyadmin-web)

   * [3.4. Clientes Multi-SGBD](#34-clientes-multi-sgbd)

     * [DBeaver Community (Gráfico)](#dbeaver-community-gráfico)

     * [Adminer (Web)](#adminer-web)

4. [Pruebas de Conexión](#4-pruebas-de-conexión)

5. [Evidencias Gráficas](#5-evidencias-gráficas)

6. [Incidencias y Solución de Problemas](#6-incidencias-y-solución-de-problemas)

7. [Fuentes Consultadas](#7-fuentes-consultadas)

## 1. Tabla de Clientes Instalados

| SGBD | Cliente | Tipo | Fuente / Repositorio | Versión Instalada | Dependencias Requeridas | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| **Oracle** | SQL Developer | Gráfico | Web Oficial Oracle (`.zip`) | `26.2.0.186.2220` | `default-jdk`, `unzip`, `bellsoft-jdk17-full` | 
| **Oracle** | Extensión Oracle SQL Developer | Gráfico | VS Code Marketplace | `26.3.0` (VS Code `1.143.0`) | Visual Studio Code (`.deb`) | 
| **Oracle** | SQL\*Plus | Consola | Oracle Instant Client (`.zip`) | `23.26.4.0.0` | `libaio1t64` / symlink `libaio.so.1` | 
| **Oracle** | SQLcl | Consola | Web Oficial Oracle (`.zip`) | `26.3.0.0` | `default-jdk`, `unzip` | 
| **PostgreSQL** | `psql` | Consola | Repositorios APT Debian/Mint | `16.15` | `postgresql-client` | 
| **PostgreSQL** | `pgAdmin 4` | Gráfico | Repositorio Oficial pgAdmin APT | `9.18` (Desktop) | `curl`, `gnupg`, `lsb-release` | 
| **MariaDB** | `mariadb` | Consola | Repositorios APT Debian/Mint | `10.11.14-MariaDB` | `mariadb-client` | 
| **MariaDB** | `phpMyAdmin` | Web | Repositorios APT Debian/Mint | `5.2.1deb3` | `apache2`, `php`, `php-mysql`, `php-mbstring` | 
| **Multi-SGBD** | DBeaver Community | Gráfico | Web Oficial DBeaver (`.deb`) | `26.2.3` | Drivers JDBC (autodescarga) | 
| **Multi-SGBD** | Adminer | Web | Web Oficial Adminer (`.php`) | `latest.php` | `php-cli` | 

## 2. Datos de la Máquina Virtual y Servidores

### Máquina Virtual

* **Sistema Operativo:** Linux Mint

* **RAM:** 4 GB

* **CPU:** 2 vCPU

* **Almacenamiento:** 250 GB

* **IP de la Máquina Virtual:** `192.168.97.141`

### Datos de los SGBD

| SGBD | Servidor | Base / Servicio | Puerto | Usuario | 
| ----- | ----- | ----- | ----- | ----- | 
| Oracle Database 23ai Free | `localhost` | `FREEPDB1` | `1521` | `orauser` | 
| PostgreSQL | `localhost` | `dbpg` | `5432` | `pguser` | 
| MariaDB | `localhost` | `dbm` | `3306` | `muser` | 

## 3. Instalación y Configuración Paso a Paso

### 3.1. Clientes para Oracle Database

#### SQL Developer (Gráfico)

1. **Instalación de Java y descompresor inicial:**

   ```
   sudo apt update
   sudo apt install default-jdk unzip -y
   java --version
   
   ```

2. **Descarga y descompresión:**
   Descargado el paquete `sqldeveloper-26.2.0.186.2220-x64.zip` desde la web oficial de Oracle y descomprimido en `/opt/`:

   ```
   sudo unzip sqldeveloper-26.2.0.186.2220-x64.zip -d /opt/
   
   ```

3. **Corrección de dependencia de JavaFX:**
   Al intentar iniciar mediante `/opt/sqldeveloper/sqldeveloper.sh` surgió el error `Module javafx.base not found`. Se procedió a instalar BellSoft JDK 17 Full:

   ```
   wget https://download.bell-sw.com/java/17.0.10+13/bellsoft-jdk17.0.10+13-linux-amd64-full.deb -O ~/Descargas/jdk17-full.deb
   sudo apt install ~/Descargas/jdk17-full.deb -y
   /usr/lib/jvm/bellsoft-java17-full-amd64/bin/java --version
   
   ```

4. **Ejecución y Versión:**

   ```
   /opt/sqldeveloper/sqldeveloper.sh
   
   ```

   * **Versión instalada:** `26.2.0.186.2220`

#### Visual Studio Code + Extensión Oracle (Gráfico)

1. **Instalación de VS Code:**

   ```
   cd ~/Descargas
   sudo apt install ./code_1.143.0-1792533444_amd64.deb -y
   
   ```

2. **Instalación de la Extensión:**
   Desde el panel de extensiones de VS Code se buscó e instaló **Oracle SQL Developer** (publicada por Oracle).

   * **Versión de VS Code:** `1.143.0`

   * **Versión de la extensión:** `26.3.0`

#### SQL\*Plus (Consola)

1. **Descarga y estructura de directorios:**
   Se descargaron los paquetes `instantclient-basic-linux.x64-23.26.4.0.0.zip` y `instantclient-sqlplus-linux.x64-23.26.4.0.0.zip`.

   ```
   mkdir -p ~/oracle-client
   unzip instantclient-basic-linux.x64-23.26.4.0.0.zip -d ~/oracle-client
   unzip instantclient-sqlplus-linux.x64-23.26.4.0.0.zip -d ~/oracle-client
   
   ```

2. **Configuración del entorno y resolución de librerías:**

   ```
   export LD_LIBRARY_PATH="$HOME/oracle-client/instantclient_23_26:$LD_LIBRARY_PATH"
   export PATH="$HOME/oracle-client/instantclient_23_26:$PATH"
   
   # Corrección de la falta de libaio.so.1 en distros recientes
   sudo apt install libaio1t64 -y
   sudo ln -s /usr/lib/x86_64-linux-gnu/libaio.so.1t64 /usr/lib/x86_64-linux-gnu/libaio.so.1
   sudo ldconfig
   
   ```

3. **Comprobación de versión:**

   ```
   sqlplus -v
   
   ```

   * **Versión instalada:** `Release 23.26.4.0.0`

#### SQLcl (Consola)

1. **Instalación y extracción:**

   ```
   sudo apt install default-jdk unzip -y
   cd ~/Descargas
   unzip sqlcl-latest.zip -d ~/sqlcl
   
   ```

2. **Variables de entorno y comprobación:**

   ```
   echo 'export PATH="$HOME/sqlcl/sqlcl/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ~/sqlcl/sqlcl/bin/sql -version
   
   ```

   * **Versión instalada:** `26.3.0.0` (Interna: `26.3.0.260.1620`)

### 3.2. Clientes para PostgreSQL

#### `psql` (Consola)

1. **Instalación:**

   ```
   sudo apt update
   sudo apt install postgresql-client -y
   
   ```

2. **Comprobación de versión:**

   ```
   psql --version
   
   ```

   * **Versión instalada:** `16.15`

#### `pgAdmin 4` (Gráfico)

1. **Adición de claves y repositorio (Adaptación para Linux Mint):**

   ```
   sudo apt install curl gnupg lsb-release -y
   curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /etc/apt/keyrings/packages-pgadmin-org.gpg
   
   # Mapeo explícito a la versión base de Ubuntu (noble) para solventar el codename zena/virginia
   sudo sh -c 'echo "deb [signed-by=/etc/apt/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/noble pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'
   
   ```

2. **Instalación:**

   ```
   sudo apt update
   sudo apt install pgadmin4-desktop -y
   
   ```

   * **Versión instalada:** `9.18`

### 3.3. Clientes para MariaDB

#### `mariadb` (Consola)

1. **Instalación:**

   ```
   sudo apt update
   sudo apt install mariadb-client -y
   
   ```

2. **Comprobación de versión:**

   ```
   mariadb --version
   
   ```

   * **Versión instalada:** `10.11.14-MariaDB`

#### `phpMyAdmin` (Web)

1. **Instalación del entorno Web y phpMyAdmin:**

   ```
   sudo apt update
   sudo apt install apache2 php php-mysql php-mbstring php-zip php-gd php-curl phpmyadmin -y
   sudo phpenmod mbstring
   
   ```

2. **Vinculación con Apache:**

   ```
   sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
   sudo a2enconf phpmyadmin
   sudo systemctl restart apache2
   
   ```

   * **Versión instalada:** `5.2.1deb3`

### 3.4. Clientes Multi-SGBD

#### DBeaver Community (Gráfico)

1. **Instalación del paquete Debian:**

   ```
   cd ~/Descargas
   sudo apt install ./dbeaver-ce-26.2.3-linux-x86_64.deb -y
   
   ```

   * **Versión instalada:** `26.2.3`

#### Adminer (Web)

1. **Descarga y ejecución mediante servidor ligero PHP CLI:**

   ```
   sudo apt install php-cli wget -y
   mkdir -p ~/adminer && cd ~/adminer
   wget https://www.adminer.org/latest.php -O adminer.php
   php -S 127.0.0.1:8080 adminer.php
   
   ```

## 4. Pruebas de Conexión

### Comandos de prueba ejecutados

* **Oracle SQL\*Plus:**

  ```
  sqlplus orauser@//localhost:1521/FREEPDB1
  
  ```

* **Oracle SQLcl:**

  ```
  sql orauser@//localhost:1521/FREEPDB1
  
  ```

* **PostgreSQL psql:**

  ```
  psql -h localhost -U pguser -d dbpg -W
  
  ```

* **MariaDB CLI:**

  ```
  mariadb -h localhost -u muser -p dbm
  
  ```

* **phpMyAdmin:** Acceso vía web a `http://localhost/phpmyadmin/`

* **Adminer:** Acceso vía web a `http://127.0.0.1:8080/adminer.php`

## 5. Evidencias Gráficas

Las capturas de pantalla están almacenadas en el directorio `./images/` (o `evidencias/`):

* **Oracle SQL Developer (`images/foto1.png`):** Muestra la conexión exitosa al servicio `FREEPDB1` con el usuario `orauser`.

* **Oracle VS Code (`images/foto2.png`):** Demuestra la conexión activa mediante la extensión oficial de Oracle SQL Developer.

* **Oracle SQL\*Plus (`images/foto3.png`):** Terminal conectada a `FREEPDB1` con `orauser`.

* **Oracle SQLcl (`images/foto4.png`):** Interfaz moderna por consola autenticada en el servicio `FREEPDB1`.

* **PostgreSQL psql (`images/foto5.png`):** Evidencia de autenticación de `pguser` en la base de datos `dbpg`.

* **PostgreSQL pgAdmin 4 (`images/foto6.png`):** Query Tool interactivo abierto en la base de datos `dbpg`.

* **MariaDB CLI (`images/foto7.png`):** Sesión CLI activa como `muser` en `dbm`.

* **phpMyAdmin (`images/foto8.png`):** Panel de administración web conectado a MariaDB gestionando `dbm`.

* **DBeaver Community (`images/foto9.png`):** Gestión simultánea de las 3 conexiones (Oracle, PostgreSQL y MariaDB).

* **Adminer (`images/foto10.png`):** Inicio de sesión web ejecutado bajo el servidor local PHP CLI.

## 6. Incidencias y Solución de Problemas

1. **SQL Developer no encontraba JavaFX:**

   * *Síntoma:* `java.lang.module.FindException: Module javafx.base not found`.

   * *Solución:* El JDK por defecto no incluía componentes OpenJFX. Se instaló la distribución completa BellSoft JDK 17 Full (`bellsoft-jdk17.0.10+13-linux-amd64-full.deb`).

2. **Falta de biblioteca compartida `libaio.so.1` en Oracle SQL\*Plus:**

   * *Síntoma:* `sqlplus: error while loading shared libraries: libaio.so.1: cannot open shared object file`.

   * *Solución:* En las distribuciones recientes existe `libaio1t64`. Se instaló el paquete y se creó un enlace simbólico:

     ```
     sudo apt install libaio1t64
     sudo ln -s /usr/lib/x86_64-linux-gnu/libaio.so.1t64 /usr/lib/x86_64-linux-gnu/libaio.so.1
     sudo ldconfig
     
     ```

3. **PostgreSQL rechazaba conexiones por `localhost`:**

   * *Síntoma:* `psql: error: connection to server at "localhost" (127.0.0.1), port 5432 failed: Conexión rehusada`.

   * *Solución:* En `/etc/postgresql/16/main/postgresql.conf` se cambió `listen_addresses` a `'localhost,192.168.97.141'`. Se añadió en `/etc/postgresql/16/main/pg_hba.conf` la línea:

     ```
     host    dbpg    pguser    127.0.0.1/32    scram-sha-256
     
     ```

     Y se reinició el servicio con `sudo systemctl restart postgresql`.

4. **Incompatibilidad del repositorio APT en pgAdmin 4 con Linux Mint:**

   * *Síntoma:* `lsb_release -cs` devolvía `zena` (nombre clave de Mint), no reconocido en los repositorios oficiales de pgAdmin.

   * *Solución:* Se especificó manualmente la distribución base de Ubuntu `noble` en la configuración de fuentes `/etc/apt/sources.list.d/pgadmin4.list`.

5. **Error 404 en phpMyAdmin:**

   * *Síntoma:* `404 Not Found` al acceder a `http://localhost/phpmyadmin/`.

   * *Solución:* Apache no vinculó la configuración por defecto. Se creó un enlace simbólico a `/etc/phpmyadmin/apache.conf` dentro de `/etc/apache2/conf-available/phpmyadmin.conf`, activándolo con `sudo a2enconf phpmyadmin` y recargando Apache.

6. **Rechazo de conexión a MariaDB en DBeaver:**

   * *Síntoma:* `Socket fail to connect to localhost. Conexión rehusada`.

   * *Solución:* Se modificó `/etc/mysql/mariadb.conf.d/50-server.cnf` cambiando `bind-address` de `192.168.97.141` a `0.0.0.0` y se reinició MariaDB (`sudo systemctl restart mariadb`).

7. **Servidor web de Adminer inaccesible:**

   * *Síntoma:* El navegador no cargaba `http://127.0.0.1:8080/`.

   * *Solución:* El servidor HTTP incorporado de PHP requiere mantener activa la terminal. Se ejecutó `php -S 127.0.0.1:8080 adminer.php` de forma persistente.

## 7. Fuentes Consultadas

| Recurso | Uso | Fecha | 
| ----- | ----- | ----- | 
| Documentación oficial de Oracle Instant Client | Descarga y configuración de SQL\*Plus y dependencias E/S. | 21/10/2026 | 
| Guía de Instalación APT de pgAdmin 4 | Configuración del repositorio y claves GPG oficiales. | 21/10/2026 | 
| Documentación oficial de DBeaver Community | Instalación de cliente multi-SGBD y controladores JDBC. | 21/10/2026 | 
| Manual de usuario de Adminer | Despliegue mediante PHP CLI local. | 21/10/2026 | 
| Guía Práctica de la Asignatura (ASGBD) | Referencia principal de requisitos de la práctica. | 21/10/2026 | 
