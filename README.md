Step 1: Created an ec2 linux instance from aws (fre tier)
        In this we have spinned up the instance and made few configs changes like enabling ICMP4 in inbound rules, inside the security groups of aws.
        Verified below: (By default the ping wont work for an aws instance)
        ansible all -i hosts -m ping
        Normal ping also giving data
        
Step 2: Installed nginx, docker, logrotate by using below roles for modularity:
        ROLES USED --> docker, logrotate, nginx (nginx role has aws installer command, due to some issue yum and apt didnt work, tried both)
        
        
Step 3: Started nginx server using ansible service module using role
        ROLES USED --> startnginx

Step 4: Ensure nginx runs on port 8080, this is achieved by modifying the /etc/nginx/nginx.conf
        ROLES USED --> modifynginxport

Step 5: Ensured syntax is correct after modifying the nginx.conf and restarted the nginx service to reflect the new changes
        ROLES USED --> nginxsyntaxcheck, restartnginx

Step 6: Configure logrotate so that, the logrotate cleans the nginx logs of 100 Mb size is reached. Modified the /etc/logrotate.d/nginx
        ROLES USED --> configlogrotate
