# aap_iac

IaC of ansible-dev automation controller

## Warning/Hazard

Be careful, if you decrypt the credentials, do not add them to the repo. You will be disciplined. 

## Getting started
This assumes a working Controller (AAP) deployment that has been activated. 

You will need an inventory that includes the controller API endpoint. If you wanted this to be quicker you can copy this repo to the Controller and run with `connection: local`.

Credentials/secrets are in `credentials.yml` all other things that aren't private are in `vars.yml`.

## Usage

Run with 
```
ansible-playbook site.yml -i inventory -e@credentials.yml --ask-vault-pass
```

## Debugging 
The module `awx.awx.credential` doesn't seem to be idempotent and some modules do not appear to be able to do minor modifications correctly (`awx.awx.tower_workflow_job_template_node`, `awx.awx.job_template`...etc).  Thus, it's helpful to have a snapshot of a vanilla AAP2 to debug this. However, reverting to a snapshot means the system time isn't accurate and leads to cloud services like AWS trashing your auth. So be sure to sync your clock after reverting. 

