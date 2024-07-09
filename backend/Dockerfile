FROM python:3.10

WORKDIR /app

COPY pyproject.toml poetry.lock ./

RUN pip install poetry && poetry install --no-dev

COPY . .

# Expose the port that your application runs on
EXPOSE 8000

# Convert line endings of prestart.sh to Unix format
RUN apt-get update && apt-get install -y dos2unix \
	&& dos2unix ./prestart.sh \
	&& chmod +x ./prestart.sh

# Run the database initialization script
ENV PYTHONPATH=/app

CMD ["bash", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000"]