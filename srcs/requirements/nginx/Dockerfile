FROM debian:buster

ARG DOMAIN_NAME
#install dependencies
RUN apt-get update && apt-get install nginx openssl -y 
#set SSL
RUN openssl req -x509 -nodes -days 365 -subj \
	"/C=BR/ST=PR/O=42/CN=$DOMAIN_NAME" -addext \
	"subjectAltName=DNS:$DOMAIN_NAME" -newkey rsa:2048 \
	-keyout /etc/ssl/private/nginx-selfsigned.key -out \
	/etc/ssl/certs/nginx-selfsigned.crt

#save conf file on container
RUN rm -rf /etc/nginx/sites-enabled/default
COPY conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/llima-ce.42.fr /etc/nginx/sites-enabled/
#port to communicate
EXPOSE 443

#start nginx and nginx only
CMD ["nginx", "-g", "daemon off;"]