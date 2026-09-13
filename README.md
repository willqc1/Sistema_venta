# Sistema_venta
Este sera un sistema de ventas desarrollado en django

## Tutorial para iniciar la base de datos MySQL

Este proyecto usa MySQL como base de datos. Sigue estos pasos para dejarla funcionando.

### 1) Verificar si MySQL está instalado

```bash
which mysql
mysql --version
```

Si devuelve la versión, el cliente está instalado.

### 2) Iniciar el servicio de MySQL

En este entorno, usa `service` porque `systemctl` no está disponible dentro del contenedor:

```bash
sudo service mysql start
```

### 3) Verificar que esté escuchando en el puerto 3306

```bash
sudo ss -tulpn | grep 3306
```

Si aparece algo como `127.0.0.1:3306`, significa que MySQL ya está corriendo.

### 4) Entrar a MySQL

```bash
sudo mysql
```

### 5) Crear la base de datos

```sql
CREATE DATABASE tienda CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
SHOW DATABASES;
```

### 6) Crear un usuario para la app (opcional pero recomendado)

```sql
CREATE USER 'tienda_user'@'localhost' IDENTIFIED BY 'tu_password';
GRANT ALL PRIVILEGES ON tienda.* TO 'tienda_user'@'localhost';
FLUSH PRIVILEGES;
```

### 7) Configurar Django para usar MySQL

En `settings.py` agrega algo como esto:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'tienda',
        'USER': 'tienda_user',
        'PASSWORD': '123',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```

### 8) Aplicar migraciones

```bash
python manage.py migrate
```

### 9) Ejecutar el proyecto

```bash
python manage.py runserver
```

## Archivo SQL de creación

El archivo `CREATE DATABASE tienda CHARACTER SET utf.sql` es un script que ejecuta el comando:

```sql
CREATE DATABASE tienda CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

No es la base de datos en sí; es solo un archivo para crearla.

## Si aparece error de conexión

Revisa lo siguiente:

- MySQL está arrancado
- El puerto es `3306`
- El usuario y contraseña son correctos
- La base de datos `tienda` existe
- La configuración de Django apunta a `127.0.0.1:3306`

Si MySQL no responde, vuelve a ejecutar:

```bash
sudo service mysql start
```
