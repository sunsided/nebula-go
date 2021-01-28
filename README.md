# Go feat. Nebula Graph

This project uses the Nebula Go driver to interface with Nebula Graph 1.0.

The client example is adjusted from [here](https://github.com/vesoft-inc/nebula-go/blob/master/example/graph_client_example.go).

## Local Setup

To start Nebula, run

```bash
docker-compose up
```

Note that this setup uses Docker network `172.29.0.0/16`.
If that doesn't fit, changes to [docker-compose.yml](docker-compose.yml) are required.

## Nebula Graph

The Nebula Graph database consists of four components:

- The Storage Service,
- the Metadata Service,
- the Query Engine Service and
- the Client.

![Nebula Architecture](.readme/nebula-architecture.jpg)

The [docker-compose.yml](docker-compose.yml) setup is taken from
[here](https://github.com/vesoft-inc/nebula-docker-compose/tree/v1.0). 
All three services described above are started with three replicas each,
however the image version was changed from `nightly` to a fixed tag.

### Web UI

After starting the services with Docker Compose, visit the following
address in your Browser:

- [http://localhost:7001/?lang=EN_US](http://localhost:7001/?lang=EN_US)

From there, connect to the running database using:

- Host: `<your IP>:3699`
- User: `user`
- Password: `password`

Note that you _must_ use the IP of your host machine. Using either
`localhost` or `127.0.0.1` will not work.
