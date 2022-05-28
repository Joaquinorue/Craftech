FROM python:3.7

#Create a new app folder and copy the Django app from the backend folder to app
WORKDIR /app
COPY . .

# Install pip requirements
RUN apt-get update \
    && apt-get install python3-dev graphviz libgraphviz-dev pkg-config -y \
    && pip install --upgrade pip 

RUN python -m pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]