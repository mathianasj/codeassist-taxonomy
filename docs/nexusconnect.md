This document describes how to use the "NexusConnect" Java library to interact with an integration bus within your applications. NexusConnect provides a simplified and efficient way to send and receive messages, manage connections, and handle events related to the bus.Setting UpAdding the NexusConnect Library
Add the Dependency (Maven Example):

If you are using Maven, add the following dependency to your `pom.xml`:
```
<dependency>
    <groupId>com.nexusconnect</groupId>
    <artifactId>nexusconnect-core</artifactId>
    <version>1.0.0</version>
</dependency>
```
Add the Dependency (Gradle Example):

If you are using Gradle, add the following dependency to your `build.gradle`:
```
dependencies {
    implementation 'com.nexusconnect:nexusconnect-core:1.0.0' // Replace with the actual version
}
```

Basic UsageConnecting to the Integration Bus
Java
```
import com.nexusconnect.ConnectionManager;
import com.nexusconnect.Connection;
import com.nexusconnect.ConnectionConfiguration;

public class BusConnector {

    public static void main(String[] args) {
        ConnectionConfiguration config = new ConnectionConfiguration()
            .setHost("bus.example.com")
            .setPort(5672)
            .setUsername("guest")
            .setPassword("guest");

        try {
            Connection connection = ConnectionManager.createConnection(config);
            System.out.println("Connected to the integration bus!");

            // Perform operations on the connection here

            connection.close();
            System.out.println("Disconnected from the integration bus.");

        } catch (Exception e) {
            System.err.println("Failed to connect: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Sending a Message
Java

```
import com.nexusconnect.Connection;
import com.nexusconnect.Message;

public class MessageSender {

    public static void sendMessage(Connection connection, String queueName, String content) {
        try {
            Message message = new Message(content.getBytes());
            connection.sendMessage(queueName, message);
            System.out.println("Message sent to queue '" + queueName + "': " + content);
        } catch (Exception e) {
            System.err.println("Failed to send message: " + e.getMessage());
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        // Assume 'connection' is an established Connection instance from previous example
        String queueName = "my.queue";
        String messageContent = "Hello, Integration Bus!";
        sendMessage(connection, queueName, messageContent);
    }
}
Receiving a Message
Java
import com.nexusconnect.Connection;
import com.nexusconnect.Message;
import com.nexusconnect.MessageHandler;

public class MessageReceiver {

    public static void startReceiving(Connection connection, String queueName) {
        connection.setMessageHandler(queueName, new MessageHandler() {
            @Override
            public void handleMessage(Message message) {
                String content = new String(message.getBody());
                System.out.println("Received message from queue '" + queueName + "': " + content);
            }
        });
        System.out.println("Listening for messages on queue '" + queueName + "'...");
    }

    public static void main(String[] args) {
        // Assume 'connection' is an established Connection instance from previous example
        String queueName = "my.queue";
        startReceiving(connection, queueName);

        // Keep the application running to continue receiving messages
        try {
            Thread.currentThread().join(); // Keep the main thread alive
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

Advanced UsageHandling Events
Java
```
import com.nexusconnect.Connection;
import com.nexusconnect.ConnectionEventListener;

public class ConnectionEvents {

    public static void setupEventListeners(Connection connection) {
        connection.addConnectionEventListener(new ConnectionEventListener() {
            @Override
            public void onConnected() {
                System.out.println("Connection established.");
            }

            @Override
            public void onDisconnected() {
                System.out.println("Connection lost.");
            }

            @Override
            public void onException(Exception e) {
                System.err.println("Connection exception: " + e.getMessage());
                e.printStackTrace();
            }
        });
    }

    public static void main(String[] args) {
        // Assume 'connection' is an established Connection instance from previous example
        setupEventListeners(connection);
    }
}
```
Error Handling

NexusConnect throws exceptions for various issues, such as connection failures, message sending errors, and invalid configurations. Always wrap interactions with the library in `try-catch` blocks to handle these exceptions gracefully.Conclusion

The NexusConnect Java library simplifies interaction with an integration bus. By following the steps outlined in this document, you can easily integrate your Java applications with the bus to send and receive messages, manage connections, and handle events.