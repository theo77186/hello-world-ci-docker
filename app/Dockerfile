FROM node:18-alpine3.18

# create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# install dependencies
COPY package*.json ./
RUN rm -rf package-lock.json node_modules
RUN npm install

COPY . /usr/src/app

USER node
CMD ["npm", "start"]
