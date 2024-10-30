# setup-pgvector

[pgvector](https://github.com/pgvector/pgvector) instructions for GitHub Actions

[![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/step-ubuntu.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions/workflows/step-ubuntu.yml) [![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/step-mac.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions/workflows/step-mac.yml) [![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/step-windows.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions/workflows/step-windows.yml) [![Build Status](https://github.com/pgvector/setup-pgvector/actions/workflows/service.yml/badge.svg?branch=master)](https://github.com/pgvector/setup-pgvector/actions/workflows/service.yml)

## Getting Started

First, choose your installation method:

- [Step](#step)
- [Service](#service)

### Step

To add to the preinstalled Postgres installation on [runner images](https://github.com/actions/runner-images#available-images), add a step to your workflow.

#### Ubuntu

```yml
      - name: Install pgvector
        run: |
          sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh -y
          sudo apt-get install postgresql-16-pgvector
```

Note: Replace `16` with `14` for `ubuntu-22.04` and `ubuntu-20.04`

See a [full example](https://github.com/pgvector/setup-pgvector/blob/master/.github/workflows/step-ubuntu.yml)

#### Mac

```yml
      - name: Install pgvector
        run: brew install pgvector
```

See a [full example](https://github.com/pgvector/setup-pgvector/blob/master/.github/workflows/step-mac.yml)

#### Windows

```yml
      - name: Install pgvector
        run: |
          call "C:\Program Files\Microsoft Visual Studio\2022\Enterprise\VC\Auxiliary\Build\vcvars64.bat"
          cd %TEMP%
          git clone --branch v0.8.0 https://github.com/pgvector/pgvector.git
          cd pgvector
          nmake /NOLOGO /F Makefile.win
          nmake /NOLOGO /F Makefile.win install
        shell: cmd
```

Note: Use `C:\Program Files (x86)\Microsoft Visual Studio\2019` for `windows-2019`

See a [full example](https://github.com/pgvector/setup-pgvector/blob/master/.github/workflows/step-windows.yml)

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
