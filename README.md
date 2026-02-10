# 🛡️ Manual de Instalación y Configuración: Fail2Ban Fortaleza

Este manual detalla la instalación y configuración de **Fail2Ban** para proteger un servidor Linux contra ataques de fuerza bruta en SSH, FTP y MySQL.

---

## 1. Instalación
Ejecuta los siguientes comandos como usuario **root**:

```bash
# Actualizar repositorios e instalar
apt update && apt install fail2ban -y

# Asegurar que el servicio inicie automáticamente
systemctl start fail2ban
systemctl enable fail2ban


2. Configuración de la "Cárcel" (jail.local)
Para evitar que las actualizaciones del sistema borren nuestra configuración, trabajaremos exclusivamente en jail.local.

Paso A: Crear el archivo limpio
