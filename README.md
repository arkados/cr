# ČR web development copy

ČR is a Rust web application about the Czech Republic. The workspace contains
its domain model, application logic, PostgreSQL schema, web server, templates,
static assets, and public territorial data used during local development.

| Crate | Role |
| --- | --- |
| `cr-domain` | Domain models and repository interfaces |
| `cr-app` | Application logic |
| `cr-infra` | PostgreSQL repositories and migrations |
| `cr-web` | Axum routes, Askama templates, and static files |

## Local development

Install a current stable Rust toolchain and PostgreSQL. Create a development
PostgreSQL database you own. Set `DATABASE_URL` in your local process environment
or in a local `.env` file. The web server applies the migrations on startup.

```shell
cargo check --workspace --locked
cargo test --workspace --locked
cargo run --locked -p cr-web
```

Open <http://localhost:3000>. The server listens on loopback. Use `PORT` to
choose another local port. To populate public territorial data once the schema
exists, run `cargo run --locked -p cr-infra --bin import-csv`.

Cloud storage and proxy integrations use optional environment variables and can
be left unconfigured. The image handlers return placeholders or a missing-image
response when an image origin has not been configured.

The source code is distributed under the [MIT license](LICENSE).
