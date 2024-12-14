     FILE NAME                        EXPLANATION 
playbook1.yml         =         Creating user USING USER MODULE IN ALL HOSTS  madhav  in /tmp/maha file,
                                with shell /bin/bash ,uid 1212, comment "a regular user 

playbook2.yml         =         Installing appache2  USING APT MODULE IN ALL HOSTS 
                                Copying data in to apache2 s/w USING COPY MODULE ,
                                and Restart apache2 s/w USING SERVICE MODULE 

playbook3.yml         =         Copying file USING COPY MODULE 
                                From /etc/passwd 
                                to /tmp
                                
playbook4.yml        =        Installing tomcat and tomcat9-admin s/w's USING APT MODULE 
                              copying tomcat-users.xml file to /etc/passwd USING COPY MODULE 
                              Changing port number 8080 to 9090  USING REPLACE MODULE 
                              Restart service of tomcat, tomcat9-admin  USING SERVICE MODULE
                              After restart waiting 1 min  USING PAUSE MODULE 
                              Checking tomcat9 is responcer on host2 USING URI MODULE 
                      
                          VARIABLES
                      
playbook5.yml      =          Installing/uninstalling s/w's USING APT MODULE WITH VARIABLES
                              GLOBAL SCOPE VARIABLES
                              In command we can give ant software we want 
                              
                              ansible-playbook playbook5.yml -b  --extra-vars "a=tree b=present c=yes"
                            
playbook6.yml      =          Installing/uninstalling s/w's USING APT MODULE AND CREATING FILES USING FILE MODULE  WITH VARIABLES
                              GLOBAL SCOPE VARIABLES
                              same as playbook5.yml file 

playbook7.yml      =          Installing/uninstalling s/w's USING APT MODULE WITH VARIABLES
                              PLAY SCOPE VARIABLES                      
                              Here  variables given in palaybook we can give outside of the playbook also 
                              
                               ansible-playbook playbook5.yml -b  --extra-vars "a=tree b=present c=yes"

               GROUP OF GVROUP WITH HOST SCOPE VARIABLES

playbook8.yml      =         Installing/uninstalling s/w's USING APT MODULE WITH VARIABLES
                             HOST SCOPE VARIABLES                                
                             Here  we alredy create a file group_vars in server this playbook takes vaariables from that file 
                             it's works on server grouping 
       
             CREATING ON SINGLE SERVER 
             
playbook9.yml      =        Creating user with variables ON SERVER 1 USING USER MODULE        
                             name, password, uid, home, comment, shell.

                      LOOPS
                      
playboiok10.yml    =       Installing s/w's with loops USING APT MODULE 
                           S/W'S with lops like tree, maven, git.



 
                    WITH_ITEMS


playbook11.yml     =       Installing/Uninstall/Upgrading Multiple S/W using WITH_ITEMS in all hosts 
                           in with_items we mentioned  Install TREE , Uninstall git , Upgrade git to latest veraion 

playbook12.yml     =       Installing tomcat9 tomcat9-admin S/W using with_items  USING APT MODULE
                           Copying tomcat.uders.xml file into /etc/tomcat9 destination USING COPY MODULE
                           Changing port no 8080 to 9090  in file /etc/tomcat9/servers.xml USING REPLACE MODULE
                           Restarting tomcat9 service USING SERVICE MODULE
                           Pause 40 sec for restart tomcat9  USING PAUSE MODULE 
                           Checking tomcat9 is reachable or not in 4 hosts with port no 9090 USING URI MODULE


                    HANDLERS


playbook14.yml       =      Installing appache2  USING APT MODULE
                            Copying  "Wellcome madhavarao"  to /var/www/html/index.html file USING COPY MODULE
                            Restart appache2  USING SERVICE MODULE 
                            -->  Here handler excute only when copy module can made any changes 
                                 Because handelers are excuted if a module in the keyword  is sucessfull and its has made changes 
                            -->  IN THIS PLAYBOOK12.YML 
                                 if you run 1st time it will run APT, COPY,SERVICE MODULES
                                 if you run 2nd time it will run only  APT, COPY,Because of handelers
                                 HANDELERS can run only if made changes

playbook144.ym         =    Installing appache2  USING APT MODULE
                            Copying  "Wellcome madhavarao"  to /var/www/html/index.html file USING COPY MODULE
                            HANDELERS can run only if made changes
                            SERVICE AND URI MODUKLES work when copy module make any changes on appache2 s/w
                            Restart appache2  USING SERVICE MODULE 
                            Check apache2 is reachable or not in all hosts USING  URI MODULE with WITH_ITMES 


                  TAGS 


                           TAGS ARE NOTHING BUT ALIAS ( NICKNAME ) 
                           --> the advantages of tags you will get more module controll on the playbook excutions 
                           --> to run specific module in the playbook use tags

playbook15.yml        =     Installing tree USING APT  MODULE IN ALL HOSTS  AND ADD TAG  INSTALLATION TREE
                            Creating user USING USER MODULE IN ALL HOSTS  AND ADD   TAG  USER_CREATION 
                            Copy paaswd file /etc/paaswd in to /tmp folder  USING COPY MODULE 

                    Taging is helping you to either run entire playbook ( or ) specifically only sertian module you want 
                    To selected modules you want To select and excute . 
                    That is the main purpose of taging

                     1) TO RUN ONLY TAGGED MODULES IN PLAYBOOK 
                       ansible-playbook playbook15.yml -b  --tags="tagged"

                     2) TO RUN  ONLY UNTAGGED MODULES IN PLAYBOOK 
                      ansible-playbook playbook15.yml -b  --tags="untagged" 

                    3) TO RUN ONLY SPECIFIC TAGGED MODULE  IN  A PLAYBOOK
                      ansible-playbook playbook15.yml -b  --tags="tagname"


               REMOVE -b


palybook112.yml      =    Removing -b in excution of playbook. ( command promt )
                          ADDING became: yes BETWEEN HOSTS AND TASKS section 
                          Instal;ling tree  USING APT MODULE
                          Now we dont need to give -b in excution of playbok 
                         
                          ansible-playbook playbook15.yml 

                  VAULT

                        ansible has security feature that is vault securing playbooks from others setting passwords for playbooks in playbook
                        FRIST we need create VAULT WITH THE NAME OF POLAYBOOK (PALYBOPOK16.YML)
                        ansible-vault  create playbok16.yml 
                        set password 

playbook16.yml        =    Creating user MADHAV   USING USERR MODULE 
                           Now if you want see this plqaybook its shows encrypeted data 
                            -->  To see  playbook 
                                 ansible-vault veiw playbook16.yml
                 
                    JENKINS 


                     FIRST WE NEED TO GROUP SERVERS JENKINS FOR I SERVER (GROUP IT LIKE JENKINSSERVER ) FOR QA AND PROD  2 SERVERS (GROUP IT LIKE SERVERS)

playbook17.yml        =    Installing jenkins = git, maven, java S/W  in JENKINSSERVSER  USING APT MODULE  WITH with_items and
                           Checking if jenkins rechable or  not USING URI MODULE
                           Installing tomcat9, tomcat9-admin   S/W IN SERVERS USING APT MODULE WITH with_items
                           Copying tomcatusers.xml file in to /etc/tomcat9
                           Restareting tomcat9 USING SRVICE MODULE  WHEN  COPY MODULE HAVE MADE ANY CHANGES  
                           HERE WE ADD HANDELERS  


                   INCLUDE MODULE 

                         INCLUDE MODULE used to call CHILDPLAYBOOKS from PARENTPLAYBOOK
                         --> IF playbook have anly module that is child playbook 
                         --> These playbooks you want to call from a another playbook That is parent palybook


playbook18.yml          =      Copying paaswd file IN TO /etc/passwd  USING COPY MODULE THROUGH CHILD PALYBOOK

paybook19.yml           =      CALLING CHILD PALYBOOK  FROM PARENT PLAYBOOK WITH Include-tasks



              CONFIGURING APPACHE2 USING CHILD PLAYBOOKS 


install_appache2.yml    =      Installing appache2 USING APT MODULE  IN CHILD PLAYBOOK 

edit_indec.yml          =      Replacing content with "madhavhai" dest: /var/wwww/html/index.html  USING COPY MODULE IN CHILD PLAYBOOK

Restsrt.yml             =      Restsrting apache2  USING SERVICE MODULE IN CHILD PLAYBOOK

Check_apache-response.yml =    Checking apache2 response in all Hosts WITH with_items  USING URI MODULE IN CHILD PLAYBOOK

CONFIGURING_APACHE.YML  =     Calling CHILD PLAYBOOKS from PARENT PLAYBOOK WITH with_items 


                     ADVANTAGES
                     --> When youn creating CHILD PLAYBOOK dont you think the same playbook call in tommarow in another PARENT PLAYBOOK
                     --> We can use CHILD PLAYBOOK N number of times in different parent playbook


                   WHEN CONDITIONS

                         --> WHEN =  Calls programming langauge people call IF
                         --> IF means if a condition is true  you do some activity orther wise dont do that
                         --> IF = WHEN  in ansible 
                         --> WHEN  means if a condition is true  you do some activity orther wise dont do that

playbook20.yml           =     Install tree in all hosts WHEN a == 0 USING APT MODULE


                  STAT MODULE 

                    --> This is mainly used to capturing the information about files and folders 
                         ( Ex:- who creates that file , when it was created . this information captured by STAT)

olaybook21.yml          =     Check if F1 folder is present or not IF there is no nthat filt create f1 folder  USING STST MODULE 
                              Display above module information  USING DEBUG  MODULE 

                        I WANT ANSIBLE TO DELETE A FILKE IF ITS HAQS EXUCUTE PERMISSIONS  
                        NOW I WANT PUT PERMISIONS FOR A FILE IN HOST1 EXUCUTE PERMMISION 
                          ansible  IP of host1 -m file -a 'name=/home/tmp/f1 mode=770' -b

playbook22.yml         =      Deleting file1 if it has exucute permissions
                              Capturing data from file1 USING STAT MODULE
                              Displaying information above module USING DEBUG MODULE 
                              IF THAT FILE HAVE EXCUTE PERMISSIONS
                              Deleting file have permissions USING FILE MODULE

CI-CD.yml              =     Build jenkins job using Ansible playbooks 
                             Refer notes for detailed information  (. .)  (●'◡'●)   ( *︾▽︾)
