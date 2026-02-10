Markdown# 🛡️ Manual de Instalación y Configuración: Fail2Ban Fortaleza

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
2. Configuración de la "Cárcel" (jail.local)Para evitar que las actualizaciones del sistema borren nuestra configuración, trabajaremos exclusivamente en jail.local.Paso A: Crear el archivo limpioBash> /etc/fail2ban/jail.local
Paso B: Editar el contenidoBashnano /etc/fail2ban/jail.local
Paso C: Pegar la configuración robustaCopia y pega el siguiente bloque de código:Ini, TOML[DEFAULT]
# --- CONFIGURACIÓN GLOBAL ---
# Tiempo de baneo base: 24 horas
bantime  = 24h
# Ventana de tiempo para detectar ataques: 1 hora
findtime = 1h
# Máximo de intentos fallidos permitidos
maxretry = 3
# Ignorar localhost
ignoreip = 127.0.0.1/8 ::1
# Acción de baneo y reporte por log
action = %(action_mwl)s

# --- CÁRCELES (JAILS) ESPECÍFICAS ---

[sshd]
enabled = true
# Protege puerto estándar y puerto personalizado (ej. 31212)
port    = 22,31212
filter  = sshd
logpath = /var/log/auth.log
maxretry = 3
# CASTIGO: 1 semana de baneo
bantime  = 1w

[vsftpd]
enabled = true
port    = 21
filter  = vsftpd
logpath = /var/log/vsftpd.log
maxretry = 2
# CASTIGO: 2 semanas de baneo
bantime  = 2w

[mysqld-auth]
enabled = true
port    = 3306
filter  = mysqld-auth
logpath = /var/log/mysql/error.log
maxretry = 2
# CASTIGO: 4 semanas (1 mes) de baneo
bantime  = 4w
3. Preparación de Logs y ReinicioAntes de aplicar, debemos asegurar que el log de MySQL exista para evitar errores:Bashmkdir -p /var/log/mysql
touch /var/log/mysql/error.log
chown mysql:adm /var/log/mysql/error.log

# Reiniciar Fail2Ban para aplicar cambios
systemctl restart fail2ban
4. Comandos de AdministraciónAcciónComandoVer estado de las cárcelesfail2ban-client statusVer IPs bloqueadas en SSHfail2ban-client status sshdDesbloquear una IP propiafail2ban-client set sshd unbanip [TU_IP]Monitorear ataques en vivotail -f /var/log/fail2ban.log
