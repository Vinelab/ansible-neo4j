# Neo4j - Ansible Role
Configure & launch a new [Neo4j](http://neo4j.com) instance using [Docker](http://docker.com) containers.

#### Dependencies
You may want to setup the host with Docker before using this role, a helper role would be [ansible-docker](http://github.com/vinelab/ansible-docker)

### Installation
Add this repository as a submodule of your git with:

```
git submodule add git@github.com:Vinelab/ansible-neo4j roles/neo4j
```

Or simply clone this repository directly into your *roles* directory:

```
git clone git@github.com:Vinelab/ansible-neo4j roles/neo4j
```

### Usage
There is one required variable for this role:

- `volume` indicating the location where the data should be stored on the host

##### Quickstart

```yaml
---
roles:
    - role: neo4j
      volume: /data/db
      ram: 3GB
```

#### Configuration

Key                 | Description                           | Default
--------       | ------------------------              | ------------
image             | The image to be used to run the container. | vinelab/neo4j
name              | The container name when it runs.           | neo4j
host              | When using ambassador containers, used to connect to the database container. | localhost
ram               | The amount of ram that this container is allowed. | 2GB
port              | The port to be exposed when running the container. | 7474
volume            | The mounting point of the directory to store data in. | /neo4j
privileged        | Whether to run the container in `privileged` mode or not. | `true`
ambassador        | Indicate whether you would like to run an ambassador container or a database container. | `false`

##### Examples

###### Database

```yaml
- hosts: db
  roles:
    - role: neo4j
      volume: /data/db
      ram: 8GB
      name: db
```

###### Ambassador

```yaml
- hosts: db
  roles:
    - role: neo4j
      host: 10.0.0.9
      port: 7676
      name: db
      ambassador: true
      ram: 2GB
```

###### Custom Image

```yaml
- hosts: db
  roles:
    - role: neo4j
      image: your/neo4j
      volume: /home/data/db
      ram : 4GB
```

### Tags
All tasks have the following tags:

- neo4j
- launch
