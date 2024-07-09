FROM python:3.8

WORKDIR /app

COPY pyproject.toml poetry.lock ./

RUN pip install poetry && poetry install --no-dev

RUN poetry run bash ./prestart.sh

COPY . .

CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
