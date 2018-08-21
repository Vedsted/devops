# Setting up Toilet-Ubuntu

1. create dockerfile 

2. dockerfile contains the following:
    ```docker
    FROM ubuntu:18.04
    RUN apt-get update -y && apt-get upgrade -y && apt-get install toilet -y
    CMD toilet -F border --gay
    ```

3. create docker image  
    ```docker build vedsted/toilet:latest```

4. run image  
    ```docker run -ti vedsted/toilet:latest```

4. push image to docker hub  
    ```docker push vedsted/toilet:latest```