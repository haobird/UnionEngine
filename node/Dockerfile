FROM node:0.12

RUN npm install -g cnpm gulp bower && npm cache clear


ADD app.js /root/app.js
#ADD /www/htdocs/broadcast/app.js /root/app.js

WORKDIR /opt
EXPOSE 8001
VOLUME ["/opt"]
CMD node /root/app.js 8001
