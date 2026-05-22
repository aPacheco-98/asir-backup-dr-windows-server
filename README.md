# Proyecto ASIR - Sistema de copias de seguridad y recuperación ante desastres con Windows Server

Este repositorio recoge la documentación principal de mi Proyecto Intermodular de 2º de Administración de Sistemas Informáticos en Red (ASIR), centrado en el diseño e implantación de una infraestructura de copias de seguridad y recuperación ante desastres para una pyme simulada.

El proyecto se basa en la empresa simulada **Gestoría Numancia, S.L.**, una pyme de 8 trabajadores que necesita proteger su información corporativa frente a incidencias como borrado accidental, corrupción de datos, fallos del servidor o pérdida de acceso a recursos compartidos.

## Objetivo del proyecto

El objetivo principal ha sido implantar una solución realista, mantenible y defendible de backup y recuperación, utilizando servicios propios de administración de sistemas y redes.

La solución busca:

- Proteger la información corporativa.
- Automatizar las copias de seguridad.
- Aislar el repositorio de backup.
- Aplicar control de accesos mediante usuarios, grupos y permisos NTFS.
- Validar restauraciones reales de archivos y carpetas.
- Documentar la infraestructura y los procedimientos de recuperación.
- Incorporar administración remota segura mediante VPN.

## Arquitectura implantada

La infraestructura se ha desplegado en un entorno virtualizado y está formada por:

- **pfSense** como router/firewall.
- **SRV-PROD** como servidor principal de producción con Windows Server 2022.
- **SRV-BACKUP** como servidor dedicado al repositorio de copias.
- **CLI-USUARIOS** como cliente Windows 11 Pro para pruebas funcionales.

La red se ha dividido en tres segmentos:

| Red | Subred | Función |
|---|---|---|
| USUARIOS | 192.168.10.0/24 | Equipos cliente |
| SERVIDORES | 192.168.20.0/24 | Servicios principales |
| BACKUP | 192.168.30.0/24 | Repositorio de copias |

El diseño se basa en una política de mínimo privilegio y segmentación, permitiendo únicamente las comunicaciones necesarias entre redes.

## Servicios implantados

En el proyecto se han configurado y validado los siguientes servicios:

- Active Directory Domain Services.
- DNS interno para el dominio `numancia.local`.
- Compartición de archivos mediante SMB.
- Permisos NTFS por departamentos.
- Intranet interna con IIS sobre HTTPS.
- Sistema de copias automatizadas.
- Repositorio remoto de backup en SRV-BACKUP.
- OpenVPN en pfSense para administración remota segura.
- Acceso por RDP únicamente tras establecer la VPN.

## Sistema de copias

El sistema de copias protege la carpeta corporativa principal del servidor de producción y envía la información al repositorio remoto ubicado en SRV-BACKUP.

Características principales:

- Origen: carpeta corporativa de producción.
- Destino: repositorio remoto en SRV-BACKUP.
- Copia diaria programada.
- Retención de versiones.
- Automatización mediante PowerShell y tarea programada.
- Pruebas reales de restauración.

SRV-BACKUP se mantiene fuera del dominio para reforzar el aislamiento del repositorio y reducir la exposición frente a incidencias en el entorno de producción.

## Seguridad aplicada

Las principales medidas de seguridad implantadas son:

- Segmentación de red mediante pfSense.
- Bloqueo del acceso desde USUARIOS hacia BACKUP.
- Comunicación limitada entre SRV-PROD y SRV-BACKUP.
- Repositorio de copias aislado.
- Usuarios y grupos gestionados desde Active Directory.
- Permisos NTFS por departamento.
- Intranet publicada mediante HTTPS.
- Administración remota mediante OpenVPN.
- RDP no expuesto directamente a Internet.

## Documentación incluida

La documentación del proyecto está disponible en la carpeta `docs/`.

| Documento | Descripción |
|---|---|
| `memoria-final.pdf` | Memoria principal del proyecto |
| `presentacion-defensa.pdf` | Presentación utilizada en la defensa |
| `anexo-i-permisos-ntfs-smb.pdf` | Documentación de permisos NTFS y compartición |
| `anexo-ii-copias-restauracion.pdf` | Operativa de copias de seguridad y restauración |
| `anexo-iii-openvpn-rdp.pdf` | Implantación de acceso remoto seguro |
| `anexo-iv-sql-server.pdf` | Ampliación complementaria con SQL Server Express |

## Tecnologías utilizadas

- Windows Server 2022
- Windows 11 Pro
- Active Directory
- DNS
- SMB
- NTFS
- IIS
- HTTPS
- pfSense
- OpenVPN
- RDP
- PowerShell
- Windows Server Backup
- VirtualBox
- SQL Server Express

## Competencias trabajadas

Este proyecto me ha permitido reforzar competencias propias de administración de sistemas y redes:

- Diseño de infraestructura.
- Segmentación de red.
- Administración de Windows Server.
- Gestión de usuarios, grupos y permisos.
- Implantación de servicios corporativos.
- Copias de seguridad y recuperación.
- Seguridad defensiva básica.
- Documentación técnica.
- Pruebas funcionales.
- Mantenimiento preventivo y correctivo.

## Demostraciones en vídeo

La carpeta `docs/videos/` incluye un archivo con los enlaces a las demostraciones funcionales del proyecto.

- Demo corta: visión general del entorno implantado.
- Demo completa: validación más detallada de la infraestructura, copias, restauración y administración remota.
  
## Finalidad

Este repositorio tiene finalidad educativa y de portfolio profesional. El objetivo es mostrar una implantación técnica realista orientada a administración de sistemas, redes y ciberseguridad defensiva en un entorno de pequeña empresa.
