# DevOps Workshop with OpenShift and OpenShift Ansible Broker

The DevOps Workshop provides full-stack and DevOps engineers an introduction to OpenShift, OpenShift Ansible Broker and containers and how OpenShift and Ansible can be used to build fully automated end-to-end deployment pipelines using advanced deployments techniques like rolling deploys and blue-green deployment.

The lab application used in this workshop is available at https://github.com/openshift-labs/devops-oab-labs

# Agenda
* DevOps Introduction
* Create DEV Environment
* Create a Deployment Pipeline
* Running the CI/CD Pipeline on Every Change
* Automate Provisioning Traditional Databases on VMs 
* Create PROD Environment
* Promote Releases to Production
* Zero-Downtime Deployment in Production

*CAUTION: if using 2 clusters (dev, prod) for these labs, make sure the prod cluster image registry is accessible from the dev cluster*

# Run Guides Locally
```
$ git clone https://github.com/openshift-labs/devops-oab-guides.git
$ cd devops-oab-guides

$ docker run -it --rm -p 8080:8080 -v $(pwd):/app-data \
              -e CONTENT_URL_PREFIX="file:///app-data" \
              -e WORKSHOPS_URLS="file:///app-data/_summit-devops-lab.yml" \
              osevg/workshopper:latest 
```

# Deploy Guides on OpenShift
```
$ oc new-app osevg/workshopper:latest --name=guides \
    -e WORKSHOPS_URLS="https://raw.githubusercontent.com/openshift-labs/devops-oab-guides/master/_summit-devops-lab.yml"
$ oc expose svc/guides
```

# Prepare OpenShift Cluster for Labs
You need [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html) to use the provided playbook for deploying the required services (Gogs, Nexus, etc) for running these labs:

```
$ git clone https://github.com/openshift-labs/devops-oab-guides
$ cd devops-oab-guides/ansible
$ ansible-galaxy install -r requirements.yml
$ ansible-playbook init.yml
```
