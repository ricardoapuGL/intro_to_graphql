# Intro to Graphql

## From the get go

- graphql is a **communication standard**
- graphql is not a programing language
- objective: "...for **describing** the capabilities and requirements of data models for client-server applications"
- **self-documented**:
  >Ensure that all of your data is statically typed and these types inform what queries the schema supports.
- **included deprecation mechanism**
  > Reduce the need for breaking changes, but utilize a built-in mechanism for deprecations when you need to.
- **data source Agnostic**
"GraphQL does not mandate a particular programming language or storage system for application services that implement it"
- **you get what you ask for**:
  - GraphQL queries are **Field Sets**
  - field -> function **field resolver**
    - see [Selection Set](https://github.com/graphql/graphql-spec/blob/51337a9b820e296fa7d03ae77d534cb4b247c201/spec/Section%202%20--%20Language.md?plain=1#L326)
    - see [Field Alias](https://github.com/graphql/graphql-spec/blob/51337a9b820e296fa7d03ae77d534cb4b247c201/spec/Section%202%20--%20Language.md?plain=1#L463)

GraphQL **principles**:

1. Product-centric: ***GraphQL is unapologetically driven by the requirements of views and the front-end engineers that write them***.  
    - "Client First", me, 2023
    - "designed to build client applications by providing an intuitive and flexible syntax and system for describing their data requirements and interactions.", GraphQL Spec, 2021
2. Hierarchical
3. Strong-typing
4. Client-specified response
5. Introspective

____
---start Diagram---

```pseudocode
Client 
--request Document (in GraphQL)--> 
GraphQL Service
```

---end Diagram---
____

## Performance
Dado que:

- 1 field -> 1 resolver function
- data batching on  the server in stead of client (source??) 

Entonces: ==>
> performance improvements in frontend can be expected (source ??)
____
if
> repeatedly load data from your database.

Then,
> implement batching technique or DataLoader.
____

## Operations

OperationType: `query` | `mutation` | `subscription`

mutation example:

```graphql
mutation {
likeStory(storyID: 12345) {
    story {
    likeCount
    }
}
}
```

____
query shorhand:

```graphql
{
field
}
```

____

## Fragments

- primary unit of composition 
- recycle and reuse common pieces of queries

```graphql
query withFragments {
  user(id: 4) {
    friends(first: 10) {
      ...friendFields
    }
    mutualFriends(first: 10) {
      ...friendFields
    }
  }
}

fragment friendFields on User {
  id
  name
  profilePic(size: 50)
}
```