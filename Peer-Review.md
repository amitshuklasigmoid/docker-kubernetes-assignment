# Peer Review

## Dhruv's Review

**TASK 1**
- Used the official airflow docker compose file available online.
- Made a postgres connection in the Airflow UI.
- Used Postgres operator for creating table and inserting values in it.

**TASK 2**
- Installed minikube to create kubernetes cluster.
- Created a pod containing postgres container using postgres deployment file.
- Went inside the container using bash.
  ```bash
  kubectl apply -f postgres-deployment.yaml
  minikube ssh
  docker exec -it -u root postgres-container-id /bin/bash
  ```
- Ran a bash script to install airflow and intialise a database and user.
- Created a postgres service to access postgres, ran an airflow deployment file to create a pod containing airflow container and finally created an airflow service to access the airflow container inside the pod.
- Went inside the airflow container and created dag containing code.
- Accessed the airflow webserver on localhost using `minikube service airflow`.

----

## Rithish's Review

**TASK 1**
- Established a connection to a PostgreSQL database within the Airflow user interface.
- Created airflow on docker by using the official docker compose file.
- Two tasks - one for creating table and other for inserting values were created using Postgres Operator.

**TASK 2**
- Set up a kubernetes cluster by installing minikube.
- Utilized the deployment file of postgres to create a postgres container inside a pod.
- Installed airflow and initialized a database and a user in the postgres container. Finally created a service to access the container.
- Similarly made a deployment and service for airflow as well. Put the dags in the airflow scheduler by going inside it and creating the dags using vim.
- Established a connection to localhost and access airflow and ran the dags.
