FROM node:18-alpine3.14

WORKDIR /project
COPY . .
RUN npm install

EXPOSE 3000
CMD ["npm", "start"]