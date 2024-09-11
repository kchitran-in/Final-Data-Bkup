problem StatementCurrent system is not event driven. And all background jobs are handled by one or more actors , it can have following problems:  


1.  Each background job is calling different actor and doing predefined set of actions. (So it's tightly coupled)
1.  System state can become inconsistent if asynchronous call fails due to system failure.
1.  For each job we are passing different set of data (no predefined event structure)
1.  Difficult to generate the audit logs

Solution Approach![](images/storage/event-producer%20(2).png)

EventPublisher will hold the producer for which the produce calls on event will be made

  


```java
public interface EventPublisher{
	public void publish(Event event);
}

public class EventPublisherImpl implements EventPublisher{
	private Producer producer;
	private static EventPublisherImpl eventPublisher;
	
	public static EventPublisher getInstance(){
		if(eventPublisher==null){
			instance = initialize();
		}
		return instance;
	}
	
	public void publish(Event event){
		producer.produce(event);
	}

	public static EventPublisher initialize(){
		EventPublisher publisher = new EventPublisherImpl();
		//read setting and initialize producer by calling producer factory
		return publisher;
	}

}
```


there could be multiple producer with each having it's own processing of events


```java
public interface Producer{
	
	public void produce(Event event);

}

public class KafkaEventProducer implements Producer {
	
	public void produce(Event event){
		// push events to kafka topics
	}
}

public class ActiveMQEventProducer implements Producer {

	public void produce(Event event){
		// push events as json file to s3
	}

}

public class LMaxEventProducer implements Producer {

	public void produce(Event event){
		// push events in memory
	}
}
```




Consumer:


```
public interface IConsumer{
  public void consume();
}

public class ConsumerImpl implements IConsumer{
  public IConsumer consumer = ConsumerFactory.getInstance();
  @Override
  public void consume() {
    // consume events
  }
}

public class ConsumerFactory{
   public static IConsumer getInstance(){
     return new ConsumerImpl();
}
```












*****

[[category.storage-team]] 
[[category.confluence]] 
