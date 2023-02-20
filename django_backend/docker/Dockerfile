#The path is using the base working dir where execute the docker compose
FROM python:3.9.0-alpine3.12

ENV PYTHONUNBUFFERED 1

RUN apk update \
  # psycopg2 dependencies
  && apk add --virtual build-deps gcc python3-dev musl-dev \
  && apk add postgresql-dev \
  && apk add postgresql-client

#!Copy the requirements file to the container root path  \
#!not the indicated container working dir in docker compose
#!and run the pip to install the requirements which are in the container root path not the working dir
#* you can also execute it directly in container wihout copy it in container root path
COPY ./django_backend/requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

COPY ./django_backend/docker/start /start
RUN sed -i 's/\r//' /start
RUN chmod +x /start

#!Set the working dir to the container working dir in docker compose
#!this is also the path that backend_root_folder mounted to
WORKDIR /app




