# 🛠️ INSTALLATION.md – Instalación Completa del Mini SOC con Splunk

Este documento describe el proceso de instalación desde cero de todo el entorno Mini SOC:

1. Preparación de las máquinas virtuales  
2. Instalación de Splunk Enterprise Free en Ubuntu Server  
3. Configuración inicial  
4. Instalación del Universal Forwarder en Linux  
5. Validación del envío de logs  

---

# 📌 1. Preparación del Entorno Virtual

## 1.1 Crear la VM para Splunk

- Abrir VirtualBox → Nueva máquina  
- Nombre: `Splunk-Server`  
- Tipo: Linux  
- Versión: Ubuntu (64-bit)  
- RAM: **4096 MB mínimo**  
- CPU: **2 vCPUs mínimo**  
- Disco: **30GB**  

<img width="1359" height="292" alt="levantando vm" src="https://github.com/user-attachments/assets/ce2070b3-d145-42ea-8bea-3b0a4420651a" />

---

## 1.2 Configurar la red de la VM

- Seleccionar **Adaptador 1 → Red interna**
- Nombre: `MiniSOC_Net`

`Nota; para evitar problemas técnicos durante la instalación es recomendable mantener la red en formato "NAT".
Posteriormente podremos cambiar al formato "Adaptador puente" para que actúe como un endpoint real.`

<img width="1359" height="360" alt="configuracion vRed" src="https://github.com/user-attachments/assets/c9cddc19-674f-4e54-8704-1ea7f232db6e" />


---

## 1.3 Instalar Ubuntu Server

- Iniciar la VM y seleccionar la ISO de Ubuntu Server.  
- Elegir idioma, layout y configuración básica.  
- Crear usuario `splunkadmin`.

<img width="1357" height="686" alt="instalacion pantalla" src="https://github.com/user-attachments/assets/7de953c0-0f0b-4070-8c30-ad39cc74bf15" />


---

# 📌 2. Instalación de Splunk Enterprise Free

Actualizar repositorios:

`sudo apt update && sudo apt upgrade -y`

## 2.1 Descargar Splunk Enterprise

`wget -O splunk-10.0.2-e2d18b4767e9-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/10.0.2/linux/splunk-10.0.2-e2d18b4767e9-linux-amd64.deb"`

<img width="1341" height="170" alt="Descargando splunk" src="https://github.com/user-attachments/assets/1260b3d8-4723-4776-9a53-99c70df7ff93" />


## 2.2 Instalar Splunk

`sudo dpkg -i splunk-10.0.2-e2d18b4767e9-linux-amd64.deb`

<img width="717" height="181" alt="Instalando splunk" src="https://github.com/user-attachments/assets/b7203d6c-4ae2-4246-9a4c-dd116927b706" />


## 2.3 Iniciar Splunk y aceptar licencia

`sudo /opt/splunk/bin/splunk start --accept-license`

Aquí creamos un usuario y contraseña de administrador. (La contraseña debe ser en formato alfanumérico)

<img width="827" height="213" alt="ingresando usuario y contraseña" src="https://github.com/user-attachments/assets/adab24f0-ee15-4cf0-80a6-0a1b84b82d94" />


## 2.4 Habilitar Splunk para que arranque automáticamente

`sudo /opt/splunk/bin/splunk enable boot-start`

<img width="590" height="51" alt="splunk inicia al booteo" src="https://github.com/user-attachments/assets/200ade66-32ee-4f0b-bc1d-9e4d2df99590" />


## 2.5 Acceder a Splunk desde el navegador

Desde tu PC host abrir:

http://<IP_DEL_SPLUNK>:8000

ie. "http://198.162.100.24:8000"

<img width="860" height="544" alt="primer login en interfaz" src="https://github.com/user-attachments/assets/bfa1a24c-3e2b-4b8d-a11b-eff816b4d7e2" />


# 📌 3. Configuración básica en Splunk

Tras iniciar sesión:

-Ir a Settings
-Indexes
-New index: linux_logs

<img width="1359" height="647" alt="config básica de splunk" src="https://github.com/user-attachments/assets/4331550c-fde9-4dc4-b8da-84375615f18e" />


<img width="1359" height="382" alt="nuevo index" src="https://github.com/user-attachments/assets/10913295-4d62-460f-a97d-61accd564f40" />


# 📌 4. Preparar la segunda VM (Linux + UF)

## 4.1 Crear VM para el endpoint Linux

Nombre: Linux-UF

RAM: 2048 MB

CPU: 1–2 vCPUs

Red: Red interna (MiniSOC_Net)

<img width="1359" height="401" alt="preparación ubuntu forwarder" src="https://github.com/user-attachments/assets/d548785b-aef6-48e2-8c32-9a943a64d5cf" />


## 4.2 Instalar Debian/Ubuntu minimal

En este caso instalaremos un Ubuntu Desktop.


- Aquí ingresamos un usuario y contraseña para dicho "Endpoint".

<img width="1282" height="641" alt="instalacion ubuntu" src="https://github.com/user-attachments/assets/5457051a-f422-4d90-bc09-b733411ee276" />


- Anteriormente solo deberemos tocar "Siguiente" repetidas veces, en el caso de que quieran modificar algún aspecto de la instalación, lo pueden realizar con total libertad.

<img width="955" height="638" alt="proceso instalacion ubuntuf" src="https://github.com/user-attachments/assets/b6bbac87-7e4a-4619-95f7-d3348bf2a0fa" />

El proceso de instalación puede llegar a demorar varios minutos.


# 📌 5. Instalación del Universal Forwarder
## 5.1 Descargar UF

`wget -O splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/10.0.2/linux/splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.deb"`

<img width="798" height="324" alt="instalacion UF" src="https://github.com/user-attachments/assets/34a65b57-6cc0-4f90-835a-e44783822303" />


## 5.2 Instalar UF

`sudo dpkg -i splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.deb`  

<img width="802" height="237" alt="instalacion UF 2" src="https://github.com/user-attachments/assets/e5a64ef8-4903-44ab-b55c-217720da4aec" />


## 5.3 Iniciar UF y aceptar licencia

`sudo /opt/splunkforwarder/bin/splunk start --accept-license`

<img width="1086" height="443" alt="iniciando universal forwarder" src="https://github.com/user-attachments/assets/9ef48f38-f329-450c-8915-e66a6a66b7a2" />


# 📌 6. Configurar el Universal Forwarder
## 6.1 Configurar outputs.conf (enviar a Splunk)

Editar:

`sudo nano /opt/splunkforwarder/etc/system/local/outputs.conf`

Contenido:

[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = <IP_DEL_SPLUNK>:9997


📸 [INSERTAR CAPTURA: Archivo outputs.conf con IP de Splunk]
