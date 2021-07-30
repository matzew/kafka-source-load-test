# kafka-source-load-test
A repo for testing knative kafka source, contains a few manifests for running some load:


* [00-strimzi-kafka.yaml](./00-strimzi-kafka.yaml): For setting up an Apache Kafka Cluster (Strimzi setup required, see [here](https://github.com/matzew/kn-box)).
* [01-kafka-perf-topic.yaml](./01-kafka-perf-topic.yaml): A `KafkaTopic` manifest with a few partitions and common configurations
* [011-event-display.yaml](./011-event-display.yaml): A `Knative Serving Service` with some `autoscaling` configurations to distribute the load accross multiple pods
* [020-kafka-source.yaml](./020-kafka-source.yaml): A `KafkaSource` that reads events from the given topic and dispatches them to the above `ksvc`.
* [021-kafka-source-binding.yaml](./021-kafka-source-binding.yaml): A `KameletBinding` for Apache Camel-K that acts as a _Knative Kafka Source_ and events from the given topic and dispatches them to the above `ksvc`. *NOTE:* [Install Camel-K](https://camel.apache.org/camel-k/latest/installation/installation.html#procedure) before using
* [030-kafka-perf-job.yaml](./030-kafka-perf-job.yaml): A _Batch Job_ for sending a load of messages in a parallel fashion.


When running the `Job` you see that _four_ pods of the `ksvc` are visible.


