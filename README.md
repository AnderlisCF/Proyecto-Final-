🛡️ ZYLONET — Infraestructura de Red Empresarial
Proyecto Final — Conmutación y Enrutamiento
Profesor: Onel Luis Pelegrino | ITLA 2026
Cisco Simulación Enrutamiento Seguridad Segmentación
________________________________________
📄 Descripción del Proyecto
Diseño e implementación de la infraestructura de red para ZYLONET, una empresa orientada a servicios de ciberseguridad y protección de activos digitales, con presencia en tres sedes geográficas:
Sede	Rol	Dominio sugerido
🏢 Santo Domingo	Sede Central (Core)	sd.zylonet.com.do
🏢 Santiago	Sede Sucursal	stgo.zylonet.com.do
🏢 La Romana	Sede Sucursal	romana.zylonet.com.do
La arquitectura implementa un modelo jerárquico de 3 capas (Núcleo → Distribución → Acceso), con segmentación por VLANs, enrutamiento dinámico OSPF multi-área, VPN IPsec inter-sedes, redundancia de gateway, seguridad de capa 2 y acceso remoto seguro por SSH.
________________________________________
👥 Equipo de Trabajo — ZYLONET
Nombre	Rol
Anderlis Caraballo Frias  |	CEO e Ingeniera en redes
Samantha Perez Fernandez  |	Encargada del área de marketing y especialista en seguridad en la nube
Emely Carolina Carrasco Torres | Especialista en respuesta a incidentes
Dairy Ibeth Rondon Constanza  |	Arquitecta de seguridad
Alan Junior Morel Marte |	Ingeniero especializado en infraestructura y gestión de servidores
Cristopher Naveo Aquino	| Especialista en seguridad de red
Lissabeth Leonor Turbides Valdez	|  Administración en sistemas
________________________________________
🏗️ Arquitectura de Red
Modelo Jerárquico de 3 Capas
                     INTERNET / ISP
                           |
          -------------------------------------------
          |                    |                    |
       R-CORE1               R-14               ROMANA
   (Santo Domingo)        (Santiago)         (La Romana)
          |                    |                    |
   ----------------        ---------            ---------
   |              |        |       |            |       |
 R-SW1          R-SW2    SW-6    SW-9         SW-7    SW-8
   |  \         /  |                       
 SW-3 SW-4   SW-5                     Hosts / PCs / Servicios
Distribución por sede
•	Santo Domingo: R-CORE1, R-SW1, R-SW2, SW-3, SW-4, SW-5
•	Santiago: R-14, SW-6, SW-9, servidores DNS/WEB/DHCP, NFS/RADIUS y MAIL
•	La Romana: ROMANA, SW-7, SW-8 y estaciones de usuario
________________________________________
🧰 Tecnologías Implementadas
Tecnología	Descripción
OSPF Multi-área	Enrutamiento dinámico entre la sede central y sucursales
VLANs + 802.1Q	Segmentación lógica por departamentos
VLSM	Uso eficiente del bloque 192.168.0.0/16
EtherChannel	Redundancia y agregación de enlaces entre switches
STP / PortFast / BPDU Guard	Prevención de bucles y protección en puertos de acceso
DHCP	Asignación dinámica de direcciones IP
VPN IPsec	Comunicación cifrada entre las 3 sedes
SSH v2	Administración remota segura
DHCP Snooping	Protección contra servidores DHCP falsos
Port Security	Control de acceso físico en switches
ACLs	Restricción del acceso administrativo por SSH
DNS / WEB / MAIL / NFS-RADIUS	Servicios centralizados en la sede de Santiago
________________________________________
🧭 Esquema de Direccionamiento IP
Parámetros Generales
Parámetro	Valor	Descripción
Bloque privado asignado	192.168.0.0/16	Espacio de direccionamiento interno
Bloque público asignado	19.0.0.0/24	Enlaces WAN hacia el ISP
Crecimiento proyectado	40 % a 5 años	Aplicado a todos los departamentos
Segmentación P2P / WAN	/30	Mínimo de 2 IPs útiles por enlace
Santo Domingo
VLAN	Departamento	Red	Gateway
10	SOC-Analistas	192.168.0.0/24	192.168.0.254
20	SOC-Incidentes	192.168.2.0/25	192.168.2.126
30	SOC-Herramientas	192.168.1.128/25	192.168.1.254
40	Admin-Corp	192.168.1.0/25	192.168.1.126
Santiago
VLAN	Departamento	Red	Gateway
100	Ventas	192.168.3.64/27	192.168.3.65
110	Centro de Datos	192.168.3.96/27	192.168.3.97
120	Administración	192.168.3.144/28	192.168.3.145
La Romana
VLAN	Departamento	Red	Gateway
200	Depto. 2	192.168.2.128/25	192.168.2.129
210	Depto. 1	192.168.3.0/26	192.168.3.1
220	Depto. 3	192.168.3.128/28	192.168.3.129
________________________________________
🌐 Enlaces Punto a Punto Internos
Enlace lógico	Red / Prefijo	IP Interfaz 1	IP Interfaz 2
R-CORE1 ↔ R-SW1	192.168.4.0/30	192.168.4.1	192.168.4.2
R-CORE1 ↔ R-SW2	192.168.4.4/30	192.168.4.5	192.168.4.6
R-SW1 ↔ R-SW2	192.168.4.8/30	192.168.4.9	192.168.4.10
________________________________________
🌍 Direccionamiento Público WAN
Enlace WAN	Red / Prefijo	IP del equipo	IP del ISP
R-CORE1 ↔ ISP	19.0.0.0/30	19.0.0.1	19.0.0.2
R-14 ↔ ISP	19.0.0.4/30	19.0.0.5	19.0.0.6
ROMANA ↔ ISP	19.0.0.8/30	19.0.0.9	19.0.0.10
WebServer ↔ ISP	19.0.0.12/30	19.0.0.13	19.0.0.14
________________________________________
🔐 Políticas de Seguridad
•	SSH v2 habilitado en los routers de borde para administración remota segura
•	VPN IPsec para comunicación cifrada entre Santo Domingo, Santiago y La Romana
•	Port Security en puertos de acceso de usuario
•	BPDU Guard + PortFast en puertos de acceso
•	DHCP Snooping activo en VLANs de usuario
•	ACL-SSH para restringir quién puede administrar los dispositivos
•	VLAN nativa y VLAN de parking para endurecimiento de troncales y puertos no usados
________________________________________
🖥️ Servicios de la Empresa
ZYLONET ofrece como enfoque principal:
1.	Respuesta a Incidentes (DFIR)
2.	Gestión de Firewalls y VPN
3.	Monitoreo y Detección de Amenazas 24/7
4.	Análisis de Vulnerabilidades y Pruebas de Penetración
5.	Cumplimiento Normativo (GRC) y Gestión de Parches
________________________________________
🧪 Plataforma de Simulación
Este proyecto fue diseñado y probado en PNetLab, utilizando:
•	Cisco 7200 para routers
•	Cisco IOS L3 para switches multicapa
•	Cisco IOS L2 para switches de acceso
•	Servidores Linux para DNS, DHCP, WEB, MAIL y NFS/RADIUS
________________________________________
📁 Estructura sugerida del repositorio
zylonet-network-infra/
│
├── README.md
├── docs/
│   ├── PROYECTO_FINAL.pdf
│   ├── direccionamiento-ip.md
│   ├── equipos.md
│   └── cotizacion.md
│
├── configs/
│   ├── santo-domingo/
│   │   ├── R-CORE1.txt
│   │   ├── R-SW1.txt
│   │   ├── R-SW2.txt
│   │   ├── SW-3.txt
│   │   ├── SW-4.txt
│   │   └── SW-5.txt
│   ├── santiago/
│   │   ├── R-14.txt
│   │   ├── SW-6.txt
│   │   └── SW-9.txt
│   └── romana/
│       ├── ROMANA.txt
│       ├── SW-7.txt
│       └── SW-8.txt
│
├── diagrams/
│   ├── topologia-general.png
│   └── arquitectura-red.png
│
└── scripts/
    ├── seguridad.txt
    └── scrip-zylonet.txt
________________________________________
🎯 Conclusión
Este proyecto demuestra el diseño e implementación de una infraestructura de red segura, escalable y jerárquica para ZYLONET, integrando conectividad entre sedes, segmentación lógica, servicios de red, redundancia y controles de seguridad alineados con un entorno empresarial real.
________________________________________
🙌 Créditos
Proyecto académico desarrollado por el equipo de ZYLONET para la asignatura de Conmutación y Enrutamiento — TI-203.
