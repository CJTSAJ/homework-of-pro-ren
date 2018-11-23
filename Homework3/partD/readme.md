# Stream processing with Kafka
本实例使用 kafka stream 实现了wordcount 功能。

应用场景为记录输入文本中的单词的出现个数。

主要实现方法如下：

1. 使用KStream建立一个 kafka topic 'word-count-input' 关联的 stream，textLines，读取输入数据流

```java

KStreamBuilder builder = new KStreamBuilder();
        // 1 - stream from Kafka

        KStream<String, String> textLines = 
        builder.stream("word-count-input");
```

2. 使用 KTable 完成计数

```java

KTable<String, Long> wordCounts = textLines
                // 2 - map values to lowercase
                .mapValues(String::toLowerCase)
                // can be alternatively written as:
                // .mapValues(String::toLowerCase)
                // 3 - flatmap values split by space
                .flatMapValues(textLine -> Arrays.asList(textLine.split("\\W+")))
                // 4 - select key to apply a key (we discard the old key)
                .selectKey((key, word) -> word)
                // 5 - group by key before aggregation
                .groupByKey()
                // 6 - count occurrences
                .count("Counts");
```

3. 将结果写回 kafka topic 'word-count-output'

```java
// 7 - to in order to write the results back to kafka
        wordCounts.to(Serdes.String(), Serdes.Long(), "word-count-output");
```

4. 通过 kafka topic 'word-count-output' 读取结果
```java
KafkaStreams streams = new KafkaStreams(builder, config);
        streams.start();



        // shutdown hook to correctly close the streams application
        Runtime.getRuntime().addShutdownHook(new Thread(streams::close));

        // Update:
        // print the topology every 10 seconds for learning purposes
        while(true){
            System.out.println(streams.toString());
            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                break;
            }
        }
```