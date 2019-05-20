---
title: "Try out GraphQL APIs"
---

import YoutubeEmbed from "../../src/YoutubeEmbed.js";

<YoutubeEmbed link="https://www.youtube.com/embed/AflCqgGu-ms" />

Similar to the `users` table, the `todos` table created in the previous step would have auto-generated GraphQL APIs for us to explore.

Let's go ahead and start exploring the GraphQL APIs for `todos` table.

## Mutation

Head over to Console -> GRAPHIQL tab and insert a todo using GraphQL Mutations.

```graphql
mutation {
  insert_todos(objects:[{title: "My First Todo", user_id: "1"}]) {
    affected_rows
  }
}
```

Click on the `Play` button on the GraphiQL interface to execute the query.

You should get a response looking something like this:

![Todo Mutation](https://graphql-engine-cdn.hasura.io/learn-hasura/assets/graphql-hasura/graphql-mutation-todo.png)

## Query

Now let's go ahead and query the data that we just inserted.

```graphql
query {
  todos {
    id
    title
    is_public
    is_completed
    user_id
  }
}
```

You should get a response looking something like this:

![Todo Query](https://graphql-engine-cdn.hasura.io/learn-hasura/assets/graphql-hasura/graphql-query-todo.png)

Note that some columns like `is_public`, `is_completed` have default values, even though you did not insert them during the mutation.

## Subscription

Let's run a simple subscription query over `todos` table to watch for changes to the table. In the above graphql query, replace `query` with `subscription`

```graphql
subscription {
  todos {
    id
    title
    is_public
    is_completed
    user_id
  }
}
```

Initially the subscription query will return the existing results in the response.

Now let's insert new data into the todos table and see the changes appearing in the response.

In a new tab, Head over to Console -> DATA tab -> todos -> Insert Row and insert another row.

![Insert new todo](https://graphql-engine-cdn.hasura.io/learn-hasura/assets/graphql-hasura/todo-insert-new-row.png)

And switch to the previous GRAPHIQL tab and see the subscription response returning 2 results.

![Todo Subscription](https://graphql-engine-cdn.hasura.io/learn-hasura/assets/graphql-hasura/graphql-subscription-todo.png)


