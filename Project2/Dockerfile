FROM ubuntu:22.04

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install -y curl \
    && apt-get install -y nodejs \
    && apt-get install -y npm

# Print nodejs and npm versions for debugging
RUN node -v
RUN npm -v

WORKDIR /usr/src/app

COPY . .

# Install dependencies
RUN npm install

EXPOSE 3000

CMD ["node", "index.js"]
