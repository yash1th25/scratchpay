FROM python:3.8-slim-buster
ENV PYTHONUNBUFFERED=1
WORKDIR /app

COPY python_database_scripts/requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY python_database_scripts/testscripts.py testscripts.py
COPY python_database_scripts/data.csv data.csv

EXPOSE 5000
CMD ["python3", "testscripts.py"]
