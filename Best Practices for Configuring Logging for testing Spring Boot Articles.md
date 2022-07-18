**Best Practices for Configuring Logging for Testing Spring Boot Articles**

The variety of tools and frameworks available in Spring Boot can be overwhelming, and it can be difficult to even know where to begin when it comes to logging. The most popular best practices for Spring Boot logging are discussed in this tutorial, along with five essential recommendations to expand your logging toolbox.

# **The content of the spring boot box**
The spring-boot-starter-log is a prerequisite for all Spring Boot Starters. The majority of your application's logging dependencies originate from here. The dependencies include frameworks and a façade (SLF4J) (Logback). Understanding what these are and how they work together is crucial.

SLF4J is a straightforward front-facing façade that is backed by a number of logging frameworks. Its key benefit is that switching between logging frameworks is simple. In our situation, switching from Logback to Log4j, Log4j2, or JUL is a simple process.

We also use dependencies that write logs. For instance, Hibernate makes use of SLF4J, which is ideal because we have it on hand. The AWS SDK for Java, however, takes advantage of Apache Commons Logging (JCL). The bridges required to guarantee that the logs are immediately assigned to our logging framework are included in spring-boot-starter-logging.

**Setting Up Your Log Format with Logback and Log4j2**

For logback and log4j2, Spring Boot Logging offers default setups. The logging level, appenders (where to log), and message format are all specified in these.

The Console Appender is the only appender used by default. Therefore, logs will only be delivered to the console, with the exception of a few specialized packages, for which the default log level is set to INFO.

**Configuring Logback**

Logback does not need to be configured. All log messages with a DEBUG level or higher are automatically written to standard out by default. A personalised configuration file in XML format can be used to adjust that.

Similar ideas are employed by Logback and Log4j. It therefore comes as no surprise that their setups are remarkably similar, even if they use distinct file formats.

After configuring Logback and adding the necessary dependencies, you may use it to write log messages using the SLF4J API. Therefore, replacing Log4j with Logback does not require any code changes if you wish to take advantage of the benefits offered by Logback.

**Spring Boot: Cherry on the top**

Let's explore what spring boot has to offer in the logging protocol and in-depth settings. Except for the Commons Logging API, which is normally provided by the spring-jcl module of the Spring Framework, Spring Boot has no required logging dependencies. You must put spring-jcl and logback on the classpath in order to use Logback. The simplest way to do so is through the starts, which rely on spring-boot-starter-logging. Only spring-boot-starter-web is required for a web application because it transitively depends on the logging starter. The following dependency adds logging for you if you use Maven:

**<dependency>**

`	`**<groupId>org.springframework.boot</groupId>**

`	`**<artifactId>spring-boot-starter-web</artifactId>**

**</dependency>**

A LoggingSystem abstraction in Spring Boot makes an effort to setup logging depending on the classpath's contents. Logback is the first option if it's accessible.

The following example demonstrates how to use the "logging.level" prefix in application.properties if the only modification you need to make to logging is to adjust the levels of multiple loggers:

**logging.level.org.springframework.web=DEBUG**

**logging.level.org.hibernate=ERROR**

Using "logging.file," you can specify a different path for a file to which the log should be written in addition to the console.

Use the native configuration format offered by the specific LoggingSystem in order to set up a logging system's more precise configuration options. The "logging.config" parameter allows you to specify the location of the configuration file, which is often picked up by Spring Boot from the native configuration's default place for the system (such as classpath:logback.xml for Logback).

**Getting Hibernate up and running**

It is important to configure Hibernate so that it will log the bind parameters used and the SQL statements executed.

Hibernate logs the performed SQL queries and their bound arguments using 2 separate log categories and log levels:

The SQL statements are written to the category org.hibernate.SQL as DEBUG messages. The bind arguments are logged at log level TRACE under the org.hibernate.type.descriptor.sql category.

In your log setup, you can independently enable and deactivate them.

Good, widely-used logging frameworks include Log4j, Logback, and Log4j2. Which one should you choose then? 

We advise using Log4j2 because it is the quickest and most sophisticated of the three frameworks. If performance is not your top priority, Logback is your ideal ally.
