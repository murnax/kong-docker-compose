FROM node:8.11.3-alpine

RUN mkdir /app
WORKDIR /app

ADD ./config.yml .
RUN chmod +x /app/config.yml

ADD ./entrypoint.sh .
RUN chmod +x /app/entrypoint.sh

RUN npm install -g kongfig

RUN ls -la

RUN cat /app/config.yml

# CMD ["kongfig", "apply", "--path", "./config.yml", "--host", "kong:8001"]