

######################################## SAVE IMAGE ######################################




######################################## LOAD IMAGE #######################################

sciencebox:~/repos/docker  $ pwd
/home/vagrant/repos/docker
sciencebox:~/repos/docker  $ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
sciencebox:~/repos/docker  $ ls
alpine.tar
sciencebox:~/repos/docker  $ docker load < alpine.tar
df64d3292fd6: Loading layer [==================================================>]  4.672MB/4.672MB
Loaded image: alpine:latest
sciencebox:~/repos/docker  $ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              196d12cf6ab1        4 months ago        4.41MB














