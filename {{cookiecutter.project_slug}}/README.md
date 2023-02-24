{% set is_open_source = cookiecutter.open_source_license != 'Not open source' -%}

# {{ cookiecutter.project_name }}

{% if is_open_source %}
[![pypi](https://img.shields.io/pypi/v/{{ cookiecutter.project_slug }}.svg)](https://pypi.org/project/{{ cookiecutter.project_slug }}/)
[![python](https://img.shields.io/pypi/pyversions/{{ cookiecutter.project_slug }}.svg)](https://pypi.org/project/{{ cookiecutter.project_slug }}/)
[![Build Status](https://github.com/{{ cookiecutter.github_username }}/{{ cookiecutter.project_slug }}/actions/workflows/dev.yml/badge.svg)](https://github.com/{{ cookiecutter.github_username }}/{{ cookiecutter.project_slug }}/actions/workflows/dev.yml)
[![codecov](https://codecov.io/gh/{{ cookiecutter.github_username }}/{{ cookiecutter.project_slug }}/branch/main/graphs/badge.svg)](https://codecov.io/github/{{ cookiecutter.github_username }}/{{ cookiecutter.project_slug }})

{% else %}
{% endif %}

{{ cookiecutter.project_short_description }}

{% if is_open_source %}

* Documentation: <<https://{{> cookiecutter.github_username }}.github.io/{{ cookiecutter.project_slug }}>
* GitHub: <<https://github.com/{{> cookiecutter.github_username }}/{{ cookiecutter.project_slug }}>
* PyPI: <<https://pypi.org/project/{{> cookiecutter.project_slug }}/>
* Free software: {{ cookiecutter.open_source_license }}
{% endif %}

## Features

This is starter  for [Starlite](https://github.com/starlite-api/starlite)  and much simpler version of <https://github.com/starlite-api/starlite-pg-redis-docker> , using peter's <https://github.com/topsport-com-au/starlite-saqlalchemy>

Starlite:

[Starlite documentation 📚](https://starlite-api.github.io/starlite/)

starlite-saqslalchmey:
<https://github.com/topsport-com-au/starlite-saqlalchemy>

## Run the application

### Setup

* `$ cp .env.example .env`
* `$ docker-compose build`
* `$ docker-compose run --rm app alembic upgrade head`

### Run

`$ docker-compose up --build`

### Async Worker Emails

To demonstrate usage of the asynchronous `SAQ` workers, when an `Author` is created we trigger a
worker function that sends an email.

`mailhog` is included in `docker-compose.yaml`, and includes a GUI that can be accessed at
`http://localhost:8025`.

Create an `Author`:

```bash
$ curl -w "\n" -X POST -H "Content-Type: application/json" -d '{"name": "James Patterson", "dob": "1974-3-22"}' http://localhost:8000/v1/authors
{"id":"6f395bdf-3e77-481d-98b2-3471c2342654","created":"2022-10-09T23:18:10","updated":"2022-10-09T23:18:10","name":"James Patterson","dob":"1974-03-22"}
```

Then check the `mailhog` GUI to see the email that has been sent by the worker.

### Migrations

#### Revision

`$ docker-compose run --rm app alembic revision --autogenerate -m "revision description"`

#### Migration

`$ docker-compose run --rm app alembic upgrade head`