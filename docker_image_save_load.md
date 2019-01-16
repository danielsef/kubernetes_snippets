

######################################## SAVE IMAGE ######################################

docker image save -o alpine.tar alpine:latest


######################################## LOAD IMAGE #######################################

$ ls
alpine.tar

$ docker load < alpine.tar

92fd6: Loading layer [==================================================>]  4.672MB/4.672MB
Loaded image: alpine:latest

$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              196d12cf6ab1        4 months ago        4.41MB














