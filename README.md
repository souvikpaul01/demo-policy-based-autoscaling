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
git clone https://github.com/radon-h2020/demo-policy-based-autoscaling

```
Change the working directory of the downloaded project. Before deploy the application, prepare the python environment and install necessary requirements. It is recommended that a Python virtual environment is used while installing the opera. This is an isolated and self-contained directory tree that contains a particular version of Python and installs additional packages.
```
cd demo-policy-based-autoscaling

```
In the virtual environment, configure the requirements for python using pip

```
pip install flask
pip install ruamel.yaml

```
Now the main components of the auto-scaler agent are set up. In order to have access to the Openstack environment, where the VM instances are deployed, Openstack SDK is used to get access to the environment. For this, initially download the Openstack RC file(ldpc-openrc.sh) and use the following command

```
(.venv) $ source ldpc-openrc.sh
(.venv) $ nova list

```
If the ‘nova list’ gives the list of servers deployed in Openstack, it confirms the connection is established. Next to make sure that the servers can be deployed and accessed with the same ssh key. This can be established with the following commands

```
(.venv) $ eval `ssh-agent`
(.venv) $ ssh pathToKey/KeyName.pem
(.venv) $ ssh-add -L

```
Now access configurations are done. The initial/base deployment of the server before starting the auto-scaler agent, assuming that the service.yaml file is ready to use
```
(.venv) $ opera deploy service.yaml
```
Finally, in order to start the webhook server for receiving the alerts from the alertmanager and trigger the autoscaler for the Scale-Up/Scale-Down, following file is used
```
(.venv) $ python server.py
```
 If the setup is done correctly and webhook is running, the following block is shown as output
 
 ```
(.venv) $ python server.py
 * Serving Flask app "server" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://0.0.0.0:5004/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 285-730-350

```
