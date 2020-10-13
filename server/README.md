## Graphql

### \- Executando o projeto

Baixar as dependências:
> npm i

Executar via:
> npm run dev

### \- Libraries

* Apollo Server (Node) - yarn add apollo-server
    * Apollo Client (React) 
* Graphql - yarn add graphql
* Nodemon - yarn add nodemon -D
* Sucrase - yarn add sucrase -D
* Dotenv - yarn add dotenv
* Mongoose - yarn add mongoose
* Graphql-iso-date - yarn add graphql-iso-date

### \- Introduction

Não é recomendável seguir o approach de schema first pois o mesmo não é escalável uma vez que a aplicação tende a crescer ao longo do tempo. Exemplo de schema first:

```js
const { ApolloServer, gql } = require('apollo-server');

// The GraphQL schema
const typeDefs = gql`
  type Query {
    "A simple type for getting started!"
    hello: String
  }
`;

// A map of functions which return data for the schema.
const resolvers = {
  Query: {
    hello: () => 'world',
  },
};

const server = new ApolloServer({
  typeDefs,
  resolvers,
});

server.listen().then(({ url }) => {
  console.log(`🚀 Server ready at ${url}`);
});
```

O modelo ideal no caso é o code first.

### \- Query & Mutation

Para realizar uma consulta, acessar o Playground do GraphQL (http://localhost:4000/) e executar a seguinte query:

```json
query {
  comments {
    id
    name
    createdAt
    updatedAt
  }
}
```

Para realizar uma inserção (Mutation) a sintaxe é a seguinte:

```json
mutation {
  saveComment(
    input: {
      name: "Eduardo Pacheco"
      content: "Novo comentário"
  }
  ){
    id
    name
    content
    createdAt
    updatedAt
  }
}
```

Onde a primeira parte são as informações que serão salvas e a segunda parte são os dados que serão retornados após a persistência no Mongo.

Caso queiramos que após salvar apenas o nome e o conteúdo seja retornado, basta remover os demais campos.