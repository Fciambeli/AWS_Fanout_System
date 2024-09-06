## AWS Fanout System ⚡

![AWS Fanout Sample](https://github.com/Fciambeli/AWS_Fanout_System/blob/main/Fanout.png)

---

## Description

If you want to create a robust and scalable architecture in the cloud, the Fanout design pattern using AWS SNS, SQS (FIFO) and Lambda is an excellent choice. Here I will show how these services can be used together to solve real problems efficiently! 📈

Whats is Fanout⁉️

Fanout refers to a message distribution pattern in which a single message is replicated and sent to multiple destinations. ☺️

Amazon SNS (Simple Notification Service): Imagine that you have an e-commerce system that needs to notify several services when a new order is placed. Using SNS, you can create a notification thread for new orders and publish a message whenever an order is placed (Pub/Sub).

Amazon SQS (Simple Queue Service): Suppose you have three services that need to process the request independently:

•	Inventory Service: Updates stock.

•	Billing Service: Generates an invoice for the order.

•	Customer Notification Service: Sends a confirmation email to the customer.

To guarantee the exact order of processing and avoid duplication of messages, you can use FIFO (First-In, First-Out) queues. These queues ensure that orders are processed in the exact order they were received, which is crucial for services like invoicing and inventory. Each service would have an SQS FIFO queue subscribed to the new request SNS topic, and messages will be processed sequentially.

AWS Lambda: To process messages in SQS queues, you can use Lambda functions. Each Lambda function is configured to be triggered by a specific SQS FIFO queue:

•	Inventory Lambda: Updates product stock.

•	Billing Lambda: Creates and stores the order invoice.

•	Notification Lambda: Sends a confirmation email to the customer.

Example:

1 - Publication on SNS: An order is placed on your e-commerce system. The backend publishes a message to the SNS topic "NewOrders" with details of the order.

2 - Distribution to SQS queues: The message is sent to three different FIFO SQS queues, one for each service that needs to process the request, ensuring that the order of arrival is respected.

3 - Processing with Lambda:
•	The Inventory Lambda is triggered by the inventory FIFO queue and updates the stock.
•	The Billing Lambda is triggered by the FIFO billing queue and generates an invoice.
•	The Notification Lambda is triggered by the FIFO notification queue and sends an email to the client.

Advantages 🚀:

•	Scalability: The system automatically scales to handle increased order volume. ✔

•	Decoupling: Each service is independent and can be upgraded or scaled separately.✔

•	Order Guaranteed with FIFO: The FIFO queue ensures that messages are processed in the correct order, which is crucial for operations that depend on the sequence of events.✔

•	Resilience: Even if one service fails, the others continue to process messages, increasing the robustness of the system.✔

<div style="display: inline_block"><br>
<img align="center" alt="Fabio-Aw" height="60" width="60" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/amazonwebservices/amazonwebservices-plain-wordmark.svg"">
