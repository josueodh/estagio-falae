# Desafio de Processo Seletivo de Estágio - Falaê

Bem-vindo ao desafio técnico para o processo seletivo de estágio no Falaê! Este projeto foi criado para avaliar suas habilidades de desenvolvimento e organização de dados. Siga as instruções abaixo para configurar o ambiente, entender a estrutura do banco de dados e implementar a lógica necessária para resolver o desafio.

## Objetivo

O desafio consiste em implementar uma aplicação para um restaurante que permita:

- Cadastrar produtos no sistema, com informações como nome, preço, descrição e imagem.
- Criar e visualizar pedidos compostos por múltiplos produtos e suas quantidades.
- Gerenciar o relacionamento entre produtos e pedidos, organizando os itens de cada pedido e calculando o total.

## Estrutura do Banco de Dados

O banco de dados está estruturado em quatro modelos principais: **User**, **Product**, **Order**, e **OrderItem**. Veja a descrição de cada modelo abaixo:

### Modelos de Dados

#### User
O modelo **User** representa um cliente no sistema. Cada cliente possui:

- `id`: Identificador único do usuário, gerado automaticamente.
- `name`: Nome do usuário.
- `email`: E-mail para login e contato.
- `address`: Endereço do usuário para entrega.
- `phone`: (Opcional) Telefone do usuário.

#### Product
O modelo **Product** representa um produto disponível no sistema. Cada produto possui:

- `id`: Identificador único do produto, gerado automaticamente.
- `name`: Nome do produto.
- `price`: Preço do produto.
- `category`: Categoria do produto (ex.: "Bebida", "Prato Principal", etc.).
- `description`: (Opcional) Descrição do produto.
- `imageUrl`: (Opcional) URL da imagem do produto.

#### Order
O modelo **Order** representa um pedido feito por um cliente, contendo os produtos selecionados.

- `id`: Identificador único do pedido, gerado automaticamente.
- `userId`: Chave estrangeira que referencia o usuário que realizou o pedido.
- `totalPrice`: Valor total do pedido.
- `status`: Status do pedido (ex.: “Pendente”, “Em Preparo”, “Entregue”).
- `createdAt`: Data e hora em que o pedido foi criado.

#### OrderItem
O modelo **OrderItem** representa o vínculo entre um produto e um pedido, incluindo a quantidade do produto no pedido.

- `id`: Identificador único do item de pedido, gerado automaticamente.
- `quantity`: Quantidade do produto neste item de pedido.
- `orderId`: Chave estrangeira que referencia o pedido.
- `productId`: Chave estrangeira que referencia o produto.


## Requisitos do Desafio

### 1. **Cadastro de Clientes**
   - **Objetivo**: Criar uma funcionalidade para registrar um novo usuário. O sistema deve permitir que informações como nome, email, endereço e telefone sejam enviados e armazenados para cada cliente.
   - **Requisitos**:
     - Criar um endpoint `POST /api/auth/register` que receba os dados do usuário e os salve no banco de dados.
     - Validar os dados do usuário, como email único e formato correto.
     - Implementar uma resposta adequada para sucesso ou falha no cadastro.

### 2. **Cadastro de Produtos**
   - **Objetivo**: Permitir o cadastro de novos produtos no sistema. O usuário deve conseguir adicionar um produto com as informações necessárias, como nome, preço, descrição e URL de imagem.
   - **Requisitos**:
     - Criar um endpoint `POST /api/products` que receba os dados de um novo produto e o adicione ao banco de dados.
     - Validar os dados do produto, como o preço positivo e as informações de imagem válidas.
     - Garantir que o produto seja criado corretamente e retorne uma resposta com o produto cadastrado ou uma mensagem de erro.

### 3. **Visualização de Produtos**
   - **Objetivo**: Permitir a visualização de todos os produtos cadastrados no sistema.
   - **Requisitos**:
     - Criar um endpoint `GET /api/products` que retorne todos os produtos disponíveis, incluindo informações como nome, categoria, preço, descrição e URL da imagem.
     - Implementar a ordenação e filtragem dos produtos, caso necessário, para facilitar a busca do cliente.

### 4. **Exibição de Detalhes de um Produto**
   - **Objetivo**: Permitir a visualização dos detalhes de um produto específico.
   - **Requisitos**:
     - Criar um endpoint `GET /api/products/:id` que retorne informações completas de um produto individual, com base no ID fornecido.
     - Garantir que, caso o produto não seja encontrado, seja retornada uma resposta de erro adequada.

### 5. **Atualização de Produtos**
   - **Objetivo**: Permitir a atualização dos dados de um produto já cadastrado, como nome, preço, categoria, descrição e URL de imagem.
   - **Requisitos**:
     - Criar um endpoint `PUT /api/products/:id` que permita a atualização das informações de um produto específico, utilizando o ID do produto.
     - Validar os dados antes de atualizar e garantir que a resposta retorne o produto atualizado com sucesso ou uma mensagem de erro.

### 6. **Exclusão de Produtos**
   - **Objetivo**: Permitir a exclusão de produtos existentes no sistema.
   - **Requisitos**:
     - Criar um endpoint `DELETE /api/products/:id` que exclua um produto específico com base no ID fornecido.
     - Garantir que, caso o produto não seja encontrado, o sistema retorne um erro indicando que o produto não existe.

### 7. **Criação de Pedidos**
   - **Objetivo**: Permitir a criação de um novo pedido, onde o cliente pode selecionar produtos e definir suas quantidades.
   - **Requisitos**:
     - Criar um endpoint `POST /api/orders` que permita ao cliente criar um pedido, especificando os produtos e suas quantidades.
     - O sistema deve validar se os produtos selecionados estão disponíveis e, em caso afirmativo, calcular o valor total do pedido.
     - Garantir que o pedido seja criado corretamente no banco de dados e que seja retornado um ID de confirmação.

### 8. **Visualização de Pedidos**
   - **Objetivo**: Permitir a visualização dos detalhes de um pedido, incluindo os produtos comprados e o valor total.
   - **Requisitos**:
     - Criar um endpoint `GET /api/orders/:id` que retorne as informações completas de um pedido, incluindo os produtos e suas quantidades.
     - A resposta deve incluir o status do pedido, valor total, e data de criação.
     - Garantir que, se o pedido não for encontrado, o sistema retorne um erro adequado.

### 9. **Cálculo do Total do Pedido**
   - **Objetivo**: Calcular o valor total de um pedido com base nos preços e nas quantidades dos produtos.
   - **Requisitos**:
     - Implementar o cálculo do valor total do pedido ao criar ou visualizar um pedido, multiplicando o preço de cada produto pela quantidade e somando o total.
     - Garantir que o valor total seja atualizado automaticamente quando o pedido for criado ou alterado.


---

## Endpoints da API

### Clientes

- **POST** `/api/auth/register`
  - **Descrição**: Registra um novo usuário.
  - **Body**:
    ```json
    {
      "name": "John Doe",
      "email": "john@example.com",
      "address": "Rua Fictícia, 123",
      "phone": "123456789"
    }
    ```



### Produtos

- **GET** `/api/products`
  - **Descrição**: Retorna todos os produtos cadastrados.
  - **Resposta**:
    ```json
    [
      {
        "id": 1,
        "name": "Pizza Margherita",
        "category": "Prato Principal",
        "price": 25.99,
        "description": "Clássica pizza italiana",
        "imageUrl": "https://example.com/image.jpg"
      },
      {
        "id": 2,
        "name": "Coca-Cola",
        "category": "Bebida",
        "price": 5.99,
        "description": "Refrigerante gelado",
        "imageUrl": "https://example.com/image.jpg"
      }
    ]
    ```

- **POST** `/api/products`
  - **Descrição**: Cria um novo produto.
  - **Body**:
    ```json
    {
      "name": "Pizza Calabresa",
      "category": "Prato Principal",
      "price": 29.99,
      "description": "Pizza com calabresa e cebola",
      "imageUrl": "https://example.com/pizza-calabresa.jpg"
    }
    ```

- **GET** `/api/products/:id`
  - **Descrição**: Retorna um produto específico.
  - **Resposta**:
    ```json
    {
      "id": 1,
      "name": "Pizza Margherita",
      "category": "Prato Principal",
      "price": 25.99,
      "description": "Clássica pizza italiana",
      "imageUrl": "https://example.com/image.jpg"
    }
    ```

- **PUT** `/api/products/:id`
  - **Descrição**: Atualiza as informações de um produto específico.
  - **Body**:
    ```json
    {
      "name": "Pizza Margherita",
      "price": 28.99,
      "category": "Prato Principal",
      "description": "Pizza italiana clássica com tomate e manjericão",
      "imageUrl": "https://example.com/new-image.jpg"
    }
    ```

- **DELETE** `/api/products/:id`
  - **Descrição**: Exclui um produto específico.

### Pedidos


- **POST** `/api/orders`
  - **Descrição**: Cria um novo pedido.
  - **Body**:
    ```json
    {
      "userId": 1,
      "products": [
        {
          "productId": 1,
          "quantity": 2
        },
        {
          "productId": 2,
          "quantity": 1
        }
      ]
    }
    ```

- **GET** `/api/orders/:id`
  - **Descrição**: Retorna um pedido específico, incluindo os produtos e suas quantidades.
  - **Resposta**:
    ```json
    {
      "id": 1,
      "totalPrice": 56.99,
      "status": "Pendente",
      "createdAt": "2024-11-06T12:34:56Z",
      "products": [
        {
          "name": "Pizza Margherita",
          "quantity": 2,
          "price": 25.99
        },
        {
          "name": "Coca-Cola",
          "quantity": 1,
          "price": 5.99
        }
      ]
    }
    ```



## Tecnologias e Ferramentas

Para realizar este desafio, você pode usar as seguintes tecnologias:

- **Backend**: Node.js com Typescript (Express, Fastify)
- **Banco de Dados**: Banco de Dados SQL
- **Frontend**:  React com Typescript ( Vite )

## Dicas
- **CSS** [Tailwind CSS](https://tailwindcss.com/), [Shadcn](https://ui.shadcn.com/)
- **ORM** [TypeORM](https://typeorm.io/), [Prisma ORM](https://www.prisma.io/)

---

## Entregáveis

1. **Código**: Submeta o código em um repositório Git com instruções claras de como configurar e rodar o projeto.
2. **Documentação**: Inclua um README com as instruções de configuração, detalhes de endpoints (se aplicável), e qualquer informação adicional sobre o projeto. (Diferencial)
3. **Extras** (Opcional): Implemente funcionalidades extras como edição e exclusão de produtos e pedidos.


## Link do formulário

[Link do Formulário](https://forms.gle/rkv9wp9yzABVmJ1U6)



Boa sorte e estamos ansiosos para ver o que você desenvolve!
