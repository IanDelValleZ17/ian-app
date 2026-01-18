#  *Medical-appointment-app*  
**IAN IKER DEL VALLE ZARATE**


##  Objetivo de la actividad

Configurar correctamente el entorno de desarrollo, creando un repositorio individual en GitHub e implementando un tablero de gestión en **GitHub Projects**, el cual será utilizado durante todo el cuatrimestre para el desarrollo del proyecto.





## ADA 2. Ajustes globales en configuración del proyecto
## Objetivo general

Dejar tu proyecto Laravel listo para seguir desarrollando:
-configuración base correcta (idioma, zona horaria, MySQL y foto de perfil) y
-estructura inicial de panel administrativo con layout Blade + Flowbite, usando includes y slot.



## qué configuraste (idioma/timezone/MySQL/foto)?

Para configurar "idioma" primeramente tuve que abrir mi terminal para usar los siguientes comandos: 
"composer require laravel-lang/common" después de que se descargaran, usé el último comando "php artisan lang:add es" y se creó una carpeta llamada /lang y dentro de ella se descargó el contenido de /es

Para configurar "timezone" primero tuve que entrar a la carpeta /config/app.php , una vez ahí tuve que cambiar los parametros de " 'timezone' => 'America/Merida' " antes aparecía como  " 'timezone' => 'utc' 
". 
Para MySQL usé XAMPP en dondé activé los modulos de APACHE, MySQL y di click en admin de MySQL para ser dirigido a la página de phpMyAdmin, una vez dentró creé la base de datos "appointment_db", después de eso abrí mi archivo .env y ahí edité "DB_CONNECTION" ,"DB_HOST" , etc. Una vez editado y terminado eso hice las migraciones con  "php artisan migrate" y se crearon 10 tablas.

Para la foto tuve que entrar a /config/jetstram y activé "'features'
         Features::profilePhotos()" 
Después entré a .env y cambié el siguiente parametro "FILESYSTEM_DISK=public" para poder almacenar las fotos en /storage/app/public/profile-photos.


## cómo verificaste cada cosa?
idioma:para este simplemente al inicar sesión antes aparecía en inglés, y ahora está en español además de que se creó las carpetas ya mencionadas en la pregunta anterior.

timezone: para el timezone puse primero Cdmx, pero me lo marcó como error entonces tuve que poner Merida y así me lo aceptó, además de que en unas clases más adelante se debe de ver reflejado en nuestra db

MySQL: XAMPP para configurar todo, hago mención a la pregunta anterior ya que ahí expliqué como hice el procedimiento para que funcionara, además de eso al dar click en users ya aparece registrado el correo con el que me registré en mi app.

foto: al entrar en la carpeta de /storage/app/public/profile-photos se ve la foto que agregué a mi perfil.


## pasos para crear el layout admin, integrar Flowbite y probar includes/slot?

Primeramente se creó dentro de /routes el archivo admin.php y se agregó:
<?php

use Illuminate\Support\Facades\Route;

Route::get('/',function(){
    return "Hola desde admin";
}); 

después de eso en app.php se agregó esta linea 

use Illuminate\Support\Facades\Route; 

y después de eso se agregó nuevas rutas personalizadas 

//nueva rutas personalizadas
        then: function(){
            Route::middleware('web', 'auth')
        ->prefix('admin')
        ->name('admin.')
        ->group(base_path('routes/admin.php'));
        }  

Se modificó fortify.php 

 'home' => '/'

 para que al entrar a /admin nos pida autentificación 

 y por último en web.php

 
Route::redirect('/','/admin'); para que al iniciar sesión ya no seamos redirigidos a dashboard o "welcome" , si no que, en automático a admin.

