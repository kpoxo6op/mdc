# mdc

try mdc steps locally

## todo

### run kafka cluster locally

- helm 2 charts
- confluent images
- 4 brokers
- zookeper
- control center
- prometheus
- graphana

### add observer

- create broker config based on standard pod config
- import broker config into stateful set based on broker ID

### pin existing topics to DC1

- create some topics with default placement strategy
- create Replica placement strategy config for DC1 placement
- create topic which only exists in DC1.

use rebalancer to pin existing topics.

Verification: all topics (including internal) have replica placement set to DC1, replica count=3. There are no underreplicated partitions and under-min-isr partitions.

How do we verify that kafka-terraform-config respects replica placement strategy?

## Notes

### creating topic

- exec into pod
- run `kafka-topics --command-config /vault/secrets/client.properties --bootstrap-server ${BOOTSTRAP_SERVER} --create --topic user.m0000.observer.test --partitions 3`

### describing topic

- exec into pod
- run `kafka-topics --command-config /vault/secrets/client.properties --bootstrap-server ${BOOTSTRAP_SERVER} --describe --topic user.m0000.observer.test`
