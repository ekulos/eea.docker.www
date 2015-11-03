## Docker orchestration for EEA main portal

Docker orchestration for EEA main portal services

### Installation

1. Install [Docker](https://www.docker.com/).

2. Install [Docker Compose](https://docs.docker.com/compose/).

3. Install [Rancher Compose](https://github.com/rancher/rancher-compose)


### Usage

Make sure you have the appropriate labels on the docker hosts in your Rancher cluster (see docker-compose.yml).

Go to your Rancher Web interface and generate your API key (API & Keys for "..." Environment):

    $ export RANCHER_URL=<(Endpoint URL)>
    $ export RANCHER_ACCESS_KEY=<(ACCESS KEY)>
    $ export RANCHER_SECRET_KEY=<(SECRET KEY)>

    $ git clone https://github.com/eea/eea.docker.www.git
    $ cd eea.docker.www
    $ rancher-compose up

## Copyright and license

The Initial Owner of the Original Code is European Environment Agency (EEA).
All Rights Reserved.

The Original Code is free software;
you can redistribute it and/or modify it under the terms of the GNU
General Public License as published by the Free Software Foundation;
either version 2 of the License, or (at your option) any later
version.


## Funding

[European Environment Agency (EU)](http://eea.europa.eu)
