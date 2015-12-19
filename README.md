# docker-easyengine-wordpress
Orchestrate/Pre-Build the 15mins EasyEngine WordPress deployment into Docker image.

Once completed, we will be going to have:
  + Vanilla Official Ubuntu:14.04 docker base image

  + EasyEngine base installation created:
	apt-get install wget
	wget -qO ee rt.cx/ee && sudo bash ee
 	source /etc/bash_completion.d/ee_auto.rc

  + Next step is to install the required stack and starting the services: MySQL (MariaDB), Web (Nginx + php5-fpm) and some admin utils
	ee stack install
	ee stack start

  + Once completed, a popular WordPress site is ready to get built automatically by the following command:
	ee site create wp.example.dev --user=YOURUSER --pass=YOURPSW --email=YOUREMAIL

    Or if you like to start with multi-site wordpress:
	ee site create wp.example.dev --user=YOURUSER --pass=YOURPSW --email=YOUREMAIL --wpsubdom
	
Alternative, we could create a pre-build stack image as follows:
	docker build -t ee-stack -f Dockerfile-stackinstall .
And then run ee-stack:
	docker run -itd -p 80:80 -p 443:443 -p 22222:22222 ee-stack bash

After that, going inside the container to start the services:
	docker exec -it ee-stack bash
	-->#$ /startStack.sh 