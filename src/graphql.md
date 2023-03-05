# Notes on GraphQL

GraphQL is just a specification.

Topics

- Type Definitions
- Resolvers
- Query Definitions
- Mutation Definitions
- Composition
- Schema

Where does GraphQL fit in?

- A GraphQL server with a connected Database.
- A GraphQL server as a layer in foront of many 3rd party services and connects them all with one GraphQL API.
- A hybrid approach where a GraphQL server has a connected Database and also connections with 3rd party APIs.

Node.js GraphQL Tools

- Servers
  - Apollo server
  - graphql-js
  - GraphQL Yoga
- Services
  - AWS Amplify
- Tools
  - Prisma
  - GraphQL Playground

### Creating Schema

Some ways to create a schema

- Using Schema Definition Language (SDL)
- Programmatically creating a Schema using language constructs.

### Creating Resolvers

- Resolver names must be exact field name on your Schema's Types.
- Resolvers must return the value type declared for the matching schema.
- Resolvers can be async.

### Creating Servers

**Schema + Resolvers = Server**

To create a server, the minimum requirement is a query type with a field and a resolver for that field.

A simple example:

```javascript
const gql = require("graphql-tag");
const { ApolloServer } = require("apollo-server");

const typeDefs = gql`
  type User {
    email: String!
    avatar: String
    friends: [User]!
  }
  type Query {
    me: User!
  }
`;

const resolvers = {
  Query: {
    me() {
      return {
        email: "test@test.com",
        avatar: "http://yoga.png",
        friends: [],
      };
    },
  },
};

const server = new ApolloServer({
  typeDefs,
  resolvers,
});

server.listen(4000).then(() => {
  console.log(`Listening on port:${4000}`);
});
```

### Input Type

- Just like types, but used for arguments
- All field value types must be other input types or scalars.
