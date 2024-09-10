# Como usar a arquitetura hexagonal em php

Aqui está um exemplo hipotético de como uma aplicação PHP poderia ser projetada usando a arquitetura hexagonal:

```
<?php
// Núcleo da aplicação

class AppCore
{
    private $userRepository;

    public function __construct(UserRepository $userRepository)
    {
        $this->userRepository = $userRepository;
    }

    public function createUser(string $name, string $email): void
    {
        // Validação e lógica de negócio aqui

        $user = new User($name, $email);
        $this->userRepository->save($user);
    }
}

// Port

interface UserRepository
{
    public function save(User $user): void;
}

// Adapter

class DatabaseUserRepository implements UserRepository
{
    private $database;

    public function __construct(Database $database)
    {
        $this->database = $database;
    }

    public function save(User $user): void
    {
        // Salva o usuário no banco de dados usando o objeto Database
    }
}
```

Neste exemplo, o núcleo da aplicação é a classe AppCore, que possui uma lógica de negócio para criar um usuário e salvar esse usuário em algum lugar. A interface UserRepository representa o port através do qual a aplicação pode salvar usuários em algum lugar, e a classe DatabaseUserRepository é um adapter que implementa essa interface e salva os usuários em um banco de dados usando uma instância da classe Database.

Isso significa que, se quisermos mudar a maneira como a aplicação salva os usuários (por exemplo, mudando de um banco de dados para um sistema de arquivos), basta escrever uma nova implementação da interface UserRepository e fornecer uma instância dessa nova implementação para o construtor da classe AppCore. A lógica de negócio principal da aplicação não precisa ser alterada.