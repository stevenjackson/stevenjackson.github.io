http://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/


* RUN executes command(s) in a new layer and creates a new image. E.g., it is often used for installing software packages.
* CMD sets default command and/or parameters, which can be overwritten from command line when docker container runs.
* ENTRYPOINT configures a container that will run as an executable.

* Use RUN instructions to build your image by adding layers on top of initial image.
* Prefer ENTRYPOINT to CMD when building executable Docker image and you need a command always to be executed. Additionally use CMD if you need to provide extra default arguments that could be overwritten from command line when docker container runs.
* Choose CMD if you need to provide a default command and/or arguments that can be overwritten from command line when docker container runs.
