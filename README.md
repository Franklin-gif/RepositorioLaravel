# Reporte de Instalación y Configuración - Laravel 9
**Estudiante:** Franklin Bernal  
**Cédula:** 8-1018-522  
**Materia:** Software VII  
**Profesora:** Ing. Irina Fong  

---

## 📝 Descripción del Proyecto
Este proyecto consiste en la instalación base de **Laravel 9** utilizando un servidor local **WAMP** para la gestión de una base de datos MySQL, enfocado en cumplir con los requisitos académicos de la materia Software VII.

---

## 🛠️ Bitácora de Errores y Soluciones

> [!IMPORTANT]
> Los siguientes puntos detallan los obstáculos técnicos encontrados y cómo se superaron para lograr un entorno estable.

### 1. Restricciones de Seguridad en Composer (PKSA)
**Error:** Al ejecutar `composer update`, el sistema bloqueaba la descarga debido a avisos de seguridad en Laravel 9.

> [!CAUTION]
> **Mensaje de error:** `Your requirements could not be resolved to an installable set of packages... affected by security advisories`.

* **Solución:** Se utilizó el comando `composer update --no-audit` para omitir la auditoría de seguridad en el entorno de desarrollo local.

### 2. Conflicto de Acceso a MySQL (Error 1045)
**Error:** phpMyAdmin y Laravel rechazaban la conexión del usuario root.

> [!WARNING]
> **Causa:** El archivo `.env` tenía una contraseña (`demo`) que no existía en el servidor local WAMP.

* **Solución:** Se editó el archivo `.env` dejando el campo vacío: `DB_PASSWORD=`.

### 3. Clase "Schema" no encontrada
**Error:** Fallo al ejecutar las migraciones iniciales.

> [!TIP]
> **Mejor práctica:** Para asegurar compatibilidad con versiones antiguas de MySQL, siempre es recomendable definir una longitud de cadena por defecto.

* **Solución:** Se añadió la importación en `AppServiceProvider.php`:
    ```php
    use Illuminate\Support\Facades\Schema;
    
    public function boot() {
        Schema::defaultStringLength(191);
    }
    ```

### 4. Ejecución de Activos (Vite)
**Error:** El comando `npm run dev` no era reconocido.

> [!NOTE]
> Esto sucede porque los módulos de Node no se descargan por defecto al clonar o crear un proyecto.

* **Solución:** Ejecución de `npm install` seguido de `npm run dev`.

---

## 🚀 Comandos Principales
A continuación, los comandos esenciales utilizados para estabilizar el proyecto:

| Objetivo | Comando |
| :--- | :--- |
| Instalar dependencias | `composer update --no-audit` |
| Generar llave | `php artisan key:generate` |
| Ejecutar tablas | `php artisan migrate` |
| Levantar servidor | `php artisan serve` |

---

## ✅ Resultado Final
Se logró establecer la conexión exitosa con la base de datos en **phpMyAdmin**, verificando la creación de las tablas de sistema y el acceso al Dashboard de Laravel.