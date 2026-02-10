🛡️ Guía de Configuración: Fail2Ban (Nivel Fortaleza)

Este manual detalla los pasos para instalar y configurar Fail2Ban, asegurando la protección de accesos críticos como SSH, FTP y MySQL.

---

## 1. Instalación del Servicio
Ejecuta los siguientes comandos como usuario **root** para instalar y habilitar el servicio:

```bash
# Actualizar repositorios e instalar el paquete
apt update && apt install fail2ban -y

# Iniciar y habilitar para que arranque con el sistema
systemctl start fail2ban
systemctl enable fail2banMonitorear ataques en vivotail -f /var/log/fail2ban.log

2. Configuración de Cárceles (jail.local)
Utilizaremos el archivo jail.local para evitar que las actualizaciones del sistema sobrescriban nuestra configuración personalizada.

Paso A: Abrir el editor
Ejecuta este comando para crear o editar el archivo:
