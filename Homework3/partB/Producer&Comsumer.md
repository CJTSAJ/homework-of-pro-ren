# Code of Producer&Comsumer
### 创建项目
- win10下eclipse新建maven项目

- 修改pom.xml，添加依赖

```
<dependency>
   <groupId>org.apache.kafka</groupId>
   <artifactId>kafka_2.11</artifactId>
   <version>2.1.0</version>
</dependency>
```

### 创建生产者
- 新建文件Producer.java

- 添加代码

```
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerRecord;
import java.util.Properties;


public class Producer {
	private static KafkaProducer<String, String> producer;
	private final static String TOPIC = "adienTest1";
	public Producer() {
		Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("acks", "all");
        props.put("retries", 0);
        props.put("batch.size", 16384);
        props.put("linger.ms", 1);
        props.put("buffer.memory", 33554432);
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

        producer = new KafkaProducer<String, String>(props);
	}
	
	public void produce(){
        for (int i = 30;i<40;i++){
            String key = String.valueOf(i);
            String data = "hello kafka message："+key;
            producer.send(new ProducerRecord<String, String>(TOPIC,key,data));
            System.out.println(data);
        }
        producer.close();
    }
	
	public static void main(String[] args) {
        new Producer().produce();
    }
```

- 参数备注
    - bootstrap.servers --设置生产者需要连接的kafka地址
    - acks --回令类型
    - retries --重试次数
    - batch.size --批量提交大小
    - linger.ms --提交延迟等待时间（等待时间内可以追加提交
    - buffer.memory --缓存大小
    - key.serializer|value.serializer --序列化方法

### 创建消费者
- 新建文件Comsumer.java

- 添加代码

```
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;

import java.util.Arrays;
import java.util.Properties;

public class Comsumer {
	private static KafkaConsumer<String, String> consumer;
    private final static String TOPIC = "adienTest1";
    
    public Comsumer() {
    	Properties props = new Properties();
    	
    	props.put("bootstrap.servers", "localhost:9092");
        props.put("group.id", "test2");
        props.put("enable.auto.commit", "true");
        props.put("auto.commit.interval.ms", "1000");
        props.put("session.timeout.ms", "30000");

        props.put("auto.offset.reset","earliest");
        props.put("key.deserializer",
                "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("value.deserializer",
                "org.apache.kafka.common.serialization.StringDeserializer");
        consumer = new KafkaConsumer<String, String>(props);
    }
    
    public void consume(){
        consumer.subscribe(Arrays.asList(TOPIC));
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
            for (ConsumerRecord<String, String> record : records){
                System.out.printf("offset = %d, key = %s, value = %s",record.offset(), record.key(), record.value());
                System.out.println();
            }
        }
    }
    
    public static void main(String[] args) {
        new Comsumer().consume();
    }
}
```

### 运行代码
- 打开cmd，启动zookeeper

- 打开新的cmd，启动kafka

- 右键Producer.java文件，Run As Java Application，运行结果如下
![](http://wx4.sinaimg.cn/mw690/006AMixJly1fxfxb4i8nhj30i5060jrc.jpg)

- 右键Comsumer.java文件，Run As Java Application，运行结果如下
![](http://wx1.sinaimg.cn/mw690/006AMixJly1fxfxb9vdf8j30in05ydfz.jpg)

### 参考资料
[Java实现Kafka的生产者、消费者](https://blog.csdn.net/galen2016/article/details/80752147)

[kafka_2.12-1.1.0 生产与消费java实现示例](https://www.cnblogs.com/yy3b2007com/p/8688289.html)
