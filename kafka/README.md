## Apache Kafka Notes


###### Replication Factor

- Governed at topic level
- Property replication.factor
- Default is 3 which means 3 replicas across different brokers
- Helps to achieve higher reliability, higher availability and fewer disasters
- Replication factor is directly proportional to hardware cost
- By Default replicas are distributed across different brokers, to ensure rack level issues, brokers must be distributed across racks.



###### Unclean leader election

- Governed at broker level
- Property unclean.leader.election.enable, default value is true
- This is to allow out of sync replicas to take leaders position
- This has a risk of of consumers facing inconsistencies as well related offset discrepancy between replicas
- This ensures availability at cost of consistency


###### Minimum InSync Replicas


- Governed at both topic and broker level
- Property min.insync.replicas
- This enforces consistency at cost of availability
- Incase this is not adhered to producers start getting NotEnoughReplicasException


###### Producers Reliability

- Use the correct acks configuration to match reliability restrictions
- Handle errors correctly in code and config
- acks=0,1,all , choose wisely


###### Consumers Reliability

- Consumers having same group.id will be allocated subset of partitions each
- auto.offset.reset = earliest or latest depends on duplication
- enable.auto.commit is at risk of loosing messages due to processing error
- Handle application errors and use inbuilt retry logic