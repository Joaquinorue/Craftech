FROM python:3.7 as builder

#Create a new app folder and copy the Django app from the backend folder to app
WORKDIR /app
COPY /backend /app/

# Install pip requirements
RUN apt-get update \
    && apt-get install python3-dev graphviz libgraphviz-dev pkg-config -y \
    && pip install --upgrade pip 

RUN python -m pip install -r /app/requirements.txt

EXPOSE 8000

CMD ["python3", "0.0.0.0:8000", "/app/manage.py"]



FROM node:18-alpine3.14

WORKDIR /project
COPY /frontend .
RUN npm install
COPY --from=builder /app . 

EXPOSE 3000
CMD ["npm", "start"]