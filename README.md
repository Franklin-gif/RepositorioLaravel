# Reporte de Instalación y Configuración - Laravel 9
**Estudiante:** Franklin Bernal  
**Cédula:** 8-1018-522  
**Materia:** Software VII  
**Profesora:** Ing. Irina Fong  

## 1. Descripción del Proyecto
Este proyecto consiste en la instalación base de Laravel 9 utilizando un servidor local WAMP para la gestión de una base de datos MySQL, enfocado en cumplir con los requisitos de la materia Software VII.

## 2. Bitácora de Errores y Soluciones

Durante el proceso de instalación se presentaron diversos inconvenientes técnicos que fueron resueltos de la siguiente manera:

### A. Restricciones de Seguridad en Composer (PKSA)
**Error:** Al ejecutar `composer update`, el sistema bloqueaba la descarga debido a "security advisories" (avisos de seguridad) en la versión de Laravel 9.
**Solución:** Se utilizó el comando `composer update --no-audit` para omitir la auditoría de seguridad en el entorno de desarrollo local, permitiendo la instalación de las dependencias necesarias.

### B. Conflicto de Acceso a MySQL (Error 1045)
**Error:** phpMyAdmin y Laravel rechazaban la conexión con el mensaje `Access denied for user 'root'@'localhost'`.
**Solución:** Se identificó que el archivo `.env` tenía configurada una contraseña por defecto (`demo`), mientras que el servidor WAMP estaba configurado sin contraseña. Se procedió a limpiar el campo `DB_PASSWORD=` en el archivo de configuración.

### C. Clase "Schema" no encontrada
**Error:** Al intentar realizar las migraciones (`php artisan migrate`), el sistema devolvía un error indicando que la clase `Schema` no existía en el contexto de `AppServiceProvider`.
**Solución:** Se añadió manualmente la fachada de soporte en la cabecera del archivo `AppServiceProvider.php`:
`use Illuminate\Support\Facades\Schema;` 
Y se definió `Schema::defaultStringLength(191);` para evitar errores de longitud de llave en versiones antiguas de MySQL.

### D. Ejecución de Activos (Vite)
**Error:** El comando `npm run dev` fallaba porque las dependencias de Node.js no estaban instaladas.
**Solución:** Se ejecutó `npm install` para descargar los módulos de Node y posteriormente se levantó el servidor de activos con `npm run dev`.

## 3. Comandos Principales Utilizados
- **Instalación de dependencias:** `composer update --no-audit`
- **Generación de llave de seguridad:** `php artisan key:generate`
- **Ejecución de migraciones:** `php artisan migrate`
- **Servidor de desarrollo:** `php artisan serve`
- **Compilación de frontend:** `npm run dev`

## 4. Resultado Final
Se logró establecer la conexión exitosa con la base de datos `laravel` en phpMyAdmin, la creación de las tablas de sistema (`users`, `migrations`, `password_resets`) y la visualización de la pantalla de bienvenida de la aplicación.