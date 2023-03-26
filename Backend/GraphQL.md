# GraphQL
GraphQL is a query language for API developed by Meta. It provides a schema of the data in the API and gives clients the power to ask for exactly what they need. GraphQL sits between clients and the backend services. It could aggregate multiple resource requests into a single query. It also supports mutations, and subscriptions. Mutations are GraphQL's way of applying data modifications to resources. Subscriptions are GraphQL's way for clients to receive notifications on data modifications.

## How is GraphQL the same as REST? How are they different?
Let's dive deeper. In practice, both GraphQL and REST send HTTP requests and receive HTTP responses. Let's compare how simple REST and GraphQL operations look like. REST centers around resources. Each resource is identified by a URL. To fetch a book from a bookstore API, it could look something like this: 

```
  GET /books/123
  {
    "title": "System Design Interview Volume 2",
    "authors": [
      {
        "name": "Alex Xu"
      },
      {
        
        "name: "Sahn Lam"
      }
    ]
    ...
  }
```
Note that the authors field is implementation specific. Some REST API implementations might break them out into separate REST calls. 

With GraphQL, this looks different. We first define types. In this example, we have the Book and Author types.
```
type Book {
  id: ID
  title: String
  authors: [Author]
}

type Author {
  id: ID
  name: String
  books: [Book]
}
```

these types describe the kinds of data available. They don't specify how the data is retrieved via GraphQL. To do that, we need to define a Query, like this. 
```
type Query {
  book(id: ID!): Book
}
```

Now we can send a request to the GraphQL endpoint to fetch the same data.
```
GET /graphql?query={book(id: "123") {title, authors {name}}}
```

As we can see, REST and GraphQL both use HTTP. Both make a request via a URL, and both can return a JSON response in the same shape.

Here are the differences:

With GraphQL, we specify the exact resources we want, and also which fields we want. In the REST example, the API implementer decided for us that authors are included as related resources. With GraphQL, the client decides what to include. This brings up one of the main benefits of GraphQL. GraphQL doesn't use URLs to specify the resources that are available in the API. Instead, it uses a GraphQL schema. We can send a complex query that fetches additional data according to the relationships defined in the schema. Doing the same in REST is more complicated. We would have to do that client side with multiple requests. This is a common problem resulting in N+1 queries. 

Next, let's discuss some drawbacks of GraphQL. 

The beauty of REST is that we don't need special libraries to consume someone else's API. Requests can simply be sent using common tools like cURL or simply a web browser. In contrast, GraphQL requires heavier tooling support, both on the client and server sides. This requires a sizable upfront investment. This upfront cost might not be orth it, especially for very simple CRUD APIs. 

Another criticism of GraphQL is that it is more difficult to cache. REST uses HTTP GET for fetching resources, and HTTP GET has a well-defined caching behavior that is  leveraged by browsers, CDNs, proxies, and web servers. GraphQL has a single point of entry and uses HTTP POST by default. This prevents the full use of HTTP caching. With care, GraphQL could be configured to better leverage HTTP caching. The detail is very nuanced. 

The final concern we have with GraphQL is that while GraphQL allows clients to query for just the data they need, this also poses a great danger. 

Imagine this example where a mobile application shipped a new feature that causes an unexpected table scan of a critical database table of backend service. This could bring the database down as soon as the new application goes live. Yes, there are ways to mitigate this risk, but it adds even more complexity to a GraphQL implementation. The cost to safeguard risks like this must be factored in when considering GraphQL. 

## So, should we use GraphQL?
We hve repeatedly said that software engineering is about tradeoffs. There is no one right answer. 