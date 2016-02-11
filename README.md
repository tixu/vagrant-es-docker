# vagrant-es-docker

A full stack of elk aimed to run in a virtualbox instance. This virtualbox instance is provisionned through [vagrant](https://www.vagrantup.com/).
It uses the docker engine and docker compose stak to start all the processes.
The container started are : 
 + an elasticsearch master
 + elasticsearch slave
 + kibana dashboard
 + logstash 
 
To start it, you need to go to the /compose directory of you virtual box instance  
+ docker-compose up 

To stop it
+ docker-compose stop
+ docker-composer rm

if you need to scale up the number of elasticsearch slave (reach 4 instances)
+docker-compose scale esslave = 4

Attention : this is only for testing purpose all the data are currently store in the container and will be lost, after each restart of the machine.



