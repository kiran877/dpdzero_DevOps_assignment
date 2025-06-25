FROM python:3.9-slim

# Install curl (use apt for Debian-based image)
RUN apt-get update && apt-get install -y curl

WORKDIR /app

COPY app.py .

RUN pip install flask

EXPOSE 8002

CMD ["python", "app.py"]
