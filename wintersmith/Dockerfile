# -- base image -- #
FROM node:alpine as builder

WORKDIR /opt/wintersmith/

# First thing we want is package.json to check for dependency/build freshness.
# If cache is invalidated, proceeding COPY build step and npm install  will not use cache either.
COPY static/package.json .

# Dependencies
RUN npm install

# Bundling both module directories in our image creates more possibilities for 
# paramaterizing the static build below.
# For this site, it's not necessary yet, however. 
#RUN npm install --only=production
#RUN cp -R node_modules production_modules
#RUN npm install

RUN npm install -g wintersmith

COPY static .
RUN wintersmith build 
RUN rm -rf node_modules

# -- static -- #
FROM nginx:stable-alpine

# Install dependencies for application, internal healthchecks etc. Optional.
#RUN apk update && apk add --no-cache \
#	ca-certificates \
#	wget \	
#	iproute2

# This COPY step could be parameterized to grab either  production_modules or node_modules from the builder step.
# So, we only copy exactly what we need and leave behind bulk and more importantly, no npm executables.
#COPY --from=builder /opt/nodejs/production_modules node_modules
COPY --from=builder /opt/wintersmith/build /srv/www

# The nginx.conf will be serving from /opt/nodejs/public directory.
# It should also have "daemon off" specified in first line. 
COPY nginx.conf /etc/nginx/nginx.conf

# Apply changes to nginx.conf here, or run custom scripts like in builder step.
# Alternatively, include nginx modification as a previous step outside of Dockerland. 

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/nginx","-g","daemon off;"]
