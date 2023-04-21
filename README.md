This repository will hold the files necessary to finish the recruitment task.



Important note for later:

As with tasks' intent, I wanted to keep the original docker-compose.yml config provided by docker tutorial.
It has a hardcoded volume mount of "./:/app".
In order to mount current directory, I have to keep the docker-compose.yml there.
Due to ansible docker_compose module limitations, I cannot keep the docker-compose.yml and workdir (actual pwd workdir) separate. Hence, docker-compose.yml unnecessary gets mounted into actual app container.
This is unintended and would be unsafe in real life, because docker-compose.yml could hold protected values like passwords to DBS."
