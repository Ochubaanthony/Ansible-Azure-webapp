Add below tasks:
Install Ansible on build agent
Install Ansible rm module on build agent
Execute Ansible playbook for creating resource group in Azure cloud.

## use this https://www.coachdevops.com/2024/04/automate-azure-app-service-setup-using.html
trigger:
- main
pr: none  # Disable PR triggers, can be adjusted as needed
pool:
  vmImage: 'ubuntu-latest'
steps:
- script: |
    # Install Ansible
    pip3 install "ansible==2.9.17"
  displayName: 'Install Ansible'
  
- script: |
    # Install Ansible rm module
    pip3 install ansible[azure]
  displayName: 'Install Ansible rm module'
  
- script: |
    # Run Ansible playbook to create Azure App Service
    ansible-playbook create-linux-app-svc.yml
  displayName: 'Run Ansible Playbook'
  env:
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    AZURE_CLIENT_ID: $(AZURE_CLIENT_ID)
    AZURE_SECRET: $(AZURE_SECRET) 
    AZURE_TENANT: $(AZURE_TENANT) 
