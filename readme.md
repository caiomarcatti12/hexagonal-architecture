# Arquitetura hexagonal

Arquitetura hexagonal, também conhecida como arquitetura de ports e adapters, é uma abordagem para projetar a arquitetura de software de uma aplicação de maneira que seja fácil de mudar a maneira como a aplicação interage com diferentes sistemas externos, sem afetar a lógica da aplicação em si.

Na arquitetura hexagonal, a aplicação é dividida em três partes principais:

- O núcleo da aplicação, que é o coração da aplicação e contém a lógica de negócio principal.

- Os ports, que são interfaces que representam os pontos de conexão da aplicação com o mundo exterior. Eles podem ser usados para interagir com sistemas externos, como bancos de dados ou sistemas de mensagens, ou para expor a aplicação como uma API para outras aplicações.

- Os adapters, que são implementações dos ports que permitem que a aplicação interaja com os sistemas externos de fato.

A ideia principal da arquitetura hexagonal é que a lógica de negócio principal da aplicação fique isolada dos detalhes de implementação das interações com os sistemas externos, o que torna mais fácil mudar essas interações sem afetar o núcleo da aplicação. Isso também torna mais fácil testar a aplicação, já que os testes podem ser escritos usando os ports em vez de depender de sistemas externos reais.


# Exemplos
- [PHP](examples/php.md)
- [NodeJS](examples/nodejs.md)
- [Bibliotecas externas](examples/library.md)