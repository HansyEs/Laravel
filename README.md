# Laravel
### Where por multiples columnas
        User::where('name', $name)->where('email', $email)->first(); 
        User::whereNameAndEmail($name, $email)->first(); // Da lo mismo
        User::whereNameOrEmail($name, $email)->first(); // También funciona con un or
        // También para el where admite un array si queremos
        User::where(['name' => $name, 'email' => $email ])->first();
### Find múltiple
        $users = User::find([1, 5, 7]); // Devuelve una coleción
        $users->modelKeys(); // Devuelve los IDs de la colección en un array [1, 5, 7]
### Carga mejorada en una relación ya cargada su coleción, en lugar de pedir los elementos por cada uno hace una sola select para traerlos todos
        $users = User->get();
        $users->load(['relacion1', 'relacion2', ...]);
        Es como un relacion1::whereIn('user_id', $users->modelKeys())->get() y luego "repartirlos" dentro de cada user
### Eventos que puede llevar un modelo de manera sencilla.
        Estos son los eventos que se pueden usar en laravel 9 
            creating: Call Before Create Record.
            created: Call After Created Record.
            updating: Call Before Update Record
            updated: Class After Updated Record
            deleting: Call Before Delete Record.
            deleted: Call After Deleted Record
            retrieved: Call Retrieve Data from Database.
            saving: Call Before Creating or Updating Record.
            saved: Call After Created or Updated Record.
            restoring: Call Before Restore Record.
            restored: Call After Restore Record.
            replicating: Call on replicate Record
        Se usan creando una función estática dentro de la clase del modelo
            clase Test extends Model
            {
                static::created(function($item) {           
                    Log::info('Este evento se lanza tras crear un elemento en el modelo'); 
                });
            }
        Es más practico y organizado utilizar un observer mediante
            php artisan make:observer UserObserver --model=User
