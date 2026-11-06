# github-java-hub

Java 21 libraries for working with GitHub: call the REST API, wrap it in objects, and receive webhooks. Each one works on
its own, and they fit together.

> Unofficial. These projects are not affiliated with or endorsed by GitHub.

## The libraries

| Library | What it does | Maven Central |
|---|---|---|
| [github-sdk](https://github.com/piotr-janczukowicz/github-sdk) | Immutable objects over the REST client: `repository.createIssue(...)`, `issue.close()`, `pullRequest.merge()`. | [![Maven Central](https://img.shields.io/maven-central/v/io.github.piotr-janczukowicz/github-sdk)](https://central.sonatype.com/artifact/io.github.piotr-janczukowicz/github-sdk) |
| [github-rest-client](https://github.com/piotr-janczukowicz/github-rest-client) | Typed client for the [GitHub REST API](https://docs.github.com/en/rest): github.com, Enterprise Cloud and Enterprise Server, with pagination and rate-limit handling built in. | [![Maven Central](https://img.shields.io/maven-central/v/io.github.piotr-janczukowicz/github-rest-client)](https://central.sonatype.com/artifact/io.github.piotr-janczukowicz/github-rest-client) |
| [github-webhook](https://github.com/piotr-janczukowicz/github-webhook) | Typed webhook events (a record for every documented event), a decoder, and a receiver that verifies the signature before it parses anything. | [![Maven Central](https://img.shields.io/maven-central/v/io.github.piotr-janczukowicz/github-webhook)](https://central.sonatype.com/artifact/io.github.piotr-janczukowicz/github-webhook) |

## Highlights

**github-sdk**
- Objects with methods: `repository.createIssue(...)`, `issue.close()`, `pullRequest.merge()`.
- Immutable objects, `Optional` lookups that are empty on 404, and lazy streams for lists.
- One request for many changes: `update()`, `protect()` and `commitTo(branch)` collect fields and send them together.
- Every object keeps the complete client record in `response()`, so you can drop back to the client at any point.

**github-rest-client**
- Generated from GitHub's own OpenAPI descriptions, so every resource has a typed `GitHub*Api` class.
- One client for github.com, Enterprise Cloud and Enterprise Server.
- A value GitHub adds later decodes to `UNRECOGNIZED` instead of failing your code.
- Rate limits are waited out, pagination is followed and responses are immutable.

**github-webhook**
- A record for every documented event (313 events in 88 families), and a sealed interface per family, so the compiler
  checks your `switch`.
- The receiver checks the signature against the raw body before it parses anything.
- A new event, action or field never fails decoding.
- No HTTP client and no dependency on the REST client.

## How they fit together

- **github-sdk** is the quickest way in: objects with methods, on top of the REST client. You can drop back to the client
  for a call it does not cover.
- **github-rest-client** is the base under it. Use it alone when you want every endpoint as a typed call.
- **github-webhook** has no dependency on the others. Use it to receive events, then act on them with the SDK or the
  client.

## Which one do I need?

- Call the API, with less code: **github-sdk** (it brings the client).
- Call the API, with full coverage: **github-rest-client**.
- React to things that happen on GitHub: **github-webhook**.
- A bot that reacts and then acts: all three.

## License

[MIT](LICENSE)
