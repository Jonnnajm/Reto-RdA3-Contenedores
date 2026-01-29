# Reto RdA3 Contenedores

**Título:** "Anatomía de un Contenedor: Del Kernel Linux a WordPress en Docker"

**Objetivo:** Demostrar la comprensión de los mecanismos del kernel Linux que hacen posible la tecnología de contenedores, aplicándolos en la implementación de un sistema web WordPress.

---

## 1. Parte Teórica: Investigación

### Fundamentos de Contenedores

1. **Historia evolutiva**: Desde `chroot` (1979) → LXC → Docker (2013). Cada etapa mejora aislamiento y facilidad de despliegue.
2. **Contenedores vs Máquinas Virtuales**:

| Característica       | Contenedores      | Máquinas Virtuales |
| ------------------- | ---------------- | ---------------- |
| Nivel de abstracción | OS               | Hardware + OS    |
| Consumo de recursos  | Bajo             | Alto             |
| Tiempo de inicio     | Segundos         | Minutos          |
| Aislamiento de HW    | Parcial          | Completo         |
| Imágenes/plantillas  | Ligero           | Pesado           |

### Mecanismos del Kernel Linux

| Mecanismo                    | Función en el SO | Rol en Docker | Comando para verificar |
| ---------------------------- | ---------------- | ------------- | ---------------------- |
| **Namespaces**               | Aislar recursos de procesos | Contenedores separados | `lsns` |
| - PID                        | Gestiona IDs de procesos | Aísla procesos | `docker inspect <container>` |
| - NET                        | Red virtual | Interfaces de red propias | `docker network ls` |
| - MNT                        | Sistema de archivos | Capas de FS por contenedor | `mount` |
| - UTS                        | Nombres de host | Hostnames independientes | `hostname` |
| - USER                       | IDs de usuario | Usuarios aislados | `id` |
| **Control Groups (cgroups)** | Limita y monitoriza recursos | CPU, memoria, I/O controlados | `docker stats` |
| - CPU                        | Control de CPU | Limita % CPU | `docker stats` |
| - Memory                     | Memoria RAM | Limita uso RAM | `docker stats` |
| - Blkio                      | I/O de disco | Limita disco | `docker stats` |
| **Capabilities**             | Privilegios de procesos | Permisos ajustables | `capsh --print` |
| **Union Filesystem**         | Capas de FS | Capas de imagen Docker | `docker history <image>` |

### Arquitectura de Docker

1. **Docker Daemon**: Ejecuta y gestiona contenedores.  
2. **Docker Client**: CLI que envía comandos al daemon.  
3. **Docker Registry**: Almacena imágenes (Docker Hub).  
4. **Imágenes vs Contenedores**: Imagen = plantilla, Contenedor = instancia ejecutable.  
5. **Dockerfile**: Archivo con instrucciones para construir imágenes personalizadas.  

---

## 2. Parte Práctica: Implementación

### Entorno de Desarrollo
1. Instalar Docker Engine (Linux, WSL2 o Docker Desktop).  
2. Verificar instalación:
```bash
docker --version
docker run hello-world

