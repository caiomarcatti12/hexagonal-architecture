# Como usar a arquitetura hexagonal em bibliotecas externas

Aqui está um exemplo hipotético de como uma biblioteca externa poderia ser encapsulada em uma aplicação usando a arquitetura hexagonal:

```
// Núcleo da aplicação

class AppCore {
  constructor(mailer) {
    this.mailer = mailer;
  }

  async sendEmail(to, subject, body) {
    // Validação e lógica de negócio aqui

    await this.mailer.send(to, subject, body);
  }
}

// Port

class Mailer {
  async send(to, subject, body) {
    // Envia um e-mail
  }
}

// Adapter
class ExternalMailerAdapter extends Mailer {
  constructor(externalMailer) {
    super();
    this.externalMailer = externalMailer;
  }

  async send(to, subject, body) {
    // Usa a biblioteca externa para enviar o e-mail
    await this.externalMailer.send(to, subject, body);
  }
}
```

Neste exemplo, o núcleo da aplicação é a classe AppCore, que possui uma lógica de negócio para enviar um e-mail. A classe Mailer representa o port através do qual a aplicação pode enviar e-mails, e a classe ExternalMailerAdapter é um adapter que estende essa classe e usa uma biblioteca externa para enviar os e-mails de fato.

Isso significa que, se quisermos mudar a maneira como a aplicação envia e-mails (por exemplo, mudando de uma biblioteca externa para um serviço de e-mail na nuvem), basta escrever uma nova classe que estenda Mailer e fornecer uma instância dessa nova classe para o construtor da classe AppCore. A lógica de negócio principal da aplicação não precisa ser alterada.