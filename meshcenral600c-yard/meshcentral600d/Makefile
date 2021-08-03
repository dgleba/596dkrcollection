
# One liners and simple stuff may be here in this makefile. See sc folder for scripts.


perm:
# fix permissions. make them group writable so www-data group can manage the files. move, delete, etc..  
	# docker-compose run --rm djan sh -c 'su root;chmod -R g+w .;exit;exit'
	# docker-compose run --rm mesh sh -c 'chgrp -R www-data . ;  chmod -R g+w . ; chmod +x *.sh ; chmod -R 777 /opt/meshcentral/meshcentral-data'
	docker-compose run --rm mesh sh -c 'chmod +x *.sh ; chown -R 1000:33 /opt/meshcentral/meshcentral-data ; chmod -R 777 /opt/meshcentral/meshcentral-data ; chmod -R 777 /opt/meshcentral/meshcentral-files'


# shell in django
#
djbash:
	docker-compose run djangodev /bin/bash



# clean docker containers 
#
clean:   
	# remove this one.. 
	-docker rmi dkr382r-django_djangodev
  # remove docker containers exited 
	-docker rm $$(docker ps -qa --no-trunc --filter "status=exited") 
	# remove tagged <none> 
	-docker rmi $$(docker images | grep "^<none>" | awk '{ print $3 }') 
	-docker network rm $(docker network ls | grep "bridge" | awk '/ / { print $1 }')


#
dkv: 
	docker --version
	docker-compose -version

# having trouble setting env variable, but do I need it?  
#
perm2:  
	docker-compose run djangodev \
	bash -c "export fold=/myproject; chmod -R g+rws,o-w  $${fold}"

  
  
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

# https://github.com/docker/compose/issues/2033 docker compose command line run sh multiple commands in one line
# $ requires escaping with $, so, $$
# continuation card  \
# - dash in front of command ignores error. -rm -f *.o
