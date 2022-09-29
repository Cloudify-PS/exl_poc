# exl_poc

1. Installation Cloudify Spire Manager

To install the Main manager, please refer to the official documentation
https://docs.cloudify.co/latest/install_maintain/installation/installing-manager/
Spire is supported as of version 6.4.0.

2. Installation submanagers

You can install a sub-manager in the same way as the main manager (Spire). The most important thing is to make sure that your network is set up correctly (all local managers must be available for Spire AIO).

3. Exposing submanagers

To perform correct management, you need to expose information about your all submanagers in Spire. There are two ways to connect Spire with submanagers. The first is the token, the second is the username and password.

a) Token-based connection

A token can be generated via command: cfy token create  
(reference https://docs.cloudify.co/latest/cli/orch_cli/tokens/)
The value of the token must be added to the secrets on Spire. In the next step, deploy manager_exposer_token.yaml with proper inputs like endpoint, tenant, protocol and port.




b) Username and Password based connection

Add the password of the user as a secret on Spire manager. Next, deploy manager_exposer.yaml with proper inputs like user name, endpoint, tenant, protocol and port.
 

The result of deployment is an environment with all necessary information in Capabilities.

















4. “Deploy on” mechanism.

Depending on connection type (token or user and password) you can deploy the proper blueprint (deploy_on_token.yaml or deploy_on.yaml) with the action “Deploy on” from Bulk action. Below dialog appears. The inputs are visible when the blueprint is selected.
 

Inputs description:
blueprint_archive        -  url to zip which contains all necessary files, the source must be 				               available from submanager (it is recommended to use public repo)
blueprint_id                  - name of blueprint with which the file is to be uploaded
cloudify_secret_token  - name of secret which contains information about token
main_file_name            - name of blueprint file in zip package
trust_all	              - is value of CLOUDIFY_SSL_TRUST_ALL (true if certificate is not valid 		                            or for testing purpose)




Official documentation:
https://docs.google.com/document/d/1Ivsn-95hwsDUmuZltAn5ncUxUtiD5wEi56Mj9O6RluA/edit

