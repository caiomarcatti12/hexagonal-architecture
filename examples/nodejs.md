# Como usar a arquitetura hexagonal em nodejs

Aqui está um exemplo hipotético de como uma aplicação Node.js poderia ser projetada usando a arquitetura hexagonal:

```
// Núcleo da aplicação

class AppCore {
  constructor(userRepository) {
    this.userRepository = userRepository;
  }

  async createUser(name, email) {
    // Validação e lógica de negócio aqui

    const user = new User(name, email);
    await this.userRepository.save(user);
  }
}

// Port

class UserRepository {
  async save(user) {
    // Salva o usuário em algum lugar
  }
}

// Adapter

class DatabaseUserRepository extends UserRepository {
  constructor(database) {
    super();
    this.database = database;
  }

  async save(user) {
    // Salva o usuário no banco de dados usando o objeto database
  }
}
```

Neste exemplo, o núcleo da aplicação é a classe AppCore, que possui uma lógica de negócio para criar um usuário e salvar esse usuário em algum lugar. A classe UserRepository representa o port através do qual a aplicação pode salvar usuários em algum lugar, e a classe DatabaseUserRepository é um adapter que estende essa classe e salva os usuários em um banco de dados usando uma instância da classe Database.

Isso significa que, se quisermos mudar a maneira como a aplicação salva os usuários (por exemplo, mudando de um banco de dados para um sistema de arquivos), basta escrever uma nova classe que estenda UserRepository e fornecer uma instância dessa nova classe para o construtor da classe AppCore. A lógica de negócio principal da aplicação não precisa ser alterada.