#  Informe de gestión de incidentes que cumple con la norma ISO 27001
<!-- hide -->

> By [@rosinni](https://github.com/rosinni) and [other contributors](https://github.com/4GeeksAcademy/deploying-wordpress-debian/graphs/contributors) at [4Geeks Academy](https://4geeksacademy.co/)

[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*These instructions are [available in english](https://github.com/breatheco-de/incident-report-management-exercise-project/blob/main/README.md)*
<!-- endhide -->


<!-- hide -->


### Antes de empezar...

> ¡Te necesitamos! Estos ejercicios se crean y mantienen en colaboración con personas como tú. Si encuentras algún error o falta de ortografía, contribuye y/o repórtalo.

<!-- endhide -->

## 📋 Propósito del Proyecto

Este ejercicio tiene como objetivo enseñar a los estudiantes cómo identificar y reportar una vulnerabilidad de inyección SQL utilizando la aplicación web Damn Vulnerable Web Application (DVWA). El reporte se debe realizar de acuerdo a las normas ISO 27001 para la gestión de incidentes de seguridad de la información.

**Objetivos de Aprendizaje:**
- Comprender las vulnerabilidades de inyección SQL
- Aprender a usar DVWA para pruebas de seguridad
- Practicar la creación de informes de incidentes compatibles con ISO 27001
- Obtener experiencia práctica con herramientas de ciberseguridad

## 🛠️ Tecnologías Utilizadas

- **Virtualización:** VirtualBox
- **Sistema Operativo:** Debian Linux
- **Stack de Servidor Web:** LAMP (Linux, Apache, MySQL/MariaDB, PHP)
- **Aplicación Vulnerable:** DVWA (Damn Vulnerable Web Application)
- **Base de Datos:** MySQL/MariaDB
- **Estándares de Seguridad:** ISO 27001
- **Lenguajes:** SQL, PHP, HTML
- **Herramientas:** Línea de Comandos, Navegador Web

## 🌱 Cómo Instalar y Ejecutar

### Requisitos

* VirtualBox instalado en tu computadora.
* Una máquina virtual Debian instalada en VirtualBox. (usaremos la máquina previamente configurada en clases anteriores).


#### Beneficios de Usar una Máquina Virtual

- **Aislamiento:** Mantiene el entorno de pruebas separado de tu sistema operativo principal, protegiéndolo de posibles daños.

- **Facilidad de Restauración:** Puedes crear instantáneas (snapshots) de tu máquina virtual y restaurarlas fácilmente si algo sale mal.

- **Portabilidad:** Puedes mover y compartir la máquina virtual fácilmente con otros.

## 📝 Instrucciones

* Abre esta URL y forkea el siguiente repositorio https://github.com/breatheco-de/incident-report-for-sql-injection-exercise-project

 ![fork button](https://github.com/4GeeksAcademy/4GeeksAcademy/blob/master/site/src/static/fork_button.png?raw=true)

Un nuevo repositorio se creará en tu cuenta.

* Clona este nuevo repositorio forkeado utilizando Git para descargartelo a tu maquina local.
* Una vez que hayas clonado, sigue los pasos de mas abajo hasta el final.

### Paso 1: Verificar la configuración de la máquina virtual antes de iniciar:
- [ ] En la sección "Red", selecciona "Adaptador Puente" (Bridge Adapter) para que la VM esté en la misma red que tu host.

- [ ] Verificar la correcta instalación de MySQL(MariaDB) Apache, y PHP (LAMP Stack)

- [ ] Establece la contraseña del root de MariaDB y configura la seguridad básica.


### Paso 2: Instalación y Configuración de DVWA:
- [ ] Descargar DVWA desde el enlace proporcionado

```sh
cd /var/www/html 
sudo apt-get install wget unzip
sudo wget https://storage.googleapis.com/breathecode/virtualbox/DVWA.zip sudo unzip DVWA.zip 
sudo mv DVWA-master DVWA

```
- [ ] Configurar DVWA
Cambia al directorio DVWA y renombra el archivo de configuración
```sh
cd DVWA/config 
sudo cp config.inc.php.dist config.inc.php
```
- [ ] Edita el archivo de configuración `config.inc.php` para configurar las credenciales de MariaDB:
```ssh
sudo nano config.inc.php
```
> 💡 IMPORTANTE: Asegúrate de que las siguientes líneas tengan las credenciales correctas:
* $_DVWA[ 'db_user' ] = 'root';
* $_DVWA[ 'db_password' ] = 'tu_contraseña_de_root'; 
* $_DVWA[ 'db_database' ] = 'dvwa';

- [ ] Configurar la Base de Datos
Inicia sesión en MariaDB y crea la base de datos DVWA
```sh
sudo mysql -u root -p 
CREATE DATABASE dvwa; 
EXIT;
```
- [ ] Ajustar Permisos
```sh
sudo chown -R www-data:www-data /var/www/html/DVWA/
sudo chmod -R 755 /var/www/html/DVWA/
```
- [ ] Abre un navegador en tu VM y ve a http://localhost/DVWA/setup.php
- [ ] Revisa la configuración y Haz clic en "Create / Reset Database".


### Paso 3: Realización del Ataque SQL Injection
- [ ] Abre un navegador en la VM y accede a http://localhost/DVWA.
- [ ] Iniciar sesión en DVWA:
```
*Usuario: admin
*Contraseña: password
```
- [ ] Configurar el Nivel de Seguridad
Ve a la pestaña "DVWA Security" y selecciona el nivel "Low" para facilitar la explotación

- [ ] Ejecutar SQL Injection
Ve a la sección "SQL Injection" en DVWA
Ingresa un ataque de inyección SQL simple en el campo proporcionado de "User ID", por ejemplo:
```sh
1' OR '1'='1
```
Haz clic en "Submit" y observa cómo DVWA procesa la inyección y muestra los resultados de la base de datos. 
> 💡 NOTA: Deberías ver una lista de todos los usuarios extraída de la base de datos, indicando una inyección SQL exitosa.


![vulnerability](https://github.com/breatheco-de/incident-report-for-sql-injection-exercise-project/blob/main/assets/vulnerability.png?raw=true)



### Paso 4: Reporte del Incidente
- [ ] Cumple la Estructura del Reporte
  * Título del Reporte
  * Introducción
  * Descripción del Incidente
  * Proceso de Reproducción
  * Impacto del Incidente
  * Recomendaciones
  * Conclusión


> 💡 NOTA: Los informes de incidentes según la norma ISO 27001 no requieren específicamente la inclusión de imágenes, a menos que estas sean necesarias para ilustrar puntos críticos o detalles técnicos específicos del incidente. Sin embargo, en la mayoría de los casos, los informes suelen incluir capturas de pantalla, gráficos o diagramas solo si son relevantes para apoyar la explicación del incidente o para demostrar cómo se llevó a cabo la explotación de la vulnerabilidad.

[Descargar un ejemplo de reporte de incidente](https://github.com/breatheco-de/incident-report-for-sql-injection-exercise-project/blob/main/assets/incident_ISO27001_report.pdf?raw=true)

## 📝 Delivery

* En tu codespace en la raiz del proyecto forkeado, sube el  reporte en formato `.pdf` con el nombre `incident-report.pdf`

