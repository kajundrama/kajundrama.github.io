---
title: "MSA:: Kafka 시작하기"
categories:
  - msa
tags:
  - msa
---

# Kafka 란?
Apache Kafka는 실시간으로 기록 스트림을 게시, 구독, 저장 및 처리할 수 있는 분산 데이터 스트리밍 플랫폼입니다. 이는 여러 소스에서 데이터 스트림을 처리하고 여러 사용자에게 전달하도록 설계되었습니다. 간단히 말해, A지점에서 B지점까지 이동하는 것뿐만 아니라 A지점에서 Z지점을 비롯해 필요한 모든 곳에서 대규모 데이터를 동시에 이동할 수 있습니다.  
Apache Kafka는 전통적인 엔터프라이즈 메시징 시스템의 대안입니다. 하루에 1조4천억 건의 메시지를 처리하기 위해 LinkedIn이 개발한 내부 시스템으로 시작했으나, 현재 이는 다양한 기업의 요구사항을 지원하는 애플리케이션을 갖춘 오픈소스 데이터 스트리밍 솔루션이 되었습니다.   
출처 : [https://www.redhat.com/ko/topics/integration/what-is-apache-kafka](https://www.redhat.com/ko/topics/integration/what-is-apache-kafka)

# Kafka 설치하기
[kafka 다운로드 사이트](https://kafka.apache.org/downloads)에서 다운로드 받아서 설치합니다. 다운로드 받은 zip 파일 압축을 해제합니다.  

# Kafka 구동하기
kafka는 [ZooKeeper](https://zookeeper.apache.org/) 기반으로 동작하기 때문에 zookeeper를 먼저 실행한다.
ZooKeeper에 대한 자세한 내용은 아래 링크를 참고하세요.
[https://zookeeper.apache.org/doc/current/zookeeperOver.html#sc_designGoals](https://zookeeper.apache.org/doc/current/zookeeperOver.html#sc_designGoals)   

```shell script
cd kafka_2.13-2.6.0
bin/zookeeper-server-start.sh config/zookeeper.properties
bin/kafka-server-start.sh config/server.properties
```

아래와 같이 기동로그가 뜨면 정상적으로 기동된 것 입니다.   

```shell script
[2021-01-27 23:17:13,039] INFO [KafkaServer id=0] started (kafka.server.KafkaServer)
[2021-01-27 23:17:13,146] INFO [broker-0-to-controller-send-thread]: Recorded new controller, from now on will use broker 0 (kafka.server.BrokerToControllerRequestThread)
```

# Topic 생성하기
아래와 같이 명령어를 수행ㅎ라여 Topic을 생성합니다.   

```shell script
$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
Created topic quickstart-events.
```
생성된 Topic을 확인합니다.   

```shell script
$ bin/kafka-topics.sh --list --bootstrap-server localhost:9092
quickstart-events
```
특정 토픽에 대한 설정 확인하기   

```shell script
$ bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
Topic: quickstart-events	PartitionCount: 1	ReplicationFactor: 1	Configs: segment.bytes=1073741824
	Topic: quickstart-events	Partition: 0	Leader: 0	Replicas: 0	Isr: 0
```
# Producer, Consumer 실행하기
kafka에서 제공하는 shell을 통해 Producer와 Consumer를 실행하여 이벤트를 주고 받을 수 있다.

Producer 생성하기   

```shell script
$ bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```

Consumer 생성하기   

```shell script
$ bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```

메시지 전송하고 받기
전송시점에 Consumer가 기동상태가 아니더라도 기동되면 그동안 보냈던 메시지가 한번에 수신한다.  
 
```shell script
$ bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
>hello kafka!!
$ bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
hello kafka!!
```

다음은 Producer, Consumer를 Java로 구현해보기
출처 : [https://velog.io/@hanblueblue/Kafka-%EC%84%A4%EC%B9%98%EC%8B%A4%ED%96%89-%EB%B0%8F-%ED%85%8C%EC%8A%A4%ED%8A%B8](https://velog.io/@hanblueblue/Kafka-%EC%84%A4%EC%B9%98%EC%8B%A4%ED%96%89-%EB%B0%8F-%ED%85%8C%EC%8A%A4%ED%8A%B8)