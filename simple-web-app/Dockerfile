FROM python:3.6-stretch

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

RUN pip install pipenv
RUN pipenv install Flask
ENV FLASK_APP app.py
ENV FLASK_ENV development

EXPOSE 5000
