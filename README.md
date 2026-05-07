Implementación de Alta Disponibilidad con pfSense en Proxmox VE
Descripción

Este proyecto consiste en la implementación de una solución de alta disponibilidad (HA) para firewalls utilizando pfSense en un entorno virtualizado mediante Proxmox VE. El objetivo principal es garantizar la continuidad de servicio en caso de fallo de uno de los firewalls, eliminando el punto único de fallo (SPOF) en la infraestructura de red.

Se utilizan los protocolos CARP (para compartir una IP virtual), pfsync (para sincronización de conexiones) y XMLRPC (para sincronización de la configuración) para mantener el sistema redundante y funcional sin intervención manual.

Tecnologías Utilizadas
Proxmox VE: Plataforma de virtualización.
pfSense CE: Firewall y router de código abierto.
Ubuntu Server 24.04: Sistema operativo para simular el gateway ISP (ISP-GW).
Windows Server 2019/2022: Para la implementación de Active Directory (AD), DNS, y servicio de backup.
CARP: Common Address Redundancy Protocol, para compartir IP virtual.
pfsync: Para la sincronización de tablas de estado entre nodos pfSense.
XMLRPC: Para la sincronización de la configuración entre los firewalls.
Arquitectura

El sistema está compuesto por:

Proxmox VE: Contiene las máquinas virtuales que simulan los dispositivos de la red.
pfSense-01: Firewall principal (MASTER).
pfSense-02: Firewall secundario (BACKUP).
ISP-GW: Gateway simulado para proporcionar acceso a Internet.
SRV-CORE (Ubuntu): Servidor que simula servicios internos de la red.
WIN-SRV-01: Servidor Windows que provee Active Directory, DNS y copias de seguridad.
CLIENT-01 y CLIENT-02: Clientes simulados conectados a la red LAN.

El sistema utiliza un failover automático en caso de fallo de pfSense-01, garantizando la continuidad de servicio sin intervención manual.

Requisitos
Proxmox VE: Para la virtualización del entorno.
pfSense CE: Para la configuración de los firewalls.
Ubuntu Server: Para el gateway.
Windows Server 2019/2022: Para la implementación de servicios AD y DNS.
Conocimientos básicos en redes, firewalling y virtualización.
Pasos de Implementación
Instalación de Proxmox VE: Se crea un entorno de virtualización en Proxmox donde se van a crear las máquinas virtuales.
Creación de las máquinas virtuales:
pfSense-01 y pfSense-02 como firewalls.
ISP-GW para simular la salida a Internet.
SRV-CORE para servicios internos.
WIN-SRV-01 para servicios de Active Directory, DNS y copias de seguridad.
Configuración de la red: Se configuran las redes WAN, LAN y SYNC para la comunicación entre los firewalls y los servidores.
Implementación de Alta Disponibilidad:
Se configura CARP para la IP virtual compartida entre los dos firewalls.
Se sincronizan las conexiones activas utilizando pfsync.
Se sincroniza la configuración con XMLRPC.
Pruebas de Failover: Se realiza una prueba de failover apagando el nodo pfSense-01 para verificar que pfSense-02 asume automáticamente el rol de MASTER sin pérdida de conexión.
Configuración de servicios en Windows Server:
Active Directory, DNS, y copias de seguridad.
Pruebas de conectividad: Se realizan pruebas de conectividad desde los clientes para verificar que el tráfico no se ve interrumpido tras el failover.
Capturas de Pantalla

Las siguientes capturas de pantalla muestran los pasos clave de la implementación:

CAP-40 – Creación de la máquina virtual WIN-SRV-01 en Proxmox.
CAP-41 – Inicio de instalación de Windows Server.
CAP-42 – Configuración inicial de Windows Server.
CAP-43 – Configuración de IP estática en WIN-SRV-01.
CAP-44 – Instalación del rol Active Directory.
CAP-45 – Configuración de DNS en Windows Server.
CAP-46 – Promoción de WIN-SRV-01 a Controlador de Dominio.
CAP-47 – Creación de usuarios y grupos en Active Directory.
CAP-48 – Configuración de carpeta compartida en Windows Server.
CAP-49 – Configuración de copias de seguridad.
CAP-50 – Unión de CLIENT-01 al dominio.
CAP-51 – Validación de inicio de sesión con usuario del dominio.
Conclusiones

El proyecto demuestra cómo pfSense y Proxmox VE pueden ser utilizados para implementar una arquitectura de alta disponibilidad en el firewall perimetral de una red, garantizando la continuidad de servicio en caso de fallo. La combinación de CARP, pfsync y XMLRPC proporciona una solución robusta para la sincronización de estados y configuración entre los firewalls, mientras que Windows Server aporta servicios críticos como Active Directory, DNS y copias de seguridad.

Este proyecto es escalable y puede ser adaptado a entornos de producción con una infraestructura más robusta, proporcionando una solución de alta disponibilidad de bajo coste en entornos virtualizados.