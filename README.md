Kafka Manager
=============

A tool for managing [Apache Kafka](http://kafka.apache.org).

It supports the following :

 - Manage multiple clusters
 - Easy inspection of cluster state (topics, brokers, replica distribution, partition distribution)
 - Run preferred replica election
 - Generate partition assignments (based on current state of cluster)
 - Run reassignment of partition (based on generated assignments)

Cluster Management

![cluster](/img/cluster.png)

***

Topic View

![topic](/img/topic.png)

***

Broker View

![broker](/img/broker.png)

***

Requirements
------------

1. [Kafka 0.8.1.1 or 0.8.2-beta](http://kafka.apache.org/downloads.html)
2. [sbt 0.13.x](http://www.scala-sbt.org/download.html)
3. Java 7+

Configuration
-------------

The minimum configuration is the zookeeper hosts which are to be used for kafka manager state.
This can be found in the application.conf file in conf directory.  The same file will be packaged
in the distribution zip file; you may modify settings after unzipping the file on the desired server.

    kafka-manager.zkhosts="my.zookeeper.host.com:2181"

You can specify multiple zookeeper hosts by comma delimiting them, like so:

    kafka-manager.zkhosts="my.zookeeper.host.com:2181,other.zookeeper.host.com:2181"

Alternatively, use the environment variable `ZK_HOSTS` if you don't want to hardcode any values.

    ZK_HOSTS="my.zookeeper.host.com:2181"

Deployment
----------

The command below will create a zip file which can be used to deploy the application.

    sbt clean dist

Please refer to play framework documentation on production deployment.

If java is not in your path, or you need to build against a specific java version,
please use the following (the example assumes oracle java8):

    $ PATH=/usr/local/oracle-java-8/bin:$PATH \
      JAVA_HOME=/usr/local/oracle-java-8 \
      /path/to/sbt -java-home /usr/local/oracle-java-8 dist clean

This ensures that the 'java' and 'javac' binaries in your path are first looked up in the
oracle java8 release. Next, for all downstream tools that only listen to JAVA_HOME, it points
them to the oracle java8 location. Lastly, it tells sbt to use the oracle java8 location as
well.

Starting the service
--------------------

After extracting the produced zipfile, and changing the working directory to it, you can
run the service like this:

    $ bin/kafka-manager

By default, it will choose port 9000. This is overridable, as is the location of the
configuration file. For example:

    ./kafka-manager -Dconfig.file=../conf/application.conf
    ./kafka-manager -Dconfig.file=../conf/application.conf >/dev/null 2>&1
    $ bin/kafka-manager -Dconfig.file=/path/to/application.conf -Dhttp.port=8080

Again, if java is not in your path, or you need to run against a different version of java,
add the -java-home option as follows:

    $ bin/kafka-manager -java-home /usr/local/oracle-java-8

Credits
-------

Logo/favicon used is from [Apache Kafka](http://kafka.apache.org).

Most of the utils code has been adapted to work with [Apache Curator](http://curator.apache.org) from [Apache Kafka](http://kafka.apache.org).


License
-------

Apache Licensed. See accompanying LICENSE file.

