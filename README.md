docker-openmpi
---

[![Build Status](https://travis-ci.org/DaisukeMiyamoto/docker-openmpi.svg?branch=master)](https://travis-ci.org/DaisukeMiyamoto/docker-openmpi)

base package for docker cluster with openmpi

# with docker compose
1. set up `docker-compose`
1. generate ssh public key pair
    ```
    $ ./keygen.sh
    ```
1. build and deploy MPI cluster
    ```
    $ docker-compose build
    $ docker-compose up --scale node=4 -d
    ```
2. login to master node
    ```
    $ ./connect-master.sh
    ```
3. run mpi program from master node
    ```
    $ ./make-hostfile.sh
    $ mpirun -np 16 hostname
    252f9f5abc18
    252f9f5abc18
    252f9f5abc18
    252f9f5abc18
    fa00f144c7be
    0ebd38ff982e
    fa00f144c7be
    0ebd38ff982e
    fa00f144c7be
    0ebd38ff982e
    fa00f144c7be
    0ebd38ff982e
    4c1364ddf9d9
    4c1364ddf9d9
    4c1364ddf9d9
    4c1364ddf9d9
    ```
4. compile an application
    ```
    cd /mpi-app/hello-world/
    make 
    ```
5. run application
    ```
    mpirun -np 16 /mpi-app/hello-world/mpi_hello_world
    ```
6. shutdown cluster
    ```
    $ docker-compose down -v
    ```

# with swarm

# with kubernetes

1. set up `kubernetes`

1. start cluster
    ```
    $ kubectl create -f mpi-deployment.yml
    ```
1. login to master node
1. run mpi program
1. shutdown cluster
