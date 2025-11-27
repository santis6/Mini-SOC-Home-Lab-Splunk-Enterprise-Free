# 🛡️ Mini SOC con Splunk Enterprise Free

Un laboratorio práctico diseñado para aprender los fundamentos de un SOC real utilizando **Splunk Enterprise Free** y un **Universal Forwarder** en Linux.  
Este proyecto recrea un entorno empresarial pequeño pero funcional para practicar:

- Recolección y envío de logs  
- Consultas SPL  
- Detecciones de seguridad  
- Dashboards  
- Alertas  
- Flujo básico de análisis en un SOC  

---

# 📚 Índice

- [Descripción General](#-descripción-general)
- [Arquitectura del Proyecto](#-arquitectura-del-proyecto)
- [Objetivos](#-objetivos)
- [Componentes del Repositorio](#-componentes-del-repositorio)
- [Requisitos](#-requisitos)
  - [Hardware](#hardware)
  - [Software](#software)
- [Guía Rápida de Inicio](#-guía-rápida-de-inicio)
- [Casos de Uso Incluidos](#-casos-de-uso-incluidos)
- [Dashboards](#-dashboards)
- [Solución de Problemas](#-solución-de-problemas)
- [Autor](#-autor)

---

# 📝 Descripción General

Este proyecto implementa un **Mini SOC** utilizando Splunk Enterprise Free.  
Permite aprender, practicar y entender cómo funciona el monitoreo de seguridad en entornos Linux mediante la recolección, análisis y visualización de logs.

Incluye:

- Instalación completa del SIEM  
- Configuración de un Universal Forwarder  
- Creación de alertas, dashboards y casos de uso  
- Arquitectura documentada  
- Archivos SPL listos para usar  

---

# 🧩 Arquitectura del Proyecto

El laboratorio funciona sobre una red interna (VirtualBox) y está compuesto por:

- **Splunk Enterprise Server** → Ubuntu Server  
- **Linux Endpoint** → Debian/Ubuntu + Universal Forwarder  
- Flujo de datos:

  **Logs del endpoint → UF → Splunk → Dashboards / Alertas**

Más detalles, diagramas y tablas se encuentran en:  
👉 `ARCHITECTURE.md`

---

# 🎯 Objetivos

- Comprender la arquitectura básica de un SOC.  
- Practicar consultas SPL orientadas a seguridad.  
- Detectar actividades sospechosas en endpoints Linux.  
- Crear dashboards prácticos.  
- Configurar alertas reales basadas en eventos del sistema.  
- Aprender a trabajar con un SIEM desde cero.

---

# 📁 Componentes del Repositorio

Este proyecto incluye:

- **INSTALLATION.md** → Instalación detallada del entorno  
- **CONFIGURATION.md** → Configuraciones clave de Splunk y UF  
- **USE-CASES.md** → Casos de uso reales documentados  
- **ALERTS.md** → Alertas listas para usar  
- **DASHBOARDS.md** → Dashboards + JSON  
- **TROUBLESHOOTING.md** → Problemas comunes y soluciones  
- **/assets** → Diagramas, capturas, configuraciones  
- **LICENSE**

---

# 🖥️ Requisitos

## Hardware
- 8 GB RAM (mínimo)
- CPU 4 hilos
- 50 GB de almacenamiento libre

## Software
- VirtualBox / VMware
- Ubuntu Server LTS
- Splunk Enterprise Free
- Splunk Universal Forwarder

---

# 🚀 Guía Rápida de Inicio

1. Crear VM Ubuntu Server  
2. Instalar Splunk Enterprise  
3. Habilitar el servicio y acceder al Web UI  
4. Crear VM Linux secundaria  
5. Instalar Splunk Universal Forwarder  
6. Configurar `outputs.conf` y `inputs.conf`  
7. Validar que los logs lleguen  
8. Cargar dashboards y alertas del repo

La guía completa está en:  
👉 `INSTALLATION.md`

---

# 🔍 Casos de Uso Incluidos

- Detección de fuerza bruta SSH  
- Intentos fallidos de sudo  
- Acceso sospechoso a cuentas críticas  
- Cambios de usuarios o grupos  
- Manipulación de logs  
- Persistencia simple en Linux  

Documentados en:  
👉 `USE-CASES.md`

---

# 📊 Dashboards

El repositorio incluye paneles listos para importar con visualizaciones de:

- Autenticaciones SSH  
- Actividad de sudo  
- Eventos críticos  
- Estados del sistema  
- Monitoreo general del endpoint  

Capturas y JSON disponibles en:  
👉 `DASHBOARDS.md`

---

# ❗ Solución de Problemas

Errores cubiertos:

- UF no envía logs  
- Indexes no visibles  
- Permisos incorrectos  
- Splunk no arranca después de reiniciar  
- Logs duplicados o incompletos  

Disponible en:  
👉 `TROUBLESHOOTING.md`

---

# 👤 Autor

**Santiago Daniel Sandili**

Proyecto creado con fines educativos y de entrenamiento práctico en **Blue Team**, **SOC** y **ciberseguridad**.

---
