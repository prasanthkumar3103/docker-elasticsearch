# ElasticSearch

Docker Image for [elasticsearch](http://www.elasticsearch.com/) based on airdock/oracle-jdk:1.8


Purpose of this image is:

- install elasticsearch server
- based on airdock/oracle-jdk:1.8 (debian)

> Name: airdock/elasticsearch

***Dependency***: airdock/oracle-jdk:1.8

***Few links***:

- [Docker Elasticsearch](https://github.com/dockerfile/elasticsearch)
- [Puckel Elasticsearch](https://github.com/puckel/dockerfiles)
- [Installation ES](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/setup-repositories.html)
- [Configuration](http://elasticsearch.org/guide/en/elasticsearch/reference/current/setup-configuration.html)



# Usage

1. You should have already install [Docker](https://www.docker.com/) and [Fig](http://www.fig.sh/) for more complex usage.
2. Download [automated build](https://registry.hub.docker.com/u/airdock/) from public [Docker Hub Registry](https://registry.hub.docker.com/):
`docker search airdock` or go directly in 3.
3. Execute redis server with default configuration:
	'docker run -d -p 9200:9200 -p 9300:9300 --name elasticsearch airdock/elasticsearch '

## Elasticsearch Configuration 

'''
	# common settings
	cluster.name: elasticsearch
	node.master: true
	node.data: true
	index.number_of_shards: 5
	index.number_of_replicas: 1
	transport.tcp.port: 9300
	transport.tcp.compress: false
	http.port: 9200
	http.jsonp.enable: false

	#Kibana 3 and Elasticsearch 1.4 - CORS problem
	http.cors.enabled: true
	http.cors.allow-origin: "*"


	path.conf: /etc/elasticsearch
	path.data: /var/lib/elasticsearch
	path.work: /tmp/elasticsearch
	path.logs: /var/logs/elasticsearch
	path.plugins: /usr/share/elasticsearch/plugins
'''

## Notes

- Configuration path: /etc/elasticsearch
- Data path: /var/lib/elasticsearch
- Log path: /var/logs/elasticsearch
- Plugins installation path: /usr/share/elasticsearch/plugins

# Change Log
 

## latest (current)

- install elasticsearch
- define ELASTICSEARCH_VERSION (1.4.3)
- add volume on data folder (/var/lib/elasticsearch) and log folder (/var/log/elasticsearch)
- default log ouput to console
- expose 9200 (http) and 9300 (transport) port
- launch elasticsearch with elasticsearch user
- default configuration is a master with node storage capability
- add plugin mobz/elasticsearch-head

# Build

Alternatively, you can build an image from [Dockerfile](https://github.com/airdock-io/docker-elasticsearch).
Install "make" utility, and execute: `make build`

In Makefile, you could retrieve this *variables*:

- NAME: declare a full image name (aka airdock/elasticsearch)
- VERSION: declare image version

And *tasks*:

- ***all***: alias to 'build'
- ***clean***: remove all container which depends on this image, and remove image previously builded
- ***build***: clean and build the current version
- ***tag_latest***: build and tag current version with ":latest"
- ***release***: execute tag_latest, push image onto registry, and tag git repository
- ***debug***: launch default command with builded image in interactive mode
- ***run***: run image as daemon and print IP address.



# License

```
 Copyright (c) 1998, 1999, 2000 Thai Open Source Software Center Ltd

 Permission is hereby granted, free of charge, to any person obtaining
 a copy of this software and associated documentation files (the
 "Software"), to deal in the Software without restriction, including
 without limitation the rights to use, copy, modify, merge, publish,
 distribute, sublicense, and/or sell copies of the Software, and to
 permit persons to whom the Software is furnished to do so, subject to
 the following conditions:

 The above copyright notice and this permission notice shall be included
 in all copies or substantial portions of the Software.

 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
 EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
 MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
 IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
 CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
 TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
 SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
