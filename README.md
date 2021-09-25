# multiple-select

Fazendo multiplo select com a busca

1 -Fazer a importação do font awesome icons


<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

✍🏻 Descrição
<hr>
Esse projeto foi desenvolvido com as seguintes 
Aplicação multi login, com perfis diferentes, parametrizado para 3 perfis: Administrador, Contratante, Financeiro.
<br>
<br>

# Table of contents

1. [Introduction](#introduction)
2. [Some paragraph](#paragraph1)
    1. [Sub paragraph](#subparagraph1)
3. [Another paragraph](#paragraph2)

## This is the introduction <a name="introduction"></a>
Some introduction text, formatted in heading 2 style

## Some paragraph <a name="paragraph1"></a>
The first paragraph text

### Sub paragraph <a name="subparagraph1"></a>
This is a sub paragraph, formatted in heading 3 style

## Another paragraph <a name="paragraph2"></a>
The second paragraph text


## Example
## Example2
## Third Example
## [Fourth Example](http://www.fourthexample.com) 

🧪 Tecnologias
<hr>
<ul>
    <li>Laravel: 8.61</li>
    <li>PHP: 7.3</li>
    <li>MySql</li>
    <li>Fortify</li>
    <li>JetStream</li>
    <li>LiveWire</li>
    <li>BootStrap</li>
</ul>
 🚀 Como executar
<hr>

```
- composer install
- mude .env.example para .env na pasta raiz.
- Abra o arquivo .env e altere o nome do banco de dados (DB_DATABASE) para o que tiver, o nome de usuário (DB_USERNAME) e a senha (DB_PASSWORD) correspondem à sua configuração.
- Por padrão, o nome de usuário é root e você pode deixar o campo da senha em branco. (Isto é para Xampp)
- Por padrão, o nome de usuário é root e a senha também é root. (Isto é para Xampp)
- Execute php artisan key:generate
- Execute php artisan migrate
- Execute php artisan serve
- Irá abrir no localhost:8000
```

💻 Como fazer ?
1 - Cria uma tabela migration perfil (role)
2 - Alterar a migration Users inserindo a coluna de perfil_id (role) - foreign key
3 - Em App\Fortify\CreateNewUser, acrescentar os campos a mais do registro
```         
return User::create([
            'name' => $input['name'],
            'cpf' => $input['cpf'],
            'email' => $input['email'],
            'password' => Hash::make($input['password']),
            'role_id' => $input['role_id'],
        ]); 
```
4 - Criado os controllers separadados em cada pasta, exemplo: App\Http\Controllers\Admin
``` 
php artisan make:controller Admin/HomeController
php artisan make:controller Contratante/HomeController
php artisan make:controller Financeiro/HomeController
```

5 - Criando a middleware 
```
php artisan make:middleware CheckRole
``` 

6 - Configurando a rota-> routes\web.php
```
Route::group(['middleware' => 'auth'], function() {
    Route::group(['middleware' => 'role:contratante'], function() {
        Route::get('/contratante/home', 'Contratante\HomeController@index')->name('contratante.home');
    });
    
    Route::group(['middleware' => 'role:admin'], function() {
        Route::get('/admin/home', 'Admin\HomeController@index')->name('admin.home');
    });
    Route::group(['middleware' => 'role:financeiro'], function() {
        Route::get('/financeiro/home', 'Financeiro\HomeController@index')->name('financeiro.home');
    });
});
```

7 - Configurando a middleware, em: App\Http\Middleware\CheckRole.php, com o código abaixo:
```
 public function handle(Request $request, Closure $next, string $role)
    {
        if ($role == 'admin' && auth()->user()->role_id != 1) {
            // abort(403);
            Auth::logout();
            return redirect()->route('login')
            ->withInput()
            ->with('erro','Página acessada somente por administrador');
        }

        if ($role == 'contratante' && auth()->user()->role_id != 2) {
            // abort(403);
            Auth::logout();
            return redirect()->route('login')
            ->withInput()
            ->with('erro','Página acessada somente por contratante');
        }

        if ($role == 'financeiro' && auth()->user()->role_id != 3) {
            // abort(403);
            Auth::logout();
            return redirect()->route('login')
            ->withInput()
            ->with('erro','Página acessada somente pelo financeiro');
        }

        return $next($request);
    }
```    

8 - Adicionar a middleware em Kernel.php App\Http\Kernel.php, embaixo de protected $routeMiddleware 

    ```  
    'role' => \App\Http\Middleware\CheckRole::class,
    ``` 
