# Elastic stack (EFK) on Docker

EFK本地部署测试，监听本地电脑一些相关信息，学习ES使用

---

## 服务启动

```sh
docker compose up setup
```

```sh
docker compose up
```

---

## Requirements

### Host setup

* [Docker Engine][docker-install] version **18.06.0** or newer
* [Docker Compose][compose-install] version **2.0.0** or newer
* 1.5 GB of RAM

> [!NOTE]
> Especially on Linux, make sure your user has the [required permissions][linux-postinstall] to interact with the Docker
> daemon.

By default, the stack exposes the following ports:

* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana

> [!WARNING]
> Elasticsearch's [bootstrap checks][bootstrap-checks] were purposely disabled to facilitate the setup of the Elastic
> stack in development environments. For production setups, we recommend users to set up their host according to the
> instructions from the Elasticsearch documentation: [Important System Configuration][es-sys-config].


## Usage

> [!WARNING]
> You must rebuild the stack images with `docker compose build` whenever you switch branch or update the
> [version](#version-selection) of an already existing stack.

### Bringing up the stack

Clone this repository onto the Docker host that will run the stack with the command below:

```sh
git clone https://github.com/zhaozhiwei1992/docker-efk.git
```

Then, initialize the Elasticsearch users and groups required by docker-elk by executing the command:

```sh
docker compose up setup
```

If everything went well and the setup completed without error, start the other stack components:

```sh
docker compose up
```

> [!NOTE]
> You can also run all services in the background (detached mode) by appending the `-d` flag to the above command.

Give Kibana about a minute to initialize, then access the Kibana web UI by opening <http://localhost:5601> in a web
browser and use the following (default) credentials to log in:

* user: *elastic*
* password: *changeme*

为方便测试，默认已经关掉了es安全认证，需要开启调整elasticsearch.yml文件

## 参考

https://github.com/deviantony/docker-elk.git
