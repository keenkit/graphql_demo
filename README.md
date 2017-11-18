# Graphql Demo

## Steps to run the project
Step1. Create the login user by:

```graphql
mutation createUser {
  createUser(
    name: "Will Hu"
    authProvider: {
      email: "Will.Hu@suncorp.com"
      password: "secret" 
    }
  ) {
    id
    name
  }
}
```
You will get
```graphql endpoint doc
{
  "data": {
    "createUser": {
      "id": "5a0fccf27fa8ef4c6d0f0903",
      "name": "Will Hu"
    }
  }
}

```

Step2. Sign in (Need to validate your information), all the actions behind is based on this signing in.

*Need to update the index.html, "Authorization" with your output from last step*
```javascript
    function graphQLFetcher(graphQLParams) {
        // This example expects a GraphQL server at the path /graphql.
        // Change this to point wherever you host your GraphQL server.
        return fetch('/graphql', {
            method: 'post',
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json',
                'Authorization': 'Bearer 5a0fccf27fa8ef4c6d0f0903',
            }
            ...
```

Begin to sign in by:
```graphql
mutation signIn {
  signinUser(auth: {email: "will.hu@suncorp.com", password: "secret"}) {
    token
    user {
      id
      name
    }
  }
}

```
You will get
```graphql endpoint doc
{
  "data": {
    "signinUser": {
      "token": "5a0fccf27fa8ef4c6d0f0903",
      "user": {
        "id": "5a0fccf27fa8ef4c6d0f0903",
        "name": "Will Hu"
      }
    }
  }
}
```

Step3. Begin to create repository (Link is the example)

```graphql
mutation createLink {
  createLink(url:"www.go.com", description:"go") {
    url
    description
  }
}

```

Step4. Fetch all the info from the db.
```graphql
query all {
  allLinks {
    id
    url
    description
  }
}
```

Add filter if you want:
```graphql
query all {
  allLinks (filter: {description_contains: "node", url_contains: "com"}) {
    url
    description
  }
}
```

Step5. Vote any link if you want.
```graphql
mutation vote {
  createVote(
    linkId: "5a0fd1797fa8ef54a396ebce"
    userId: "5a0fccf27fa8ef4c6d0f0903") {
    createdAt
    link {
      url
    }
    user {
      name
    }
  } 
}
```