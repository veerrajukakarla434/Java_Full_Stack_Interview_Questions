# Kafka Interview Questions

#### Kafka Architecture

* Refer -> https://medium.com/@cobch7/kafka-architecture-43333849e0f4
*  **Kafka architecture—a deep dive**
* Refer - > P1*****  https://www.redpanda.com/guides/kafka-architecture
* Refer -> https://doc.hcs.huawei.com/productdesc/mrs/mrs_08_00131.html#:~:text=Kafka%20Architecture,-Producers%20publish%20data&text=For%20each%20topic%2C%20the%20Kafka,ID%2C%20which%20is%20called%20offset.
* Refer -> https://www.projectpro.io/article/apache-kafka-architecture-/442#mcetoc_1fa2lfgs7a
* Refer -> P2*** https://developer.confluent.io/courses/architecture/get-started/#:~:text=Overview%20of%20Kafka%20Architecture,architecture%20and%20how%20it%20works.

#### Java-Spring Boot: How Kafka handle multiple objects while consuming ?

![image](https://github.com/user-attachments/assets/b27087b2-b343-4b44-85aa-2e65e794d177)

![image](https://github.com/user-attachments/assets/15954401-d263-41f4-a6c1-17d7efaddc8e)

![image](https://github.com/user-attachments/assets/a621f315-cc34-4925-8c10-02e387ccd53e)

![image](https://github.com/user-attachments/assets/169e9c88-504d-45e7-8550-4831e88322e6)

![image](https://github.com/user-attachments/assets/c37ef08b-ad22-4aa9-91a9-fbc33582bd2f)

```java
@JsonTypeInfo(use = Id.NAME, include = As.PROPERTY, property = "type")

@JsonSubTypes({

@JsonSubTypes.Type(value = Order.class, name = "order"),

@JsonSubTypes.Type(value = Customer.class, name = "customer")

})

public abstract class BaseType {}
```
![image](https://github.com/user-attachments/assets/64cf3ae7-811e-48a0-87d8-d6cd8ea4523f)

![image](https://github.com/user-attachments/assets/d5a34a70-9d54-4da6-abeb-24a24c2852f9)

```java
@Bean

public ConsumerFactory<String, Object> consumerFactory() {

Map<String, Object> configProps = new HashMap<>();

configProps.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);

configProps.put(ConsumerConfig.GROUP_ID_CONFIG, groupId);

configProps.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);

JsonDeserializer<Object> deserializer = new JsonDeserializer<>();

deserializer.setTypeMapper(typeMapper());

configProps.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, deserializer);

return new DefaultKafkaConsumerFactory<>(configProps, new StringDeserializer(), deserializer);

}

@Bean

public DefaultJackson2JavaTypeMapper typeMapper() {

DefaultJackson2JavaTypeMapper typeMapper = new DefaultJackson2JavaTypeMapper();

typeMapper.setTypePrecedence(Jackson2JavaTypeMapper.TypePrecedence.TYPE_ID);

typeMapper.addTrustedPackages("*");

Map<String, Class<?>> mappings = new HashMap<>();

mappings.put("order", Order.class);

mappings.put("customer", Customer.class);

typeMapper.setIdClassMapping(mappings);

return typeMapper;

}
```

![image](https://github.com/user-attachments/assets/7ed6eaeb-4b22-4ce6-8d7b-d88e418bbbd8)

```java
public class CustomDeserializer implements Deserializer<Object> {

private ObjectMapper objectMapper = new ObjectMapper();

@Override

public Object deserialize(String topic, byte[] data) {

try {

JsonNode jsonNode = objectMapper.readTree(data);

String type = jsonNode.get("type").asText();

switch (type) {

case "order":

return objectMapper.treeToValue(jsonNode, Order.class);

case "customer":

return objectMapper.treeToValue(jsonNode, Customer.class);

default:

throw new IllegalArgumentException("Unknown type: " + type);

}

} catch (IOException e) {

throw new SerializationException("Error deserializing message", e);

}

}

}
```
![image](https://github.com/user-attachments/assets/0a1d5ec7-7b70-46e9-a7eb-be758509a1fc)

![image](https://github.com/user-attachments/assets/ebe8f819-2ded-43ec-bc6c-04c05d008877)

![image](https://github.com/user-attachments/assets/75b2b18c-5a00-4afd-93a0-eb1bab2ecb12)

```java
  @Bean
public ConsumerFactory<String, Object> consumerFactory() {
    Map<String, Object> configProps = new HashMap<>();
    configProps.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
    configProps.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
    configProps.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, JsonDeserializer.class);
    
    JsonDeserializer<Object> deserializer = new JsonDeserializer<>();
    deserializer.setTypeMapper(typeMapper());
    
    return new DefaultKafkaConsumerFactory<>(configProps, new StringDeserializer(), deserializer);
}

@Bean
public DefaultJackson2JavaTypeMapper typeMapper() {
    DefaultJackson2JavaTypeMapper typeMapper = new DefaultJackson2JavaTypeMapper();
    typeMapper.setTypePrecedence(Jackson2JavaTypeMapper.TypePrecedence.TYPE_ID);
    typeMapper.addTrustedPackages("*");
    typeMapper.setIdClassMapping(Map.of("order", Order.class, "customer", Customer.class));
    return typeMapper;
}
```

![image](https://github.com/user-attachments/assets/6fbf32d1-a2c1-4e98-83f9-89760efe358d)

![image](https://github.com/user-attachments/assets/e9d0fe2d-7317-4ec6-ace3-05228ad4193d)

![image](https://github.com/user-attachments/assets/329a3382-caa0-4fbb-ab07-ec47c9933659)

![image](https://github.com/user-attachments/assets/30a98401-8f75-436a-ba23-09a2cbf34ed0)
