### Docker By Technology Channel
In this guide you will learn to add docker to python project. We are using fastapi as a python web framework. We will create a simple web application and then we will add docker to it.

### Prerequisites
- Docker Desktop


### Step 1: Create a Virtual Environment
Create and activate a virtual environment using the following commands:
```bash
virtualenv venv
source venv/Scrips/activate
```

### Step 2: Install FastAPI
Install FastAPI and Uvicorn using the following commands:
```bash
pip install fastapi
pip install uvicorn
```

### Step 3: Create a FastAPI Application
Create a main.py file and add the following code:
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

### Step 4: Create a Dockerfile
Create a Dockerfile in the root directory of your project and add the following code:
```Dockerfile
# Use the official Python image from the Docker Hub
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
COPY requirements.txt .

# Install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the FastAPI app code into the container
COPY . .

# Expose port 80 to the outside world
EXPOSE 80

# Command to run the FastAPI app using Uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]

```

### Step 5: Create a requirements.txt File
Use freeze to create a requirements.txt file:
```bash
pip freeze > requirements.txt
```

### Step 6: Build the Docker Image
Build the Docker image using the following command:
```bash
docker build -t my-fastapi-app .
```

### Step 7: Run the Docker Container
Run the Docker container using the following command:
```bash
docker run -d --name my-fastapi-app -p 80:80 my-fastapi-app
```

### Step 8: Test the FastAPI Application
Open your web browser and go to http://localhost:80 to test the FastAPI application.
