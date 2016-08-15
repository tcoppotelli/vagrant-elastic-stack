# Elastic Stack in Vagrant

This repository will install the [Elastic Stack](https://www.elastic.co/products) (Elasticsearch, Logstash, and Kibana) with a simple `vagrant up` by using [Vagrant](https://www.vagrantup.com)'s [Ansible provisioner](https://www.vagrantup.com/docs/provisioning/ansible.html). All you need is a working [Vagrant installation](https://www.vagrantup.com/docs/installation/) 1.8.3+ and 4GB of RAM.



## Configure the Elastic Stack with Ansible

With the [Ansible playbooks](https://docs.ansible.com/ansible/playbooks.html) in the */elastic-stack/* folder you can configure the whole system step by step. Just run them in the given order inside the Vagrant box:

```
> vagrant ssh
$ ansible-playbook /elastic-stack/1_configure-elasticsearch.yml
$ ansible-playbook /elastic-stack/2_configure-kibana.yml
$ ansible-playbook /elastic-stack/3_configure-logstash.yml
```



## Configure Kibana

Check whether apache index was populater or not: (http://localhost:9200/_cat/indices?v)

Login to kibana: http://localhost:5601/


## Generate test data

You can use */opt/injector-5.0.jar* to generate test data in the `person` index. To generate 100,000 documents in batches of 1,000 run the following command:

```
$ java -jar /opt/injector-5.0.jar 100000 1000
```

## How to manage timezone
```
vagrant plugin install vagrant-timezone
```
