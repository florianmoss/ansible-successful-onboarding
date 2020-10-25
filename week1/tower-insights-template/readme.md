# Register Cloud Host with Red Hat Insights

To follow this guide, you need an active Red Hat Automation subscription, commonly known as Ansible and Ansible Tower. This playbook will allow you to register existing RHEL deployments with Insights, this is especially useful for existing public cloud deployments.

### Ansible Tower Setup
1. Go to [Red Hat Automation Hub: Insights](https://cloud.redhat.com/ansible/automation-hub/redhat/insights).
2. Select **Get API token**
3. Log in to your Ansible Tower instance as Admin
4. Select **Settings** -> **Jobs**
5. Enter the following values: 
    - ```Primary Galaxy Server``` : 
    **https://cloud.redhat.com/api/automation-hub/**
    - ```Primary Galaxy Authentication URL``` : 
    **https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token**
    - ```Primary Galaxy Server Token```:
    **<generated_token_from_step_2>**
6. Select **Save**


### Inventory + Project + Credentials
- Make sure that you have an *Inventory that is made up of RHEL hosts only* - as these are the only hosts you can use with Insights.

- Create a project that links to your copy of this repo.

- Make sure you have the right Credentials setup to connect to the machine.

### Template
Create a template that uses the Inventory, Project and Credentials as setup above.
The following variables are needed under **Extra Variables** (or an external file):
```yaml
redhat_portal_username: <red_hat_username>
redhat_portal_password: <password>
insights_display_name: <example_system>
autoconfig: False
authmethod: BASIC
```

Example:
![Template Example](/images/template.png)

**!!! Don't forget to Save the Template!!!**

### Running it

To run the playbook, simply launch it. Tower will automatically pull the Collection from the Automation Hub. 

Go to the [Insights Dashboard](https://cloud.redhat.com/insights/dashboard) to confirm that the host registered correct.
