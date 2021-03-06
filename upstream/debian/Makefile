PREP = prep
GIT_ROOT = $(shell git rev-parse --show-toplevel)
DISTRO_VAL = $(shell lsb_release -r | egrep -o '[0-9]{2}.[0-9]{2}')
DISTRO =  $(strip $(DISTRO_VAL))
$(PREP):
	#First time run requires update to install pkgs
	sudo apt-get update
	#Install pbuilder and copy the conf file
	if [ -d "/var/cache/pbuilder" ]; then \
		@echo "Folder found"; \
		cp utils/.pbuilderrc ~/; \
	else \
		@echo "Folder not found"; \
		sudo apt-get install pbuilder debootstrap devscripts; \
		sudo cp utils/.pbuilderrc ~/; \
		sudo pbuilder create; \
	fi; \
	sudo pbuilder update
	mkdir -p $(GIT_ROOT)/../build

kazoo:$(PREP)
	#Copy the kazoo debian directory to build dir and prepare a .orig file
	cp -R kazoo/kazoo-1.3.1 $(GIT_ROOT)/../build/
	(cd $(GIT_ROOT)/../build ; rm -rf kazoo-1.3.1/debian/)
	(cd $(GIT_ROOT)/../build; tar -zcvf kazoo_1.3.1.orig.tar.gz kazoo-1.3.1)
	cp -Rf kazoo/kazoo-1.3.1 $(GIT_ROOT)/../build/
	#Build the kazoo from the BUILD dir
	(cd $(GIT_ROOT)/../build/kazoo-1.3.1; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

docker-py-1.3.0:$(PREP)
	(cd $(GIT_ROOT)/../build; wget https://pypi.python.org/packages/source/d/docker-py/docker-py-1.3.0.tar.gz)
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/docker-py-1.3.0.tar.gz)
	(cd $(GIT_ROOT)/../build; cp docker-py-1.3.0.tar.gz docker-py_1.3.0.orig.tar.gz)
	cp -Rf docker-py-1.3.0/debian $(GIT_ROOT)/../build/docker-py-1.3.0
	#Build the docker-py from the BUILD dir
	(cd $(GIT_ROOT)/../build/docker-py-1.3.0; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

docker-py-0.6.0:$(PREP)
	(cd $(GIT_ROOT)/../build; wget https://pypi.python.org/packages/source/d/docker-py/docker-py-0.6.0.tar.gz)
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/docker-py-0.6.0.tar.gz)
	(cd $(GIT_ROOT)/../build; cp docker-py-0.6.0.tar.gz docker-py_0.6.0.orig.tar.gz)
	cp -Rf docker-py-0.6.0/debian $(GIT_ROOT)/../build/docker-py-0.6.0
	#Build the docker-py from the BUILD dir	
	(cd $(GIT_ROOT)/../build/docker-py-0.6.0; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

nova-docker-liberty: $(PREP)
	(cd $(GIT_ROOT)/../build; if [ -d nova-docker ] ; then cd nova-docker && echo "git clean -f && git pull"; else git clone -b stable/liberty git@github.com:Juniper/nova-docker.git; fi)
	(cd $(GIT_ROOT)/../build/nova-docker/; python setup.py sdist)
	cp $(GIT_ROOT)/../build/nova-docker/dist/nova-docker-0.0.1.dev241.tar.gz $(GIT_ROOT)/../build/nova-docker_0.0.1.dev241.orig.tar.gz
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/nova-docker_0.0.1.dev241.orig.tar.gz)
	mkdir -p $(GIT_ROOT)/../build/nova-docker-0.0.1.dev241/debian/; cp -Rf nova-docker/debian/liberty/* $(GIT_ROOT)/../build/nova-docker-0.0.1.dev241/debian
	(cd $(GIT_ROOT)/../build/nova-docker-0.0.1.dev241; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

nova-docker-kilo: $(PREP)
	(cd $(GIT_ROOT)/../build; if [ -d nova-docker ] ; then cd nova-docker && echo "git clean -f && git pull"; else git clone -b stable/kilo git@github.com:Juniper/nova-docker.git; fi)
	(cd $(GIT_ROOT)/../build/nova-docker/; python setup.py sdist)
	cp $(GIT_ROOT)/../build/nova-docker/dist/nova-docker-0.0.0.post196.tar.gz $(GIT_ROOT)/../build/nova-docker_0.0.0.post196.orig.tar.gz
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/nova-docker_0.0.0.post196.orig.tar.gz)
	mkdir -p $(GIT_ROOT)/../build/nova-docker-0.0.0.post196/debian/; cp -Rf nova-docker/debian/kilo/* $(GIT_ROOT)/../build/nova-docker-0.0.0.post196/debian
	(cd $(GIT_ROOT)/../build/nova-docker-0.0.0.post196; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

nova-docker-juno: $(PREP)
	(cd $(GIT_ROOT)/../build; if [ -d nova-docker ] ; then cd nova-docker && echo "git clean -f && git pull"; else git clone -b stable/juno git@github.com:Juniper/nova-docker.git; fi)
	(cd $(GIT_ROOT)/../build/nova-docker/; python setup.py sdist)
	cp $(GIT_ROOT)/../build/nova-docker/dist/nova-docker-0.0.0.post163.tar.gz $(GIT_ROOT)/../build/nova-docker_0.0.0.post163.orig.tar.gz
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/nova-docker_0.0.0.post163.orig.tar.gz)
	mkdir -p $(GIT_ROOT)/../build/nova-docker-0.0.0.post163/debian/; cp -Rf nova-docker/debian/juno/* $(GIT_ROOT)/../build/nova-docker-0.0.0.post163/debian/
	(cd $(GIT_ROOT)/../build/nova-docker-0.0.0.post163; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

nova-docker-icehouse: $(PREP)
	(cd $(GIT_ROOT)/../build; if [ -d nova-docker ] ; then cd nova-docker && echo "git clean -f && git pull"; else git clone -b stable/icehouse git@github.com:Juniper/nova-docker.git; fi)
	(cd $(GIT_ROOT)/../build/nova-docker/; python setup.py sdist)
	cp $(GIT_ROOT)/../build/nova-docker/dist/nova-docker-0.0.0.post126.tar.gz $(GIT_ROOT)/../build/nova-docker_0.0.0.post126.orig.tar.gz
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/nova-docker_0.0.0.post126.orig.tar.gz)
	mkdir -p $(GIT_ROOT)/../build/nova-docker-0.0.0.post126/debian/; cp -Rf nova-docker/debian/icehouse/* $(GIT_ROOT)/../build/nova-docker-0.0.0.post126/debian
	(cd $(GIT_ROOT)/../build/nova-docker-0.0.0.post126; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

oslo-concurrency:$(PREP)
	(cd $(GIT_ROOT)/../build; wget https://pypi.python.org/packages/source/o/oslo.concurrency/oslo.concurrency-1.4.1.tar.gz)
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/oslo.concurrency-1.4.1.tar.gz)
	(cd $(GIT_ROOT)/../build; cp oslo.concurrency-1.4.1.tar.gz python-oslo.concurrency_1.4.1.orig.tar.gz)
	cp -Rf oslo.concurrency-1.4.1/debian $(GIT_ROOT)/../build/oslo.concurrency-1.4.1
	#Build the docker-py from the BUILD dir
	(cd $(GIT_ROOT)/../build/oslo.concurrency-1.4.1; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

libipfix:$(PREP)
	#copy the libipfix debian directory to build dir and prepare a .orig file
	cp -Rf libipfix/libipfix_110209 $(GIT_ROOT)/../build/libipfix_110209-1
	#Run configure once to setup the prefix path and
	# then prepare the orig.tar.gz
	(cd $(GIT_ROOT)/../build/libipfix_110209-1/; ./configure --prefix=/home/ubuntu/build/libipfix_110209-1/debian/tmp/usr)
	(cd $(GIT_ROOT)/../build ; rm -rf libipfix_110209-1/debian/)
	(cd $(GIT_ROOT)/../build; tar -zcvf libipfix_110209-1.orig.tar.gz libipfix_110209-1)
	(cd $(GIT_ROOT)/../build; rm -rf libipfix_110209-1)
	cp -Rf libipfix/libipfix_110209 $(GIT_ROOT)/../build/libipfix_110209-1
	#Change the changelog to include distro information
	(cd $(GIT_ROOT)/../build/libipfix_110209-1/; sed -i 's/(110209-1)/(110209-1-0ubuntu0.$(DISTRO))/g' debian/changelog)
	#Build the liibpfix from the BUILD dir
	(cd $(GIT_ROOT)/../build/libipfix_110209-1; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

expat:$(PREP)
	#Copy the expat debian directory to build dir and prepare a .orig file
	cp -R expat/ $(GIT_ROOT)/../build/
	(cd $(GIT_ROOT)/../build/expat;bash $(GIT_ROOT)/upstream/debian/utils/get-sources.sh)
	#Build the expat from the BUILD dir
	(cd $(GIT_ROOT)/../build/expat; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

kafka:$(PREP)
	#Get the kafka binary pkg
	(cd $(GIT_ROOT)/../build/; wget http://www.motorlogy.com/apache/kafka/0.9.0.1/kafka_2.11-0.9.0.1.tgz)
	#untar the gz
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/kafka_2.11-0.9.0.1.tgz)
	#Rename the gz file to orig.tar.gz
	(cd $(GIT_ROOT)/../build; cp kafka_2.11-0.9.0.1.tgz kafka_2.11-0.9.0.1.orig.tar.gz)
	#copy the debian  to build dir
	cp -Rf kafka/debian $(GIT_ROOT)/../build/kafka_2.11-0.9.0.1
	#Build the kafka from the BUILD dir
	(cd $(GIT_ROOT)/../build/kafka_2.11-0.9.0.1; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

kafka_2.10:$(PREP)
	#Get the kafka binary pkg
	(cd $(GIT_ROOT)/../build/; wget https://github.com/Juniper/contrail-third-party-cache/blob/master/kafka/kafka_2.10-0.9.0.0-SNAPSHOT.tgz?raw=true -O kafka_2.10-0.9.0.0-SNAPSHOT.tgz)
	#untar the gz
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/kafka_2.10-0.9.0.0-SNAPSHOT.tgz)
	#Rename the gz file to orig.tar.gz
	(cd $(GIT_ROOT)/../build; cp kafka_2.10-0.9.0.0-SNAPSHOT.tgz kafka_2.10-0.9.0.0-SNAPSHOT.orig.tar.gz)
	#copy the debian  to build dir
	cp -Rf kafka_2.10-0.9.0.0/debian $(GIT_ROOT)/../build/kafka_2.10-0.9.0.0-SNAPSHOT
	#Build the kafka from the BUILD dir
	(cd $(GIT_ROOT)/../build/kafka_2.10-0.9.0.0-SNAPSHOT; pdebuild --use-pdebuild-internal --debbuildopts -tc)

lxml:$(PREP)
	#Copy the lxml debian directory to build dir and prepare a .orig file
	cp -R lxml/ $(GIT_ROOT)/../build/
	(cd $(GIT_ROOT)/../build/lxml;bash $(GIT_ROOT)/upstream/debian/utils/get-sources.sh)
	#Build the lxml from the BUILD dir
	(cd $(GIT_ROOT)/../build/lxml; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)

nodejs:$(PREP)
	#Copy the nodejs debian directory to build dir and prepare a .orig file
	cp -R nodejs/ $(GIT_ROOT)/../build/
	(cd $(GIT_ROOT)/../build/nodejs;bash $(GIT_ROOT)/upstream/debian/utils/get-sources.sh)
	#Build the nodejs from the BUILD dir
	#(cd $(GIT_ROOT)/../build/nodejs; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc)
	(cd $(GIT_ROOT)/../build/nodejs; sbuild -A)

librdkafka:$(PREP)
	#copy the 0.8.5 orig.tar.gz file to build
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/ubuntu/+archive/primary/+files/librdkafka_0.8.5.orig.tar.gz)
	#copy the debian file to build
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/librdkafka_0.8.5.orig.tar.gz)
	(cd $(GIT_ROOT)/../build; mv librdkafka-0.8.5 librdkafka-0.8.5-2)
	(cd $(GIT_ROOT)/../build; mv librdkafka_0.8.5.orig.tar.gz librdkafka_0.8.5-2.orig.tar.gz)
	#untar the .debian.gz file inside the untarred location
	cp -rf librdkafka*/debian $(GIT_ROOT)/../build/librdkafka*/
	#Issue pdebuild inside the source
	#(cd $(GIT_ROOT)/../build/librdkafka*; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc )
	(cd $(GIT_ROOT)/../build/librdkafka*; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc --auto-debsign  --debsign-k $(GPGKEY))

kafka-python:$(PREP)
	#wget the file to GIT_ROOT
	(cd $(GIT_ROOT)/../build; wget https://pypi.python.org/packages/source/k/kafka-python/kafka-python-0.9.2.tar.gz)
	#untar the file
	(cd $(GIT_ROOT)/../build; tar -zxvf kafka-python-0.9.2.tar.gz)
	#Copy the debian from the repo to the untarred location
	(cp -avr kafka-python-0.9.2/debian $(GIT_ROOT)/../build/kafka-python-0.9.2)
	#Create the .orig file
	(mv $(GIT_ROOT)/../build/kafka-python-0.9.2.tar.gz $(GIT_ROOT)/../build/python-kafka-python_0.9.2.orig.tar.gz)
	#Issue pdebuild inside the source
	(cd $(GIT_ROOT)/../build/kafka-python-0.9.2; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc )

horizon:$(PREP)
	#Update the pbuilder with canonical cloud repo and update it
	#.pbuilderrc-cloud contains trusty repository for precise we may have to add
	sudo cp utils/.pbuilderrc-cloud ~/.pbuilderrc; \
	#Put a script in hooks dir of pbuilder to export the gpg keys of the repo
	#the keyring is for canonical trusty. It may change for precise
	if [ ! -d "/var/cache/pbuilder/hook.d" ]; then \
		sudo mkdir /var/cache/pbuilder/hook.d; \
		sudo cp utils/E01cacnonical-keyring /var/cache/pbuilder/hook.d/; \
		sudo chmod a+x /var/cache/pbuilder/hook.d/E01cacnonical-keyring;	\
	fi; \
	#Update the pbuilder with these changes
	sudo pbuilder --update --override-config --distribution trusty
	#Get the horizon source and the orig file
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/ubuntu/+archive/primary/+files/horizon_2014.2.2.orig.tar.gz)
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/ubuntu/+archive/primary/+files/horizon_2014.2.2.orig-xstatic.tar.gz)
	#untar the contents
	(cd $(GIT_ROOT)/../build;tar -zxvf horizon_2014.2.2.orig.tar.gz)
	(cd $(GIT_ROOT)/../build;tar -zxvf horizon_2014.2.2.orig-xstatic.tar.gz)
	#Move the xstatic folder inside the horizon
	(cd $(GIT_ROOT)/../build;mv xstatic horizon-2014.2.2/)
	#copy the horizon/debian folder to the build dir
	(cp -avr horizon-2014.2.2/debian $(GIT_ROOT)/../build/horizon-2014.2.2/)
	#Apply the patches manually because patch format is not quilt(it wont be applied automatically as part of build)
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; patch -p1 < debian/patches/contrail-floating-ip.patch)
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; patch -p1 < debian/patches/fix-dashboard-django-wsgi.patch)
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; patch -p1 < debian/patches/fix-dashboard-manage.patch)
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; patch -p1 < debian/patches/ubuntu_settings.patch)
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; patch -p1 < debian/patches/embedded-xstatic.patch)
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; patch -p1 < debian/patches/add-juju-environment-download.patch)	
	#Issue pdebuild command	
	(cd $(GIT_ROOT)/../build/horizon-2014.2.2; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc )

horizon-kilo:$(PREP)
	#Update the pbuilder with canonical cloud repo and update it
	#.pbuilderrc-cloud contains trusty repository for precise we may have to add
	sudo cp utils/.pbuilderrc-cloud ~/.pbuilderrc; \
	#Put a script in hooks dir of pbuilder to export the gpg keys of the repo
	#the keyring is for canonical trusty. It may change for precise
	if [ ! -d "/var/cache/pbuilder/hook.d" ]; then \
		sudo mkdir /var/cache/pbuilder/hook.d; \
		sudo cp utils/E01cacnonical-keyring /var/cache/pbuilder/hook.d/; \
		sudo chmod a+x /var/cache/pbuilder/hook.d/E01cacnonical-keyring;	\
	fi; \
	#Update the pbuilder with these changes
	sudo pbuilder --update --override-config --distribution trusty
	#Get the horizon source and the orig file
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/~ubuntu-cloud-archive/+archive/ubuntu/kilo-staging/+files/horizon_2015.1.2.orig.tar.gz)
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/~ubuntu-cloud-archive/+archive/ubuntu/kilo-staging/+files/horizon_2015.1.2.orig-xstatic.tar.gz)
	#untar the contents
	(cd $(GIT_ROOT)/../build;tar -zxvf horizon_2015.1.2.orig.tar.gz)
	(cd $(GIT_ROOT)/../build;tar -zxvf horizon_2015.1.2.orig-xstatic.tar.gz)
	#Move the xstatic folder inside the horizon
	(cd $(GIT_ROOT)/../build;mv xstatic horizon-2015.1.2/)
	#copy the horizon/debian folder to the build dir
	(cp -avr horizon-2015.1.2/debian $(GIT_ROOT)/../build/horizon-2015.1.2/)
	#Issue pdebuild command
	(cd $(GIT_ROOT)/../build/horizon-2015.1.2; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc )

horizon-liberty:$(PREP)
	#Update the pbuilder with canonical cloud repo and update it
	#.pbuilderrc-cloud contains trusty repository for precise we may have to add
	sudo cp utils/.pbuilderrc-cloud ~/.pbuilderrc; \
	#Put a script in hooks dir of pbuilder to export the gpg keys of the repo
	#the keyring is for canonical trusty. It may change for precise
	if [ ! -d "/var/cache/pbuilder/hook.d" ]; then \
	sudo mkdir /var/cache/pbuilder/hook.d; \
	sudo cp utils/E01cacnonical-keyring /var/cache/pbuilder/hook.d/; \
	sudo chmod a+x /var/cache/pbuilder/hook.d/E01cacnonical-keyring;        \
	fi; \
	#Update the pbuilder with these changes
	sudo pbuilder --update --override-config --distribution trusty
	#Get the horizon source and the orig file
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/~ubuntu-cloud-archive/+archive/ubuntu/liberty-staging/+files/horizon_8.0.1.orig.tar.gz)
	(cd $(GIT_ROOT)/../build; wget https://launchpad.net/~ubuntu-cloud-archive/+archive/ubuntu/liberty-staging/+files/horizon_8.0.1.orig-xstatic.tar.gz)
	#untar the contents
	(cd $(GIT_ROOT)/../build;tar -zxvf horizon_8.0.1.orig.tar.gz)
	(cd $(GIT_ROOT)/../build;tar -zxvf horizon_8.0.1.orig-xstatic.tar.gz)
	#Move the xstatic folder inside the horizon
	(cd $(GIT_ROOT)/../build;mv xstatic horizon-8.0.1/)
	#copy the horizon/debian folder to the build dir
	(cp -avr horizon_8.0.1/debian $(GIT_ROOT)/../build/horizon-8.0.1/)
	#Issue pdebuild command
	(cd $(GIT_ROOT)/../build/horizon-8.0.1; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc )

python-cassandra:$(PREP)
	(cd $(GIT_ROOT)/../build; wget https://pypi.python.org/packages/source/c/cassandra-driver/cassandra-driver-3.0.0.tar.gz#md5=c853a91c63d3ca4e646c4a8ee2ebed05)
	(cd $(GIT_ROOT)/../build; tar -xvzf $(GIT_ROOT)/../build/cassandra-driver-3.0.0.tar.gz)
	# This depends on having extensions so do python build and clean 
	# Then prepare orig.tar.gz so that it does not complain abt upstream changes
	(cd $(GIT_ROOT)/../build/cassandra-driver-3.0.0; python setup.py build)
	(cd $(GIT_ROOT)/../build/cassandra-driver-3.0.0; python setup.py clean)
	(cd $(GIT_ROOT)/../build/; tar -zcf cassandra-driver_3.0.0.orig.tar.gz cassandra-driver-3.0.0)
	cp -Rf python-cassandra/debian $(GIT_ROOT)/../build/cassandra-driver-3.0.0
	#Build the python-cassandra from the BUILD dir 
	(cd $(GIT_ROOT)/../build/cassandra-driver-3.0.0; pdebuild --use-pdebuild-internal --debbuildopts "-tc")

python-sseclient:$(PREP)
	#wget the file to GIT_ROOT
	(cd $(GIT_ROOT)/../build; wget https://pypi.python.org/packages/source/s/sseclient/sseclient-0.0.11.tar.gz)
	#untar the file
	(cd $(GIT_ROOT)/../build; tar -zxvf sseclient-0.0.11.tar.gz)
	#Copy the debian from the repo to the untarred location
	(cp -avr python-sseclient/debian $(GIT_ROOT)/../build/sseclient-0.0.11)
	#Create the .orig file
	(mv $(GIT_ROOT)/../build/sseclient-0.0.11.tar.gz $(GIT_ROOT)/../build/python-sseclient_0.0.11.orig.tar.gz)
	#Issue pdebuild inside the source
	(cd $(GIT_ROOT)/../build/sseclient-0.0.11; sudo pdebuild --use-pdebuild-internal --debbuildopts -tc )

# Pls keep sorted (reduce merge issues)
all:$(PREP) \
	docker-py \
        nova-docker \
	expat \
	kafka \
	kafka_2.10 \
	kazoo \
	libipfix \
	nodejs \
	librdkafka \
	lxml \
	kafka-python \
        horizon \
        python-cassandra \
        python-sseclient
