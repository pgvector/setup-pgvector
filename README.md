# setup-pgvector

[pgvector](https://github.com/pgvector/pgvector) instructions for GitHub Actions

[![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/step.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions) [![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/service.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions)

## Getting Started

First, choose your installation method:

- [Step](#step)
- [Service](#service)

### Step

Add pgvector to the preinstalled Postgres installation on [runner images](https://github.com/actions/runner-images).

Linux

```yml
      - name: Install pgvector
        run: |
          sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh -y
          sudo apt-get install postgresql-14-pgvector
```

Mac

```yml
      - name: Install pgvector
        run: brew install pgvector
```

See a [full example](https://github.com/pgvector/setup-pgvector/blob/master/.github/workflows/step.yml)

### Service

Use the `ankane/pgvector` image instead of `postgres` for the [service container](https://docs.github.com/en/actions/using-containerized-services/creating-postgresql-service-containers).

```yml
    services:
      postgres:
        image: ankane/pgvector
        env:
          POSTGRES_HOST_AUTH_METHOD: trust
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          - 5432:5432
```

See a [full example](https://github.com/pgvector/setup-pgvector/blob/master/.github/workflows/service.yml)

## Contributing

Everyone is encouraged to help improve this project. Here are a few ways you can help:

- [Report bugs](https://github.com/pgvector/setup-pgvector/issues)
- Fix bugs and [submit pull requests](https://github.com/pgvector/setup-pgvector/pulls)
- Write, clarify, or fix documentation
- Suggest or add new features
