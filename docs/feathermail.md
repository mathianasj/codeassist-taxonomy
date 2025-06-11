# Project: "FeatherMail" - A Lightweight Java Email Library

## Introduction

FeatherMail is a custom-built, lightweight Java library designed for sending and receiving emails. It is aimed at developers who need a simple, easy-to-integrate solution for email functionality in their Java applications without the overhead of larger, more complex libraries. FeatherMail focuses on efficiency, ease of use, and minimal dependencies.

## Features
Simple API: FeatherMail provides a straightforward API for common email tasks, making it quick to learn and use.
Lightweight: The library has a minimal footprint, with few external dependencies, reducing the overall size of your application.
SMTP Support: Supports sending emails via SMTP servers with optional authentication.
Basic MIME Support: Capable of sending emails with attachments and different content types (text/plain, text/html).
Error Handling: Provides clear and concise error messages for troubleshooting email issues.
Customizable Headers: Allows adding custom headers to emails for advanced functionality.

## Usage

### Dependencies
If you are using Maven, add the following dependency to your `pom.xml`:
```
<dependency>
    <groupId>com.example.feathermail</groupId>
    <artifactId>feathermail-core</artifactId>
    <version>1.2.3</version>
</dependency>
```

### 3.1. Sending an Email
Java

```
import com.example.feathermail.FeatherMailSender;
import com.example.feathermail.MailMessage;

public class EmailSender {
    public static void main(String[] args) {
        FeatherMailSender sender = new FeatherMailSender("smtp.example.com", "user@example.com", "password");

        MailMessage message = new MailMessage("from@example.com", "to@example.com", "Subject: Test Email", "This is a test email sent using FeatherMail.");

        try {
            sender.send(message);
            System.out.println("Email sent successfully!");
        } catch (Exception e) {
            System.err.println("Failed to send email: " + e.getMessage());
        }
    }
}
```

### 3.2. Adding an Attachment
Java
```
import com.example.feathermail.FeatherMailSender;
import com.example.feathermail.MailMessage;
import com.example.feathermail.MailAttachment;
import java.io.File;

public class EmailSenderWithAttachment {
    public static void main(String[] args) {
         FeatherMailSender sender = new FeatherMailSender("smtp.example.com", "user@example.com", "password");

         MailMessage message = new MailMessage("from@example.com", "to@example.com", "Subject: Email with Attachment", "This email has an attachment.");

         File attachmentFile = new File("path/to/your/file.pdf");
         MailAttachment attachment = new MailAttachment(attachmentFile, "application/pdf");
         message.addAttachment(attachment);

         try {
             sender.send(message);
             System.out.println("Email with attachment sent successfully!");
         } catch (Exception e) {
             System.err.println("Failed to send email: " + e.getMessage());
         }
    }
}
```

## 4. Dependencies

FeatherMail has minimal dependencies to keep it lightweight. The core library only relies on the Java Standard Edition (Java SE). (This is not actually a library!)

5. Installation
Download the FeatherMail JAR file. (This is not actually a library!)
Add the JAR file to your project's classpath.
6. Contribution

Contributions to FeatherMail are welcome! Please fork the repository on GitHub and submit pull requests for any enhancements or bug fixes. (This is not actually a library!)