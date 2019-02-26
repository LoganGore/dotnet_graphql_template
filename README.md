# MAANA.IO - .NET Core (C#) - GraphQL Service Template (Basic)

## What's the purpose of this template?

To provide an example of how a GraphQL service is built using a particular technology stack, in this case .NET Core in C#.
It is assumed you are familiar with developing .NET applications in C#.

## What are this template's capabilities?

Basic GraphQL interactions over HTTP. This template creates an application exposing a GraphQL endpoint with a Star Wars theme. With this endpoint you can examine the service's graphql schema, which will tell you about its types, queries, mutations, and subsriptions (look at the additional resources section at the bottom of this page if you don't know what these terms mean). Through the endpoint, and in the visual GraphQL playground, you can execute operations on the example database that is hardcoded in the application. Getting from the project files to an up-and-running application can be accomplished in one command through docker or the .NET Core CLI.

## What are the key technologies?

-.NET Core and ASP.NET Core
-GraphQl
-Docker

## About the template's dummy database and repository

This template uses a dummy database with a strongly typed repository to help you understand how your datasource (frequenly entity framework (EF) for .NET) can be leveraged via a graphql endpoint with an appropriate level of decoupling.

## Building and running this template

Use either the below Docker or .NET build instructions, then open the GraphQL playgroun exposed by the application in "https://localhost:5000". You may need to override a bad cert warning as the template defaults to HTTP/S.

-IN .NET (CLI):
The root-level project directory run the following .NET Core command:

```bash
dotnet run
```

-IN DOCKER (CLI) (Docker required):
The root-level project directory contains a Dockerfile.
The following docker command sequentially builds and then runs in docker.

```bash
docker build -t q_dotnet . && docker run -p 5000:5000 q_dotnet
```

#Post build/run health check of the service
-After building and running in docker, you should see the following CLI output from the application:

```bash
watch : Polling file watcher is enabled
watch : Started
[21:42:06 INF] Starting application
Hosting environment: Development
Content root path: /app
Now listening on: https://0.0.0.0:5000
Application started. Press Ctrl+C to shut down.
[21:42:12 INF] CORS policy execution successful.
[21:42:15 INF] CORS policy execution successful.
[21:42:18 INF] CORS policy execution successful.
(CORS MESSAGES WILL CONTINUE)
```

-Any errors should be visible in this output with stack trace.

## Example queries in the GraphQL playground

-GraphQL operations can be executed in the graphql playgound on the localhost endpoint in the left-hand side panel.
--Info Query:

```graphql
query {
  info {
    id
    name
    description
  }
}
```

--Info Query Response: (The query response will be the "data" property, meta-data associated with the response will be in the "extensions")

```json
{
"data": {
"info": {
"id": "ed7584-2124-98fs-00s3-t739478t",
"name": "maana.io.template",
"description": "Dockerized ASP.NET Core GraphQL Template"
}
},
"extensions": {
"tracing": {
"version": 1,
"startTime": "2019-02-25T21:45:53.8003062Z",
"endTime": "2019-02-25T21:45:53.8033062Z",
"duration": 2695400,
"parsing": {
...
...
```

--createHuman mutation (adds a human):

```graphql
mutation {
  createHuman(
    human: {
      name: "You"
      dateOfBirth: "02/28/1970"
      homePlanet: "Dantooine"
      appearsIn: [NEWHOPE]
    }
  ) {
    id
  }
}
```

--createHuman mutation response:

```json
{
"data": {
"createHuman": {
"id": "b1dd619e-be0d-40b5-8706-b2e14b3032c4"
}
},
"extensions": {
"tracing": {
"version": 1,
"startTime": "2019-02-26T04:29:21.942681Z",
"endTime": "2019-02-26T04:29:21.943681Z",
...
...
```

## Additional Resources

GraphQL.org for general graphql concepts and info
https://graphql.org/

The GraphQL .NET library on GitHub
https://github.com/graphql-dotnet/graphql-dotnet

Dockerizing .NET Core applications
https://docs.microsoft.com/en-us/dotnet/core/docker/docker-basics-dotnet-core

Dotnet-Boxed Templates - Github
https://github.com/Dotnet-Boxed/Templates

Example use of Dotnet-Boxed Templates (scaffolding for this template)
https://elanderson.net/2018/07/asp-net-core-with-graphql-using-net-boxed/
