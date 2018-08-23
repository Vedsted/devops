# Pipeline

This assignment is more or less the result of [the ca-project](https://github.com/praqma-training/ca-project)

You are welcome to use your own project and set it up with the process described in the project.

## Requirements

* Pipeline should be _as code_ alongside the code
* The pipeline should have stages on at least two different nodes.
* It should be possible to download the newest artifact from Jenkins webpage
* All builds must be run in a docker container
* If at all possible, you should produce both the binaries, as well as a docker image on docker hub.
* You should use a pretested integration workflow (pull-request with build qualification, or the Pretested integration flow).

## Hand in

* Link to the running Jenkins server
* Link to the Git repository where the code is
* A description of your pipeline, and any problems that you run into during development.




<br>

# Solution

### Github Repository
https://github.com/Vedsted/ca-project

### Jenkins build server
IP: 52.59.220.156:8080

username: admin  
password: admin

### Waffle IO 
link: https://waffle.io/Vedsted/ca-project/join

## Problems encountered
* Used port 80 by accident where Jenkins occupied the port.  
    * This took quite a long time to figure out due to the poor error messages.

* The python interpreter version in the docker image made the app.py unable to execute, due to the wrong imports being installed.


* We have discussed whether or not to have the whole python application to be added to the  docker image, or if we should **volume in** the application at **run-time** (REF-1). For the unit-tests it was decided to volume the applicatoin into a base-image containing the required environment. This was desided because it eliminates the need to build a new docker-image each time a developer commits a change. By doing this, it allows a faster feedback loop from the tests. When the application needs to be testet at a staging/production environment, it is desireble to actually make the application-files a part of the image, because this is the image that should be shipable upon release.


* We had a small pibeline up and running relatively easy. The hard part was to get the whole pipeline up and running from the commit to actually deploying the docker image to docker hub. The reason for this, were the many small changes to the Jenkinsfile and the `deploy-image.sn` script, wich took a long time fine adjust and test.

### Refs:

(REF-1) https://stackoverflow.com/questions/24958140/what-is-the-difference-between-the-copy-and-add-commands-in-a-dockerfile

### Pipeline description
We have built a pipeline wich looks at the git repository for new *ready-branches*. The pipeline is configured to utilize the Jenkinsfile in the project. Furthermore the pipeline is configured to run using multiple nodes for different tasks. The Jenkinsfile is a groovy-script that carries out all the stages made, wich are described roughly in the sequential order below:


* Preparation - Node 1
    * This step will looks for branches matching the pattern \*\*/ready/\*\*. If a branch is found, the build server will pull the branch into the working directory.

* Unit-Tests
    * This step will pulls the latest *base* docker image with the required environment for running the tests. When the image is ready, a docker container will be started and will run the `tests.py` script. 

* Push-VC
    * This step utilizes the PretestedIntegration plugin from Praqma. The plugin merges the *ready-branch* into the *master-branch* if there is no merge-conflicts, ie. trying a fast-forward merge.

* Deploy-test - Node 2
    * This node and stage pulls the latest base docker image, and start a container were the whole application is volumed in. This is done in order to start the web-server directly by running the `run.py`. A smoke-test is then made by running curl on the URL where the web-server is hosted.

* Publish image - Master node (privileged)
    * This node and step is running a custom made deployment-script that builds the whole application into a new docker image, wich then can be run from anywhere using docker. The script finishes off by pushing the new image to be available on https://hub.docker.com/r/vedsted/codechan/ .

Some of the stages are run of different nodes, where publish image has elevated priveleges to eg push images to docker hub.


