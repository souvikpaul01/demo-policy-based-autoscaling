# Auto-Scaling of VM instances using Prometheus and xOpera Orchestrator
This demo presents detailed instructions on how to process the initial deployment of the service.yaml, automate the deployment of servers and other scalable components based on the alerts from the alertmanager, which are triggered based on the rules defined in Prometheus server.

In the following example, we used two components for scaling the OpenStack instances such as Webhook Autoscaler and Monitoring Server.

# Set-up Webhook Server/Autoscaler Agent
The initial requirement of this example is to install and set up the recent release of  Xopera orchestrator. This can be done from the quickstart guide, shown as follows:
```
https://github.com/xlab-si/xopera-opera

```
This steps of installing XOpera are demonstrated as follows:
```
$ sudo apt-get update
$ mkdir ~/opera && cd ~/opera
$ sudo apt-get install python3-venv
$ python3 -m venv .venv && . .venv/bin/activate
(.venv) $ pip install opera

```
The OpenStack modules from Ansible playbooks is quite common, thus we can install opera with all required OpenStack libraries by running the following command:
```
(.venv) $ pip install -U opera[openstack]
```
After setup of the XOpera and Openstack SDK, it is required to clone the github repository in the opera folder consisting of the autoscaler agent with the following command:
```
git clone https://github.com/mainak89/demo-scaling 

```
