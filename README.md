🔐 pfSense HA en Proxmox VE

Proyecto intermodular que implementa alta disponibilidad de firewall en un entorno virtualizado, usando pfSense y Proxmox VE para garantizar continuidad, redundancia y seguridad.

🧠 Descripción del proyecto
Este proyecto consiste en desplegar una infraestructura de red virtualizada con dos firewalls pfSense en modo HA, simulando un entorno empresarial con failover automático. El objetivo es evitar puntos únicos de falla y mantener el tráfico seguro y disponible aun cuando un firewall deje de funcionar.

🎯 Objetivo principal
Diseñar y validar una solución de alta disponibilidad para el perímetro de red, basada en:
- Proxmox VE para virtualización
- pfSense CE como firewall y router
- CARP, pfsync y XMLRPC para sincronización y failover
- Simulación de servicios internos con Ubuntu y Windows Server

🛠️ Tecnologías utilizadas
- Proxmox VE
- pfSense CE
- Ubuntu Server 24.04 (ISP-GW y servidor de servicios)
- Windows Server 2019/2022 (Active Directory, DNS y backup)
- CARP: IP virtual compartida para HA
- pfsync: Sincronización de tablas de estado
- XMLRPC: Sincronización de configuración

📡 Arquitectura del entorno
El proyecto se compone de:
- pfSense-01: firewall principal (MASTER)
- pfSense-02: firewall secundario (BACKUP)
- ISP-GW: gateway simulado con Ubuntu Server
- SRV-CORE: servidor Ubuntu para servicios internos
- WIN-SRV-01: Windows Server con Active Directory y DNS
- CLIENT-01 y CLIENT-02: estaciones de usuario

🔧 Configuración clave
- Redundancia de firewalls con CARP
- Sincronización de estado de conexiones con pfsync
- Sincronización de configuración con XMLRPC
- Redes WAN, LAN y SYNC correctamente separadas

📌 Componentes principales
- Proxmox VE como plataforma de virtualización
- Dos instancias pfSense en modo HA
- Gateway ISP simulado con Ubuntu
- Servidor de dominio y DNS en Windows Server
- Clientes conectados a la LAN para pruebas de conectividad

✅ Resultados esperados y verificados
- Failover automático entre pfSense-01 y pfSense-02
- Continuidad del servicio tras caída de un firewall
- Estado y configuración sincronizados en ambos nodos
- Acceso seguro a la red interna
- Simulación de entorno realista con servicios de directorio y DNS

📋 Pasos principales del proyecto
1. Instalación y configuración de Proxmox VE.
2. Creación de máquinas virtuales para firewalls, gateway, servidores y clientes.
3. Configuración de redes, interfaces y VLANs necesarias.
4. Implementación de HA con CARP, pfsync y XMLRPC.
5. Configuración de servicios internos en Ubuntu y Windows Server.
6. Pruebas de failover y conectividad desde clientes.

🖼️ Capturas de pantalla incluidas
- CAP-40: Creación de WIN-SRV-01 en Proxmox
- CAP-41: Instalación inicial de Windows Server
- CAP-42: Configuración de Windows Server
- CAP-43: IP estática en WIN-SRV-01
- CAP-44: Instalación de Active Directory
- CAP-45: Configuración de DNS
- CAP-46: Promoción a controlador de dominio
- CAP-47: Usuarios y grupos en Active Directory
- CAP-48: Carpeta compartida configurada
- CAP-49: Backup configurado
- CAP-50: Cliente unido al dominio
- CAP-51: Inicio de sesión validado

🚀 Conclusión
Esta implementación demuestra cómo combinar pfSense y Proxmox VE para crear una solución de firewall redundante y resistente. Con CARP, pfsync y XMLRPC, el proyecto asegura que la red siga operativa aunque uno de los firewalls falle.

📌 Autor
Oliver Domínguez Castro
Proyecto intermodular - Sistemas Microinformáticos y Redes

⚠️ Nota
El proyecto se realizó en un entorno de laboratorio con recursos controlados y busca replicar un escenario empresarial real para validar el diseño de alta disponibilidad y seguridad.