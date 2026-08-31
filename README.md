[![](https://img.shields.io/nuget/v/soenneker.make.openapiclient.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.make.openapiclient/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.make.openapiclient/build-and-test.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.make.openapiclient/actions/workflows/build-and-test.yml)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.make.openapiclient/publish-package.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.make.openapiclient/actions/workflows/publish-package.yml)
[![](https://img.shields.io/nuget/dt/soenneker.make.openapiclient.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.make.openapiclient/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.make.openapiclient/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/soenneker/soenneker.make.openapiclient/actions/workflows/codeql.yml)

# Soenneker.Make.OpenApiClient

A Kiota-generated .NET client for Make's API, with typed request builders, models, query parameters, and API error responses.

## Install

```bash
dotnet add package Soenneker.Make.OpenApiClient
```

## Direct usage

```csharp
using System.Net.Http.Headers;
using Microsoft.Kiota.Abstractions.Authentication;
using Microsoft.Kiota.Http.HttpClientLibrary;
using Soenneker.Make.OpenApiClient;

var httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization =
    new AuthenticationHeaderValue("Bearer", apiKey);

var adapter = new HttpClientRequestAdapter(
    new AnonymousAuthenticationProvider(),
    httpClient: httpClient)
{
    BaseUrl = "https://us1.make.com/api/v2"
};

var make = new MakeOpenApiClient(adapter);
var currentUser = await make.Users.Me.GetAsync(cancellationToken: cancellationToken);
```

Choose the base URL for the Make region that owns the account. Reuse the `HttpClient`, request adapter, and generated client rather than constructing them per request.

API failures are exposed as the generated endpoint-specific error types listed on each request method. Because this package is regenerated from Make's OpenAPI document, generated names and models can change when the upstream specification changes.

For application registration, configuration-based credentials, and managed reuse, use `Soenneker.Make.OpenApiClientUtil` with `Soenneker.Make.HttpClients`.
