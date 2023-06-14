# Docker Assignment
- Created a postgres connection with below configurations
<img width="1431" alt="Screenshot 2023-06-14 at 1 05 43 PM" src="https://github.com/amitshuklasigmoid/docker-kubernetes-assignment/assets/122515454/bf36b3af-9578-49fc-984c-5e583df401a9">


- This is my airflow DAG that contains two tasks, One task for creating a table and another for inserting current timestamp into this.

<img width="1439" alt="Screenshot 2023-06-14 at 1 06 18 PM" src="https://github.com/amitshuklasigmoid/docker-kubernetes-assignment/assets/122515454/bfe0560c-76e2-4644-a8b8-f33a2c65fdef">

- My table as myTime has been created successfully and current timestamp inserted successfully into my table.
<img width="914" alt="Screenshot 2023-06-14 at 1 07 28 PM" src="https://github.com/amitshuklasigmoid/docker-kubernetes-assignment/assets/122515454/d1958368-0605-490e-8848-4870673555b6">


## Kubernetes Assignment
1. Installed minikube to make a kubernetes cluster using the following commands.
```bash
brew install minikube
minikube start
```

2. Using the ```postgres-deployment.yaml``` file the pod containing postgres container was made. The following command was used,
```bash
kubectl apply -f postgres-deployment.yaml
minikube ssh
kubectl exec -it -u root postgres /bin/bash
```
Then ran the following command to initialise the database and make a user.
```bash
apt-get -y update
apt-get  -y install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget 
wget https://www.python.org/ftp/python/3.7.12/Python-3.7.12.tgz
tar -xf Python-3.7.12.tgz
cd /Python-3.7.12
./configure --enable-optimizations
make -j $(nproc)
make altinstall
# STEPS TO INSTALL AIRFLOW VERSION 2.5.0
apt-get install libpq-dev
pip3.7 install "apache-airflow[postgres]==2.5.0" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.5.0/constraints-3.7.txt"
export AIRFLOW__CORE__SQL_ALCHEMY_CONN=postgresql://airflow:airflow@localhost:5432/airflow

airflow db init
airflow users create -u airflow -p airflow -f amit -l shukla -e amitshukla@gmail.com -r Admin
```

3. Then created a service of type clusterIP by running ```postgres-service.yaml``` to give access to postgres pods inside the cluster. The following command was used.
```bash
kubectl apply -f postgres-service.yaml
```

4. Using the ```airflow-deployment.yaml``` file the pod containing airflow container was made. The following command was used,
```bash
kubectl apply -f airflow-deployment.yaml
```
5. Created a service of type loadbalancer by running ```airflow-service.yaml``` to access airflow webserver from my local system using the following command,
```bash
kubectl apply -f airflow-service.yaml
```
6. create my dag as time_task.py inside airflow scheduler
```
minikube ssh
# for creating dag
kubectl exec -it -u root airflow-scheduler /bin/bash
cd dags
#installed vim by running these commands
apt-get update
apt install vim
vim time_task.py
#copied the same above code from docker assignment dag
```


7. Accessed the airflow webserver by running the command ```minikube service airflow```. My airflow is accessible on http://127.0.0.1:54868 Upon logging in, the dag was visible, then created a postgres connection and then ran my dag, it has been succesfully executed.

<img width="758" alt="Screenshot 2023-06-14 at 1 09 15 PM" src="https://github.com/amitshuklasigmoid/docker-kubernetes-assignment/assets/122515454/059d619f-00c2-42d3-a1e1-931e73e051d7">

<img width="1440" alt="Screenshot 2023-06-13 at 5 53 51 PM" src="https://github.com/amitshuklasigmoid/docker-kubernetes-assignment/assets/122515454/00a923d7-d7df-4cda-b7a0-a8cc442c70a3">


8. Verified this by logging into the postgres container and viewing the table.
<img width="1440" alt="Screenshot 2023-06-13 at 5 55 25 PM" src="https://github.com/amitshuklasigmoid/docker-kubernetes-assignment/assets/122515454/db4c16a4-56d6-4f13-9cc9-5c7275bb19ba">

