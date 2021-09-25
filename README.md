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
<ul>
    <li>Cria uma tabela migration perfil (role)</li>
    <li>Alterar a migration Users inserindo a coluna de perfil_id (role) - foreign key</li>
    <li>Em App\Fortify\CreateNewUser, acrescentar os campos a mais do registro
        <ul>
            <li>```         return User::create([
            'name' => $input['name'],
            'cpf' => $input['cpf'],
            'email' => $input['email'],
            'password' => Hash::make($input['password']),
            'role_id' => $input['role_id'],
        ]); ```</li>
        </ul>
    </li>
    <li></li>
</ul>



