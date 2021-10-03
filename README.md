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

Verification: all topics (including internal) have replica placement set to DC1, replica count=3. There are no underreplicated partitions and under-min-isr partitions.

How do we verify that kafka-terraform-config respects replica placement strategy?

### rebalancing

relocate replica in broker 5 to brokers 1-4

## Notes

### creating topic

- exec into pod
- run `kafka-topics --command-config /vault/secrets/client.properties --bootstrap-server ${BOOTSTRAP_SERVER} --create --topic user.m0000.observer.test --partitions 3`

### describing topic

- exec into pod
- run `kafka-topics --command-config /vault/secrets/client.properties --bootstrap-server ${BOOTSTRAP_SERVER} --describe --topic user.m0000.observer.test`

## Questions

Rebalancing.

- How many brokers and observers are we going to run in future?
- Do we convert broker to observer OR do we add extra broker?
- Did we move all-broker topic to brokers 1-4?
- did we move replica from broker 5 to brokers 0,1,2,3,4?
- why replica on broker 5 stays 3
- did we drown broker 5?
