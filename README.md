# setup-pgvector

[pgvector](https://github.com/pgvector/pgvector) instructions for GitHub Actions

[![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/step.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions) [![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/service.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions)

## Getting Started

First, choose your installation method:

- [Step](#step)
- [Service](#service)

### Step

To add to the preinstalled Postgres installation on [runner images](https://github.com/actions/runner-images#available-images), add a step to your workflow.

Ubuntu 24.04

```yml
      - name: Install pgvector
        run: |
          sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh -y
          sudo apt-get install postgresql-16-pgvector
```

Ubuntu 22.04 and 20.04

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

For a [service container](https://docs.github.com/en/actions/using-containerized-services/creating-postgresql-service-containers), use the `pgvector/pgvector:pg17` image instead of `postgres`.

```yml
    services:
      postgres:
        image: pgvector/pgvector:pg17
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
