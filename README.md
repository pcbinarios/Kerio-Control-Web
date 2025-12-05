# Kerio-Control-Web
# Kerio Control Dashboard

Sistema completo de gestión y monitoreo para Kerio Control con análisis avanzado de logs.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![PHP](https://img.shields.io/badge/PHP-7.4%2B-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## 📋 Características Principales

- ✅ **Dashboard Interactivo** - Vista general del sistema en tiempo real
- 🔥 **Gestión de Firewall** - Control de reglas de firewall
- 👥 **Gestión de Usuarios** - Monitor de usuarios y conexiones activas
- 📊 **Estadísticas de Tráfico** - Gráficos y análisis de ancho de banda
- 📝 **Análisis Avanzado de Logs** - Búsqueda, filtrado y exportación de logs
- 🔐 **Sistema Multi-Usuario** - Autenticación segura para múltiples usuarios
- 📈 **Gráficos en Tiempo Real** - Visualización de datos con Chart.js
- 💾 **Exportación de Datos** - CSV, JSON y TXT
- 🎨 **Interfaz Moderna** - Bootstrap 5 con diseño responsive

## 🗂️ Estructura del Proyecto

```
kerio-dashboard/
├── config/
│   ├── config.php              # Configuración principal
│   └── database.sql            # Estructura de base de datos
├── src/                        # API de Kerio (tus archivos)
│   ├── KerioControlApi.php
│   ├── KerioConnectApi.php
│   └── class/
│       ├── KerioApi.php
│       ├── KerioApiSocket.php
│       └── KerioApiException.php
├── core/                       # Clases principales
│   ├── Database.php
│   ├── Session.php
│   └── KerioManager.php
├── modules/                    # Módulos de la aplicación
│   ├── dashboard/
│   ├── firewall/
│   ├── users/
│   ├── statistics/
│   ├── logs/
│   └── traffic/
├── assets/                     # Recursos estáticos
│   ├── css/
│   │   ├── style.css
│   │   └── login.css
│   ├── js/
│   │   └── main.js
│   └── img/
├── api/                        # Endpoints AJAX
├── includes/                   # Plantillas
│   ├── header.php
│   ├── footer.php
│   └── sidebar.php
├── logs/                       # Logs de la aplicación
├── index.php                   # Punto de entrada
├── login.php                   # Página de login
├── logout.php                  # Cerrar sesión
├── .htaccess                   # Configuración Apache
└── README.md                   # Este archivo
```

## 🚀 Requisitos del Sistema

### Software Requerido

- **PHP**: 7.4 o superior
- **Servidor Web**: Apache 2.4+ (con mod_rewrite)
- **Base de Datos**: MariaDB 10.3+ o MySQL 5.7+
- **Kerio Control**: Versión 9.0 o superior

### Extensiones PHP Requeridas

- `mysqli` o `pdo_mysql`
- `json`
- `openssl`
- `curl`
- `session`

### Verificar Requisitos

```bash
php -v                    # Verificar versión de PHP
php -m | grep mysqli      # Verificar extensión mysqli
php -m | grep openssl     # Verificar extensión openssl
```

## 📥 Instalación

### Paso 1: Descargar el Proyecto

```bash
# Opción 1: Clonar repositorio (si aplica)
git clone https://github.com/tu-usuario/kerio-dashboard.git

# Opción 2: Descargar y extraer ZIP
# Colocar en: C:\UniServer\www\kerio-dashboard\
```

### Paso 2: Copiar Archivos de la API de Kerio

Copia tus archivos de la API de Kerio en el directorio `src/`:

```
kerio-dashboard/src/
├── KerioControlApi.php
├── KerioConnectApi.php
├── KerioDirectoryApi.php
├── KerioOperatorApi.php
├── KerioWorkspaceApi.php
├── SamepageApi.php
└── class/
    ├── KerioApi.php
    ├── KerioApiException.php
    ├── KerioApiInterface.php
    ├── KerioApiSocket.php
    └── KerioApiSocketInterface.php
```

### Paso 3: Configurar la Base de Datos

1. **Crear la base de datos**:

```sql
CREATE DATABASE kerio_dashboard CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

2. **Importar el schema**:

```bash
# Desde línea de comandos
mysql -u root -p kerio_dashboard < config/database.sql

# O desde phpMyAdmin
# Importar archivo: config/database.sql
```

3. **Verificar la creación**:

```sql
USE kerio_dashboard;
SHOW TABLES;
```

Deberías ver las siguientes tablas:
- `app_users`
- `kerio_sessions`
- `activity_logs`
- `kerio_logs_cache`
- `firewall_rules_cache`
- `traffic_statistics`
- `app_settings`
- `notifications`
- `saved_filters`

### Paso 4: Configurar la Aplicación

Edita el archivo `config/config.php`:

```php
// Configuración de Base de Datos
define('DB_HOST', 'localhost');
define('DB_NAME', 'kerio_dashboard');
define('DB_USER', 'root');
define('DB_PASS', '');           // Tu contraseña de MySQL
define('DB_PORT', 3306);

// Configuración de la Aplicación
define('APP_NAME', 'Kerio Control Dashboard');
define('APP_AUTHOR', 'Tu Nombre');
define('TIMEZONE', 'America/Mexico_City');  // Tu zona horaria

// Configuración de Kerio API
define('KERIO_DEFAULT_PORT', 4081);
define('KERIO_API_TIMEOUT', 30);

// Debug (cambiar a false en producción)
define('ENABLE_DEBUG', true);
```

### Paso 5: Configurar Apache

El archivo `.htaccess` ya está incluido con la configuración necesaria:

```apache
RewriteEngine On

# Proteger archivos sensibles
<FilesMatch "^\.">
    Order Allow,Deny
    Deny from all
</FilesMatch>

# Prevenir listado de directorios
Options -Indexes
```

### Paso 6: Permisos de Archivos

En Windows con UniServer, normalmente no necesitas ajustar permisos, pero asegúrate de que:

- El directorio `logs/` sea escribible
- El directorio `config/` sea accesible

En Linux/Unix:

```bash
chmod 755 kerio-dashboard/
chmod 777 kerio-dashboard/logs/
chmod 644 kerio-dashboard/config/config.php
```

## 🔐 Primer Acceso

### Credenciales por Defecto

```
Usuario: admin
Contraseña: admin123
```

**⚠️ IMPORTANTE**: Cambia esta contraseña después del primer login.

### Proceso de Login

1. Accede a: `http://localhost/kerio-dashboard/login.php`
2. Ingresa las credenciales de la aplicación (admin/admin123)
3. Ingresa los datos de tu servidor Kerio Control:
   - **Host/IP**: IP o hostname de tu servidor Kerio
   - **Puerto**: 4081 (por defecto)
   - **Usuario Kerio**: Usuario administrador de Kerio
   - **Contraseña Kerio**: Contraseña del administrador

## 📖 Uso de los Módulos

### Dashboard

Vista general del sistema con:
- Estado del servidor
- Usuarios activos
- Uso de CPU y memoria
- Gráficos de tráfico en tiempo real
- Información del sistema

### Firewall

Gestión de reglas de firewall:
- Ver todas las reglas
- Habilitar/Deshabilitar reglas
- Filtrar por estado
- Ver detalles de cada regla

### Usuarios

Gestión de usuarios y conexiones:
- Ver usuarios conectados
- Desconectar usuarios
- Ver estadísticas de tráfico por usuario
- Lista completa de usuarios del sistema

### Análisis de Logs

Módulo completo para análisis de logs:

**Tipos de Logs Disponibles:**
- `alert.log` - Alertas del sistema
- `config.log` - Cambios de configuración
- `connection.log` - Conexiones de red
- `debug.log` - Información de depuración
- `dial.log` - Conexiones dial-up
- `error.log` - Errores del sistema
- `filter.log` - Filtrado de contenido
- `host.log` - Información de hosts
- `http.log` - Tráfico HTTP/HTTPS
- `security.log` - Eventos de seguridad
- `warning.log` - Advertencias
- `web.log` - Actividad web

**Funcionalidades:**
- Búsqueda por palabra clave
- Filtrado por tipo de log
- Filtrado por severidad
- Filtrado por rango de fechas
- Estadísticas automáticas
- Análisis de patrones (Top IPs, Top usuarios)
- Exportación en CSV, JSON y TXT
- Gráficos de distribución

**Ejemplo de Búsqueda:**

1. Selecciona tipos de logs (ej: security, error)
2. Selecciona severidad (ej: ERROR, CRITICAL)
3. Ingresa palabra clave (ej: "failed login")
4. Define rango de fechas
5. Click en "Buscar Logs"
6. Analiza resultados y exporta si es necesario

## 🛠️ Configuración Avanzada

### Cambiar Puerto de Kerio

Si tu Kerio Control usa un puerto diferente:

```php
// En config/config.php
define('KERIO_DEFAULT_PORT', 4081);  // Cambiar aquí
```

### Ajustar Timeout de Conexión

```php
// En config/config.php
define('KERIO_API_TIMEOUT', 30);  // Segundos
```

### Configurar Auto-Refresh

```php
// En config/config.php
define('REFRESH_INTERVAL', 60);  // Segundos
```

### Configurar Retención de Logs

```php
// En config/config.php
define('LOGS_RETENTION_DAYS', 30);  // Días
```

O desde la base de datos:

```sql
UPDATE app_settings 
SET setting_value = '30' 
WHERE setting_key = 'logs_retention_days';
```

## 👥 Gestión de Usuarios de la Aplicación

### Crear Nuevo Usuario

```sql
INSERT INTO app_users (username, password, email, full_name, is_active, is_admin) 
VALUES (
    'nuevo_usuario',
    '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',  -- admin123
    'usuario@example.com',
    'Nombre Completo',
    1,
    0
);
```

### Cambiar Contraseña

Desde PHP:

```php
$password = 'nueva_contraseña';
$hash = password_hash($password, PASSWORD_DEFAULT);
// Actualizar en la BD
```

O generar hash online en: https://www.bcrypt-generator.com/

## 🔧 Solución de Problemas

### Error: "Cannot connect to database"

**Causa**: Credenciales incorrectas de MySQL

**Solución**:
1. Verifica `config/config.php`
2. Verifica que MySQL esté corriendo
3. Verifica que la base de datos exista

```bash
# En UniServer
mysql -u root -p
> SHOW DATABASES;
> USE kerio_dashboard;
```

### Error: "Cannot connect to Kerio Control"

**Causa**: Servidor Kerio inaccesible o credenciales incorrectas

**Solución**:
1. Verifica que Kerio Control esté corriendo
2. Verifica el puerto (4081 por defecto)
3. Verifica usuario y contraseña de Kerio
4. Verifica firewall del servidor Kerio

```bash
# Probar conexión desde línea de comandos
telnet kerio-server 4081
```

### Error: "Session timeout"

**Causa**: Sesión expirada

**Solución**:
- Simplemente vuelve a iniciar sesión
- Ajusta el timeout en `config/config.php`:

```php
define('SESSION_TIMEOUT', 7200);  // 2 horas
```

### Error: "Permission denied" en logs

**Causa**: Directorio logs/ no escribible

**Solución**:

```bash
# Linux/Unix
chmod 777 logs/

# Windows
# Click derecho > Propiedades > Seguridad > Editar permisos
```

### Los logs no se muestran

**Causa**: Ruta de logs incorrecta o permisos

**Solución**:
1. Verifica que la ruta `/var/winroute/logs/` sea correcta en tu servidor Kerio
2. Si es diferente, ajusta en `core/KerioManager.php`:

```php
const LOG_PATH = '/tu/ruta/logs/';
```

## 📊 Mantenimiento

### Limpiar Logs Antiguos

Ejecuta periódicamente (se puede programar):

```sql
-- Limpiar logs más antiguos de 30 días
CALL clean_old_logs(30);
```

### Limpiar Sesiones Expiradas

```sql
CALL clean_expired_sessions();
```

### Backup de Base de Datos

```bash
# Hacer backup
mysqldump -u root -p kerio_dashboard > backup_$(date +%Y%m%d).sql

# Restaurar backup
mysql -u root -p kerio_dashboard < backup_20240101.sql
```

## 🔒 Seguridad

### Recomendaciones

1. **Cambiar contraseña por defecto** inmediatamente
2. **Usar HTTPS** en producción
3. **Deshabilitar debug** en producción:
   ```php
   define('ENABLE_DEBUG', false);
   ```
4. **Configurar firewall** para proteger el puerto 4081
5. **Actualizar regularmente** PHP y dependencias
6. **Revisar logs** de actividad periódicamente

### Habilitar HTTPS

En `.htaccess`:

```apache
# Descomentar estas líneas
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

## 📝 Notas Importantes

- Los logs se leen desde `/var/winroute/logs/` del servidor Kerio Control
- La aplicación no modifica los logs originales
- Los datos se cachean en la base de datos para análisis histórico
- Se recomienda ejecutar limpieza periódica de logs antiguos
- El sistema soporta hasta 3+ usuarios simultáneos según diseño

## 🤝 Soporte y Contribuciones

Para reportar bugs o sugerir mejoras:
- Crea un issue en el repositorio
- Contacta al desarrollador

## 📄 Licencia

Este proyecto está bajo las Licencias MIT y GNU

## ✨ Créditos

- **Desarrollado por**: PCbinariOS
- **API de Kerio**: Kerio Technologies s.r.o.
- **Framework CSS**: Bootstrap 5
- **Gráficos**: Chart.js
- **Iconos**: Font Awesome

---

**Versión**: 1.0.0  
**Fecha**: Diciembre 2025  
**Compatible con**: Kerio Control 9.0+
