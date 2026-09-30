# CRM "Gestión Integral de Negocios" — ALP-365

Taller Semana 9 — SQL, Query Builder y Reportes del CRM.
I.U.J.O. Extensión Barquisimeto — Docente: Ing. José Daniel Cadenas L.

Este repositorio contiene el código del taller **hasta el Paso 4.2**:
migraciones, modelos, seeder con datos de prueba, controlador de reportes,
vistas Blade y rutas.

## Estructura

```
app/Http/Controllers/ReportController.php   ← Reportes (Pasos 3.1 y 4.1)
app/Models/Client.php                        ← Modelo (Paso 0.9)
database/migrations/                         ← 4 migraciones (Pasos 0.5–0.8)
database/seeders/CrmDemoSeeder.php            ← Datos de prueba (Paso 1.2)
resources/views/reports/zonas.blade.php      ← Vista reporte 1 (Paso 3.2)
resources/views/reports/interacciones.blade.php ← Vista reporte 2 (Paso 4.2)
routes/web.php                               ← Rutas /reportes/* (Fase 2)
```

## Cómo ponerlo a correr

> Requiere PHP 8.2+, Composer y MySQL (XAMPP sirve).

```bash
# 1. Crear el proyecto Laravel 12 (Paso 0.1)
cd C:\xampp\htdocs
composer create-project laravel/laravel crm-gestion-integral "12.*"
cd crm-gestion-integral

# 2. Copiar los archivos de este repo sobre el proyecto
#    (app/, database/, resources/, routes/)

# 3. Crear la base de datos en phpMyAdmin (Paso 0.2)
#    Nombre: crm_gestion_integral — Cotejamiento: utf8mb4_unicode_ci

# 4. Configurar .env (Paso 0.3)
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crm_gestion_integral
DB_USERNAME=root
DB_PASSWORD=

# 5. Migrar y poblar (Pasos 0.4 y 1.1)
php artisan migrate
php artisan db:seed --class=CrmDemoSeeder

# 6. Servir y abrir los reportes
php artisan serve
# http://127.0.0.1:8000/reportes/zonas
# http://127.0.0.1:8000/reportes/interacciones
```

## Reportes

| Ruta | Reporte | Técnica clave |
|---|---|---|
| `/reportes/zonas` | Clientes por zona geográfica | `GROUP BY` + `COUNT(*)` + `map()` para porcentajes |
| `/reportes/interacciones` | Interacciones por asesor | `LEFT JOIN` doble + `COUNT(CASE WHEN...)` por tipo |
