# Go feat. Nebula Graph

This project uses the Nebula Go driver to interface with Nebula Graph 1.0.

The client example is adjusted from [here](https://github.com/vesoft-inc/nebula-go/blob/master/example/graph_client_example.go).

## Nebula Graph

The Nebula Graph database consists of four components:

- The Storage Service,
- the Metadata Service,
- the Query Engine Service and
- the Client.

![Nebula Architecture](.readme/nebula-architecture.jpg)

The [docker-compose.yml](docker-compose.yml) setup is taken from
[here](https://github.com/vesoft-inc/nebula-docker-compose/tree/v1.0); take
care not to accidentally use the experimental 2.0 branch. 
All three services described above are started with three replicas each,
however the image version was changed from `nightly` to a fixed tag.
