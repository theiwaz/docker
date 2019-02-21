# Base it on Ubuntu 16.04 LAP image (latest)
FROM node:8-alpine


# install chromium for headless browser tests
ENV CHROME_BIN=/usr/bin/chromium-browser
RUN apk add --no-cache chromium udev ttf-freefont \
	&& rm -rf /var/cache/apk/*

# set rights for node user
RUN chown -R node:node /usr/local/lib/node_modules \
  && chown -R node:node /usr/local/bin

# install angular-cli as node user
USER node
RUN npm install -g @angular/cli

# set npm as default package manager for root
USER root
WORKDIR /home/node
RUN ng new AngularApp --directory app --defaults true

WORKDIR /home/node/app
RUN ng set --global packageManager=npm

# Start the webserver
EXPOSE 4200 49153 

CMD ng serve --host 0.0.0.0 --port 4200 --verbose --poll 1000