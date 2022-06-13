# Graphql and Apollo server

First of all, let's take github as example:

1. restful api (old) [https://docs.github.com/en/rest](https://docs.github.com/en/rest)
2. graphql api (new) [https://docs.github.com/en/graphql](https://docs.github.com/en/graphql)



The github api from v1 to v3 is based on `restful api`. However, v4 is based on `graphql.`

Why currently `Graphql` is trying to replace Restful api in the BFF layer in FE?&#x20;



### Graphql

#### 1. Ask the data you need

Sending the query with each field to api and getting exactly the data based on the query.

No over fetching and under fetching issue

#### 2. Get many resources in single request

Generally, `restful api` requires several apis to support one page, while in graphql the query could be one.

Plus, these data would follow the reference as `graph-theory` .

#### 3. Type system

1. The type system could ensure the return data is predictable.
2. It provides clear and helpful errors, when something is going wrong



### Apollo

`Graphql` is much more like a concept or the standard of building an api, while it still need to be implemented.

`Apollo` is the best tool to build `graphql` in the current tech environment.

The `Apollo` technology includes 3 parts: a). Apollo server b). Apollo client c). Apollo federation



#### 1. Apollo server

Features of `apollo server` includes:

a). mock server

when micro-service is not ready, it is very easy to setup some mock data for the endpoint.

This feature could reduce the developing time significantly.

b). well supported UT framework

Normally, the integration test is based on the framework like `nock` to simulate the server.

The framework gives a more simple way to mock the data source.

As the ut just needs to test the logic from query to calling microservice, the framework could cover all the logic in this scope.

c). Server-side caching

The cache for `Apollo` is not based on the request.

The `Apollo cache` has a different level, a.) static level b.) dynamic level



**a). static level**

As graphql is defined based on the type. So the static cache has is also based on the type system.

For example:

```
type Post {
  id: ID!
  title: String
  author: Author
  votes: Int @cacheControl(maxAge: 30)
  comments: [Comment]
  readByCurrentUser: Boolean! @cacheControl(maxAge: 10, scope: PRIVATE)
}
```

the cache could set in field level. you can see the `votes` and `readByCurrentUser` have been cached with the expiration date.

the cache could also be set in `type` level:

```
type Post @cacheControl(maxAge: 240) {
  id: Int!
  title: String
  author: Author
  votes: Int
  comments: [Comment]
  readByCurrentUser: Boolean!
}
```

Still this example, currently the whole object has been cached.

**b). dynamic level**

To implement the result of the query, the graphql has a concept of `resolver`. the `resolver` is a function to call microservice to get the entity.

such as:

```
const resolvers = {
  Query: {
    post: (_, { id }, _, info) => {
      info.cacheControl.setCacheHint({ maxAge: 60, scope: 'PRIVATE' });
      return find(posts, { id });
    }
  }
}
```

the `post` function result has been cached.

**c). memcached**

It could also centralize the `cache` to `redis` with no code (memcached).

eg:

```
const { BaseRedisCache } = require('apollo-server-cache-redis');
const Redis = require('ioredis');

const server = new ApolloServer({
  typeDefs,
  resolvers,
  cache: new BaseRedisCache({
    client: new Redis({
      host: 'redis-server',
    }),
  }),
  dataSources: () => ({
    moviesAPI: new MoviesAPI(),
  }),
});
```

From this example, you can see the only action to setup `redis` cache is to add plugin and connection string.



#### 2. Apollo client (browser)

First of all, `Apollo client` supports both `browser`, `android`, `ios`. As protool currently is based on browser, so below content will only discuss the browser part.

**a). cache system**

what is totally different from other packages is for client-side is `cache system` of `apollo client`.

Similar to the `apollo server`, `apollo client` is also not just based on the request. The cache is much more like an in-memory database.

![](<../../.gitbook/assets/myads filter vip cache.gif>)

The image above is the browser cache looks like in protool 2.0.

**b). fetch policy**

The other difference is fetch-policy: [https://www.apollographql.com/docs/react/data/queries/#supported-fetch-policies](https://www.apollographql.com/docs/react/data/queries/#supported-fetch-policies)

Developer could define different `fetch-policy` to enhance the performance.

**c). other features**

Apollo client's other features include: `pagination`, `error handle`, `Testing support` and so on. it is not necessary to discuss one by one.



#### 3. Apollo federation

Like the concept of microservice, sub-graph could also be implemented only the part of the composed supergraph and then merge into the BFF system.

![](<../../.gitbook/assets/image (4) (1).png>)





### Reference

1. [https://www.apollographql.com/](https://www.apollographql.com/)
2. [https://graphql.org/](https://graphql.org/)









