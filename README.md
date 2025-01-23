# 阿腾运维知识库网站

- 网站管理员：[阿腾](http://wpa.qq.com/msgrd?v=3&uin=2385569970&Menu=yes)

> 如果左侧点击无反应需要刷新以下页面哦~~

## 概述

欢迎来到阿腾的运维知识库网站！

## 目录

- Linux Service
    - 服务器配置
        - [基础配置](/work/service/00-basic/)
        - [网络配置](/work/service/network/)
        - [升级OpenSSH](/work/service/openssh/v9.9/)
    - 存储服务
        - [网络文件共享 NFS](work/service/nfs/)
        - [网络文件共享 Samba](work/service/samba/)
        - [网络文件共享 VSFTP](work/service/ftp/)
        - 对象存储服务 MinIO
            - [安装文档](/work/service/minio/v20241107/)
            - [使用文档](/work/service/minio/OPS.md)
        - 分布式存储 JuiceFS
            - [安装文档](/work/service/juicefs/v1.2.1/)
            - [使用文档](/work/service/juicefs/OPS.md)
        - [备份工具 Restic](/work/service/restic/)
    - 数据存储
        - MySQL
            - [安装文档](/work/service/mysql/v8.4.3/)
            - [编译安装文档](/work/service/mysql/v8.4.3/make/)
            - [使用文档](/work/service/mysql/OPS.md)
        - MariaDB Galera
            - [安装文档](/work/service/mariadb/v11.4.4/)
        - Redis
            - [安装文档](/work/service/redis/v7.4.1/)
            - [使用文档](/work/service/redis/OPS.md)
        - PostgreSQL
            - [编译安装文档](/work/service/postgresql/v17.2.0/)
            - [编译PostGIS](/work/service/postgresql/v17.2.0/postgis/)
            - [使用文档](/work/service/postgresql/OPS.md)
        - ETCD
            - [安装文档](/work/service/etcd/v3.5.17/)
            - [使用文档](/work/service/etcd/OPS.md)
        - FoundationDB
            - [安装文档](/work/service/foundationdb/v7.1.38/)
            - [使用文档](/work/service/foundationdb/OPS.md)
        - ElasticSearch
            - [安装单机模式](/work/service/elastic/elasticsearch/standalone/)
            - [安装集群模式](/work/service/elastic/elasticsearch/cluster/)
        - OpenSearch
            - [1.x安装文档](/work/service/opensearch/v1.3.19/)
            - [2.x安装文档](/work/service/opensearch/v2.18.0/)
            - [使用文档](/work/service/opensearch/OPS.md)
    - Web服务
        - Nginx
            - [安装文档](/work/service/nginx/v1.27.3/)
            - [使用文档](/work/service/nginx/OPS.md)
        - Haproxy
            - [安装文档](/work/service/haproxy/)
            - [使用文档](/work/service/haproxy/OPS.md)
        - TLS证书
            - [cfssl创建证书](/work/service/tls/tls-cfssl/v1.6.5/)
            - [openssl创建证书](/work/service/tls/tls-openssl/)
    - 其他服务
        - [内网穿透FRP](/work/service/frp/)
        - [CoreDNS](/work/service/coredns/)
    - 开发工具
        - OpenJDK
            - [OpenJDK8](/work/service/openjdk/openjdk8/)
            - [OpenJDK11](/work/service/openjdk/openjdk11/)
            - [OpenJDK17](/work/service/openjdk/openjdk17/)
            - [OpenJDK21](/work/service/openjdk/openjdk21/)
            - [使用文档](/work/service/openjdk/OPS.md)
- Shell
    - Spring
        - [应用管理](work/shell/java/)
    - 服务备份脚本
        - [mysql](work/shell/backups/mysql/)
        - [postgresql](work/shell/backups/postgresql/)
        - [etcd](work/shell/backups/etcd/)
        - [minio](work/shell/backups/minio/)
        - [mongodb](work/shell/backups/mongodb/)
- Docker
    - 使用文档
        - [Docker使用文档](/work/docker/OPS.md)
    - 安装文档
        - [Docker安装文档](/work/docker/deploy/v27.3.1/)
    - Dockerfile
        - [jdk21](/work/docker/dockerfile/java/debian/jdk21/)
        - [springboot app](/work/docker/dockerfile/java/debian/application/jdk21/)
    - 服务安装文档
        - [mysql](/work/docker/service/mysql/)
        - [postgresql](/work/docker/service/postgresql/)
        - [doris](/work/docker/service/doris/)
        - [redis](/work/docker/service/redis/)
        - [kafka](/work/docker/service/kafka/)
        - [kafka-ui](/work/docker/service/kafka-ui/)
        - [minio](/work/docker/service/minio/)
        - [mongodb](/work/docker/service/mongodb/)
        - [rabbitmq](/work/docker/service/rabbitmq/)
        - [gitea](/work/docker/service/gitea/)
        - [gitlab](/work/docker/service/gitlab/)
        - [zookeeper](/work/docker/service/zookeeper/)
        - [windows](/work/docker/service/windows/)
        - [elasticsearch](/work/docker/service/elasticsearch/)
        - [opensearch](/work/docker/service/opensearch/)
        - [elastic-view](/work/docker/service/elastic-view/)
        - [jenkins](/work/docker/service/jenkins/)
        - [jumpserver](/work/docker/service/jumpserver/)
- Kubernetes
    - 使用文档
        - [K8S使用文档](/work/kubernetes/OPS.md)
    - 安装文档
        - [kubekey](/work/kubernetes/deploy/kubekey/v3.1.7/)
        - [kubesphere3](/work/kubernetes/deploy/kubesphere/v3.4.1/)
        - [kubesphere4](/work/kubernetes/deploy/kubesphere/v4.1.2/)
        - [kubeadm](/work/kubernetes/deploy/kubeadm/v1.23.12/)
        - [kubevirt](/work/kubernetes/deploy/kubevirt/deploy/v1.3.0/)
    - 镜像仓库
        - [Harbor](/work/kubernetes/deploy/harbor/v2.12.0/)
        - [Registry](/work/kubernetes/deploy/harbor/registry/)
    - 存储服务
        - openebs
            - [localpv](/work/kubernetes/deploy/storage/openebs/localpv-provisioner/v4.1.0/)
            - [nfs](/work/kubernetes/deploy/storage/openebs/nfs-provisioner/v0.11.0/)
        - nfs
            - [nfs-client](/work/kubernetes/deploy/storage/nfs/nfs-client/)
            - [nfs-server](/work/kubernetes/deploy/storage/nfs/nfs-server/)
        - juicefs-csi
            - [juicefs-csi](/work/kubernetes/deploy/storage/juicefs-csi/v0.24.4/)
        - rook
            - [ceph](/work/kubernetes/deploy/storage/rook/ceph/)
            - [nfs](/work/kubernetes/deploy/storage/rook/nfs/)
        - longhorn
            - [longhorn](/work/kubernetes/deploy/storage/longhorn/v1.4.0/)
        - kadalu
            - [kadalu](/work/kubernetes/deploy/storage/kadalu/v1.0.0/)
    - 中间件服务
        - 数据存储
            - Redis
                - [单机模式](/work/kubernetes/service/redis/v7.4.1/standalone/)
                - [主从模式](/work/kubernetes/service/redis/v7.4.1/replication/)
                - [哨兵模式](/work/kubernetes/service/redis/v7.4.1/sentinel/)
                - [集群模式](/work/kubernetes/service/redis/v7.4.1/cluster/)
            - Mariadb Galera
                - [Galera集群](/work/kubernetes/service/mariadb/v11.4.4/)
            - PostgreSQL
                - [单机模式](/work/kubernetes/service/postgresql/v17.2.0/standalone/)
                - [主从模式](/work/kubernetes/service/postgresql/v17.2.0/replication/)
                - [集群模式](/work/kubernetes/service/postgresql/v17.2.0/ha/)
            - MongoDB
                - [单机模式](/work/kubernetes/service/mongodb/v8.0.3/standalone/)
                - [副本集群模式](/work/kubernetes/service/mongodb/v8.0.3/replicaset/)
                - [分配集群模式](/work/kubernetes/service/mongodb/v8.0.3/sharded/)
            - MySQL
                - [单机模式](/work/kubernetes/service/mysql/v8.4.3/standalone/)
                - [主从模式](/work/kubernetes/service/mysql/v8.4.3/replication/)
                - [配置metrics](/work/kubernetes/service/mysql/v8.4.3/metrics/)
            - Doris
                - [集群模式2](/work/kubernetes/service/doris/v2.1.7/)
                - [集群模式3l](/work/kubernetes/service/doris/v3.0.3/)
            - Clickhouse
                - [集群模式](/work/kubernetes/service/clickhouse/v23.12.2/)
            - ElasticSearch7
                - [单机模式](/work/kubernetes/service/elasticsearch/v7.17.26/all-in-one/)
                - [认证模式](/work/kubernetes/service/elasticsearch/v7.17.26/auth/)
                - [HTTPS模式](/work/kubernetes/service/elasticsearch/v7.17.26/https/)
                - [HTTPS模式(自定义证书)](/work/kubernetes/service/elasticsearch/v7.17.26/https-custom/)
                - [Kibana](/work/kubernetes/service/kibana/v7.17.26/)
                - [Elastic View可视化](/work/kubernetes/service/elasticsearch/elastic-view/)
            - ElasticSearch8
                - [单机模式](/work/kubernetes/service/elasticsearch/v8.16.1/all-in-one/)
                - [认证模式](/work/kubernetes/service/elasticsearch/v8.16.1/auth/)
                - [HTTPS模式](/work/kubernetes/service/elasticsearch/v8.16.1/https/)
                - [HTTPS模式(自定义证书)](/work/kubernetes/service/elasticsearch/v8.16.1/https-custom/)
                - [Kibana](/work/kubernetes/service/kibana/v7.17.26/)
                - [Elastic View可视化](/work/kubernetes/service/elasticsearch/elastic-view/)
            - OpenSearch1
                - [单机模式](/work/kubernetes/service/opensearch/v1.3.19/all-in-one/)
                - [HTTPS模式(自定义证书)](/work/kubernetes/service/opensearch/v1.3.19/https-custom/)
                - [Elastic View可视化](/work/kubernetes/service/opensearch/elastic-view/)
            - OpenSearch2
                - [单机模式](/work/kubernetes/service/opensearch/v2.18.0/all-in-one/)
                - [HTTPS模式](/work/kubernetes/service/opensearch/v2.18.0/https/)
                - [HTTPS模式(自定义证书)](/work/kubernetes/service/opensearch/v2.18.0/https-custom/)
                - [Elastic View可视化](/work/kubernetes/service/opensearch/elastic-view/)
            - ETCD
                - [集群模式](/work/kubernetes/service/etcd/v3.5.17/basic/)
                - [认证模式](/work/kubernetes/service/etcd/v3.5.17/http-auth/)
                - [HTTPS模式](/work/kubernetes/service/etcd/v3.5.17/https/)
            - FoundationDB
                - [安装文档](/work/kubernetes/service/foundationdb/v7.1.38/)
        - 消息队列
            - RabbitMQ
                - [集群模式](/work/kubernetes/service/rabbitmq/v4.0.2/)
            - Kafka
                - [单机模式](/work/kubernetes/service/kafka/v3.8.1/standalone/)
                - [集群模式](/work/kubernetes/service/kafka/v3.8.1/cluster/)
                - [高可用集群模式](/work/kubernetes/service/kafka/v3.8.1/cluster-ha/)
                - [认证模式](/work/kubernetes/service/kafka/v3.8.1/auth/)
            - Kafka UI
                - [Kafka可视化](/work/kubernetes/service/kafka-ui/v0.7.2/)
        - 存储服务
            - MinIO
                - [单机模式](/work/kubernetes/service/minio/v2024.11.7/standalone/)
                - [集群模式](/work/kubernetes/service/minio/v2024.11.7/distributed/)
            - Harbor
                - [http模式](/work/kubernetes/service/harbor/v2.12.0/http/)
                - [ingress模式](/work/kubernetes/service/harbor/v2.12.0/ingress-http/)
                - [https模式](/work/kubernetes/service/harbor/v2.12.0/https/)
                - [https模式(自定义证书)](/work/kubernetes/service/harbor/v2.12.0/https-custom/)
        - 开发工具
            - [Spring Boot应用](/work/kubernetes/service/springboot-app/v1.1/)
            - [Gitlab](/work/kubernetes/service/gitlab/v17.6.1/)
            - [Gitea](/work/kubernetes/service/gitea/v1.22.3/)
            - [Jenkins](/work/kubernetes/service/jenkins/v2.479.1/baseic/)
            - [Snail-Job](/work/kubernetes/service/snail-job/v1.2.0/)
            - [PowerJob](/work/kubernetes/service/powerjob/)
            - [Spring Boot Admin](/work/kubernetes/service/springboot-admin/v3.3.0/)
            - [Nacos](/work/kubernetes/service/nacos/v2.4.0/)
            - [Seata](/work/kubernetes/service/seata/v2.0.0/)
            - [Sentinel](/work/kubernetes/service/sentinel/)
            - [SkyWalking](/work/kubernetes/service/springboot-admin/v3.3.0/)
            - [禅道](/work/kubernetes/service/zentao/v20.7.1/)
            - [Sonarqube](/work/kubernetes/service/sonarqube/v10.7.0/)
        - 大数据
            - [Zookeeper](/work/kubernetes/service/zookeeper/v3.9.3/)
            - [Flink](/work/kubernetes/service/flink/v1.19.1/)
            - [Spark](/work/kubernetes/service/spark/v3.5.4/)
            - [DolphinScheduler](/work/kubernetes/service/dolphinscheduler/v3.2.2/)
            - Doris2
                - [集群模式](/work/kubernetes/service/doris/v2.1.7/)
            - Doris3
                - [集群模式](/work/kubernetes/service/doris/v3.0.3/)
        - 负载均衡和网络
            - [MetalLB](/work/kubernetes/service/metallb/v0.14.8/)
            - [External-DNS](/work/kubernetes/service/external-dns/v0.15.0/)
            - [HAProxy](/work/kubernetes/service/haproxy/v3.0.2/)
            - [Nginx](/work/kubernetes/service/nginx/v1.27.0/)
            - [Multus-CNI](/work/kubernetes/service/multus-cni/)
        - 其他
            - [Cert-Manager](/work/kubernetes/service/cert-manager/v1.16.2/)
            - [安装Windows系统](/work/kubernetes/service/windows/)
            - [Stirling-PDF](/work/kubernetes/service/Stirling-PDF/)
        - KubeBlocks
            - [安装](/work/kubernetes/service/kubeblocks/deploy/)
            - [mysql](/work/kubernetes/service/kubeblocks/service/mysql/)
            - [postgresql](/work/kubernetes/service/kubeblocks/service/postgresql/)
            - [redis](/work/kubernetes/service/kubeblocks/service/redis/)
            - [kafka](/work/kubernetes/service/kubeblocks/service/kafka/)
            - [备份](/work/kubernetes/service/kubeblocks/backup/)
        - 堡垒机
            - [JumpServer](/work/kubernetes/service/jumpserver/v4.3.1/)
            - [Nexterm](/work/kubernetes/service/nexterm/v1.0.2/)
        - 共享文件
            - [kodbox](/work/kubernetes/service/kodbox/v1.52/)
    - 备份服务
        - velero
            - [安装备份和恢复Velero](/work/kubernetes/deploy/backups/velero/v1.11.0/)
        - etcd
            - [备份到本地](/work/kubernetes/deploy/backups/etcd/local/)
            - [备份到MinIO](/work/kubernetes/deploy/backups/etcd/minio/)
        - mysql
            - [备份到本地](/work/kubernetes/deploy/backups/mysql/local/)
            - [备份到MinIO](/work/kubernetes/deploy/backups/mysql/minio/)
        - postgresql
            - [备份到本地](/work/kubernetes/deploy/backups/postgresql/local/)
            - [备份到MinIO](/work/kubernetes/deploy/backups/postgresql/minio/)
    - 服务测试
        - [存储测试](/work/kubernetes/deploy/test/storage/)
        - [网络测试](/work/kubernetes/deploy/test/network/)
- KVM
    - [使用文档](work/kvm/)
- 大数据
    - 基础服务
        - 基础配置
            - [基础配置](work/bigdata/00-basic/)
        - JDK
            - [安装OpenJDK8](/work/bigdata/01-jdk/)
        - Zookeeper
            - [单机](work/bigdata/02-zookeeper/standalone/)
            - [集群](work/bigdata/02-zookeeper/cluster/)
            - [使用文档](work/bigdata/02-zookeeper/OPS.md)
        - Hadoop
            - [单机](work/bigdata/03-hadoop/standalone/)
            - [集群](work/bigdata/03-hadoop/cluster/)
            - [高可用集群](work/bigdata/03-hadoop/cluster-ha/)
            - [使用文档](work/bigdata/03-hadoop/OPS.md)
        - Kafka
            - [单机](work/bigdata/03-kafka/standalone/)
            - [集群](work/bigdata/03-kafka/cluster/)
            - [高可用集群](work/bigdata/03-kafka/cluster-ha/)
            - [使用文档](work/bigdata/03-kafka/OPS.md)
    - 数据存储
        - HBase
            - [单机](work/bigdata/04-hbase/standalone/)
            - [集群](work/bigdata/04-hbase/cluster/)
            - [高可用集群](work/bigdata/04-hbase/cluster-ha/)
            - [使用文档](work/bigdata/04-hbase/OPS.md)
        - Hive
            - [单机](work/bigdata/04-hive/standalone/)
            - [集群](work/bigdata/04-hive/cluster/)
            - [高可用集群](work/bigdata/04-hive/cluster-ha/)
            - [集成TEZ](work/bigdata/04-hive/tez/)
            - [使用文档](work/bigdata/04-hive/OPS.md)
        - Doris
            - Doris v2.1.7
                - [单机](work/bigdata/05-doris/v2.1.7/standalone/)
                - [集群](work/bigdata/05-doris/v2.1.7/cluster/)
                - [高可用集群](work/bigdata/05-doris/v2.1.7/cluster-ha/)
            - Doris v3.0.3
                - [单机](work/bigdata/05-doris/v3.0.3/standalone/)
                - [集群](work/bigdata/05-doris/v3.0.3/cluster/)
                - [高可用集群](work/bigdata/05-doris/v3.0.3/cluster-ha/)
            - [使用文档](work/bigdata/05-doris/OPS.md)
        - Iceberg
            - [使用文档](work/bigdata/06-iceberg/)
    - 数据计算
        - Spark
            - [单机](work/bigdata/05-spark/standalone/)
            - [集群](work/bigdata/05-spark/cluster/)
            - [高可用集群](work/bigdata/05-spark/cluster-ha/)
            - [YARN](work/bigdata/05-spark/yarn)
            - [Kubernetes Operator](work/bigdata/05-spark/kubernetes-operator/)
            - [集成Hive](work/bigdata/05-spark/hive/)
            - [使用文档](work/bigdata/05-spark/OPS.md)
        - Flink
            - [单机](work/bigdata/05-flink/standalone/)
            - [集群](work/bigdata/05-flink/cluster/)
            - [高可用集群](work/bigdata/05-flink/cluster-ha/)
            - [YARN](work/bigdata/05-flink/yarn)
            - [Kubernetes Operator](work/bigdata/05-flink/kubernetes-operator/)
            - [Flink CDC](work/bigdata/05-flink/cdc/)
            - [使用文档](work/bigdata/05-flink/OPS.md)
    - 调度平台
        - Dolphinscheduler
            - [单机](work/bigdata/06-dolphinscheduler/standalone/)
            - [集群](work/bigdata/06-dolphinscheduler/cluster/)
- 系统和软件
    - 操作系统
        - [Windows](/work/syssoft/os/windows/)
        - [OpenEuler](/work/syssoft/os/openeuler/)
        - [CentOS](/work/syssoft/os/centos/)
    - 开发软件
        - [JDK](/work/syssoft/dev/jdk/)
        - [Maven](/work/syssoft/dev/maven/)
        - [Git](/work/syssoft/dev/git/)
        - [IntelliJ IDEA ](/work/syssoft/dev/idea/)
        - [DataGrip](/work/syssoft/dev/datagrip/)
    - 系统软件
        - [常用软件](/work/syssoft/software/primary/)
        - [其他软件](/work/syssoft/software/others/)
    - 相关文档
        - [技术文档](/work/syssoft/doc/nb/)
        - [其他文档](/work/syssoft/doc/others/)
