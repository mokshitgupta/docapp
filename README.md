# DocApp — Doctor Appointment System

A production-ready Django web application for booking doctor appointments, deployed with full DevOps setup.

## Tech Stack
- **Backend:** Django 4.2
- **Server:** Gunicorn
- **Containerization:** Docker
- **CI/CD:** Jenkins
- **Cloud:** AWS EC2
- **Monitoring:** Prometheus + Grafana

## Features
- Patient registration & login
- Doctor listing by specialization
- Appointment booking & cancellation
- Admin dashboard
- Prometheus metrics endpoint

## Local Setup

```bash
git clone https://github.com/mokshitgupta/docapp.git
cd docapp
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

## Docker Setup

```bash
docker-compose up -d
```

App runs on: http://localhost:8000
Prometheus: http://localhost:9090
Grafana: http://localhost:3000

## Environment Variables

```
SECRET_KEY=your-secret-key
DEBUG=True
ALLOWED_HOSTS=*
```

## Built by Mokshit Gupta
