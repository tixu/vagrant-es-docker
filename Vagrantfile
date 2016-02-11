Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  chmod = 'chmod 777 /compose'
  config.vm.provision('shell',inline: chmod)
  config.vm.synced_folder "compose", "/compose"

  docker_opts = 'sudo sed -i \'$ a DOCKER_OPTS=\"$DOCKER_OPTS --insecure-registry=port-fv.smals-mvm.be:5000\"\' /etc/default/docker'

  # Elasticsearch
  create_es_data_folder = 'mkdir -p /usr/share/elasticsearch/data;chmod 777 /usr/share/elasticsearch/data'
  create_es_config_folder = 'mkdir -p /usr/share/elasticsearch/config;chmod 777 /usr/share/elasticsearch/config'
  config.vm.provision('shell',inline: create_es_data_folder)
  config.vm.provision('shell',inline: create_es_config_folder)

  # Logstash
  create_ls_config_folder = 'mkdir -p /usr/share/logstash/config;chmod 777 /usr/share/logstash/config'
  config.vm.provision('shell',inline: create_ls_config_folder)

  # Kibana
  create_kb_config_folder = 'mkdir -p /usr/share/kibana/config;chmod 777 /usr/share/kibana/config'
  config.vm.provision('shell',inline: create_kb_config_folder)

  # Provisionning via Docker & Docker Compose
  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: "/compose/docker-compose.yml", rebuild: true, run: "always"

  config.vm.provision('shell',inline:docker_opts)

  # Surcharge config VM
  config.vm.provider "virtualbox" do |v,override|
    v.name="getting_started_vm"
    v.gui = false
    v.memory = 2048
    v.cpus = 1
    override.vm.network :forwarded_port, guest: 80 , host: 8000
    override.vm.network :forwarded_port, guest: 9200 , host: 9200
    override.vm.network :forwarded_port, guest: 5601 , host: 5601
    override.vm.network :forwarded_port, guest: 5000 , host: 5000
 end

end
