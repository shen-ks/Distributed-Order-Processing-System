# Distributed-Order-Processing-System
This system will simulate an e-commerce order processing pipeline. It will involve various microservices, asynchronous messaging, and robust monitoring, giving you hands-on experience with all the required technologies.
# Architecture:

    Order Placement (AEM/Angular/Node.js):
        A user places an order through an AEM-powered website with an Angular frontend.
        Node.js will be used for backend logic within the frontend, if needed.
        This component will send the order details as a REST request to the Order Service.

    Order Service (SpringBoot/Quarkus):
        This service will receive orders via REST API.
        It will be implemented using both SpringBoot and Quarkus to compare and contrast.
        It will validate the order, persist it to a database, and publish an "Order Created" event to Kafka.

    Inventory Service (SpringBoot):
        This service will consume the "Order Created" event from Kafka.
        It will check if the items in the order are in stock.
        If in stock, it will update the inventory and publish an "Inventory Updated" event to IBM MQ.
        If out of stock, it will publish an "Inventory Out of Stock" event to IBM MQ.

    Payment Service (Quarkus):
        This service will consume events from IBM MQ.
        It will process payments using a simulated payment gateway.
        It will publish a "Payment Processed" event to Kafka.

    Shipping Service (SpringBoot):
        This service will consume the "Payment Processed" event from Kafka.
        It will generate shipping labels and update the order status.
        It might use a SOAP web service to interact with a simulated shipping provider.

    Monitoring and Logging:
        All services will log events to Splunk.
        Dynatrace will be used for performance monitoring and tracing.
        Bluetriangle will be used to monitor the user experience from the frontend perspective.

    CI/CD and Testing:
        Junit will be used for unit and integration testing.
        A CI/CD pipeline will be set up to automate testing and deployment.
