FROM python:3.12-alpine3.19 

ENV PYTHONUNBUFFERED 1

RUN pip install --upgrade pip

RUN mkdir -p /app 

WORKDIR /app 

COPY requirements.txt . 

RUN pip install -r requirements.txt 

EXPOSE 5000 

COPY . .

CMD ["python", "app.py"]