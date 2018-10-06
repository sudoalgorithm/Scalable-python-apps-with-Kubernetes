# Steps to run and deploy the application on to IBM Kubernetes Services

## Prerequisites

- Python2.X or Python 3.X
- Docker

## Testing Locally

### Step - 1: Run the flask app locally

```
source venv/bin/activate
```
```
pip intall -r requirements.txt
```
```
python app.py
```

### Step - 2: Build the Docker image

```
docker build -t flask-web-app:latest .
```

### Step - 3: Build a container from the docker images and run the app

```
docker run -p -d 5000:5000 flask-web-app
```





