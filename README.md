# Ansible Playbook for InfluxDB & Grafana

This playbook aims to install [InfluxDB](http://influxdb.com/) and
[Grafana](http://grafana.org/) on a CentOS 7

Based on: bitmazk/ansible-digitalocean-influxdb-grafana and updated to support influxdb 0.9

# Quick quide

```
git clone https://github.com/joseba/ansible-influxdb-grafana.git
cd ansible-influxdb-grafana
cp hosts.sample hosts
vim hosts
cp vars/external_vars.yml.sample vars/external_vars.yml
vim vars/external_vars.yml
ansible-playbook -i hosts site.yml
```

# Detailed instructions

Grafana will be served via [nginx](http://nginx.org/), InfluxDB will be
accessible throught it's default webserver.

I haven't figured out how to run this stack with an SSL cert, so this is rather
insecure at the moment. For some reason, InfluxDB doesn't seem to work with
the same self signed SSL cert that I created for nginx.

## Create CentOS 7 & upload SSH key

First setup your CentoOS. Make sure to upload your public
SSH key. This will allow you to login as root without entering a password.

## Install Ansible

Make sure that you have Ansible installed. I wouldn't even bother to create a
virtualenv for this because it is quite unlikely that you will ever need
several different versions of Ansible on your machine. The latest should always
do.

```
sudo pip install ansible --upgrade
```

## Clone this repository & change variables

Now clone this repository and ``cd`` into the cloned folder.

Copy the ``hosts.example`` file and enter the IP address of your CentOS 7.

```
cp hosts.example hosts
vim hosts
```

Copy the ``external_vars.yml.example`` file and change all usernames and
passwords to your liking.

```
cp vars/external_vars.yml.sample vars/external_vars.yml
vim vars/external_vars.yml
```

## Run the playbook

Execute the playbook:

```
ansible-playbook -i hosts site.yml
```

Wasn't that easy? ;)

## Create awesome dashboards

You can now visit ``http://<CentOS 7-ip>:8083`` and see your InfluxDB admin.
You will see that we have two databases, one for saving grafana dashboards and
another for your project's metrics.

You can also visit ``http://<CentOS 7-ip>`` to see your grafana dashboard.
