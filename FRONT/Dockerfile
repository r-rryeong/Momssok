# frontend/Dockerfile

FROM node:16-alpine as build-stage
WORKDIR /var/jenkins_home/workspace/momssok/FRONT
COPY package*.json ./
RUN npm install --force
COPY . .
RUN npm run build

FROM nginx:stable-alpine as production-stage
COPY --from=build-stage /var/jenkins_home/workspace/momssok/FRONT/build /usr/share/nginx/html

COPY --from=build-stage /var/jenkins_home/workspace/momssok/FRONT/nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]