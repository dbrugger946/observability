FROM registry.access.redhat.com/ubi9/nodejs-22:latest

# Copy package.json and package-lock.json
COPY package*.json ./


RUN npm ci 

COPY . /opt/app-root/src

ENV NODE_ENV=production

ENV PORT 3000

EXPOSE 3000

CMD ["npm", "start"]
