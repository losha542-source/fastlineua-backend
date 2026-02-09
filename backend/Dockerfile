FROM python:3.11

ENV PYTHONUNBUFFERED=1
WORKDIR /app

# system deps
RUN apt-get update \
 && apt-get install -y gcc libpq-dev \
 && rm -rf /var/lib/apt/lists/*

# install poetry
RUN pip install --no-cache-dir poetry

# copy deps
COPY pyproject.toml poetry.lock* ./

RUN poetry config virtualenvs.create false \
 && poetry install --no-interaction --no-ansi

# copy app
COPY app ./app
COPY alembic.ini .
COPY scripts ./scripts

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
