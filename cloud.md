# cloud Course
#### [study link](https://explore.skillbuilder.aws/learn/course/134/play/136404/aws-cloud-practitioner-essentials?lp=2170 "cloud practioner study")
## EC2

- Pay only for the compute time when it is running.
- Hypervisor and multitenancy.
  - EC2 runs on top of physical host machines managed by AWS using virtualization technology.
  - And a hypervisor running on the host machine is responsible for sharing the underlying physical resources between the virtual machines.
  - This idea of sharing underlying hardware is called multitenancy. The hypervisor is responsible for coordinating this multitenancy and it is managed by AWS.
  - The hypervisor is responsible for isolating the virtual machines from each other as they share resources from the host.
- Instance Types:
  - General purpose instances provide a good balance of compute, memory, and networking resources, and can be used for a variety of diverse workloads like web service or code repositories.
  - Compute optimized instances are ideal for compute-intensive tasks like gaming servers, high performance computing or HPC, and even scientific modeling.
  - Similarly, memory optimized instances are good for memory-intensive tasks. Accelerated computing are good for floating point number calculations, graphics processing, or data pattern matching, as they use hardware accelerators.
  - Accelerated Computing instances.
  - Storage optimized instances.
- EC2 pricing:
  - on-Demand ---> pay as you use.
  - savings plan ---->per year usage.
  - Reserved plan:
      - These are suited for steady-state workloads or ones with predictable usage and offer you up to a 75% discount versus On-Demand pricing. You qualify for a discount once you commit to a one or three-year term and can pay for them with three payment options: all upfront, where you pay for them in full when you commit; partial upfront, where you pay for a portion when you commit; and no upfront, where you don't pay anything at the beginning.
  - Spot instance:
      - they allow you to request spare Amazon EC2 computing capacity for up to 90% off of the On-Demand price. The catch here is that AWS can reclaim the instance at any time they need it, giving you a two-minute warning to finish up work and save state. You can always resume later if needed. So when choosing Spot Instances, make sure your workloads can tolerate being interrupted. A good example of those are batch workloads.
  - Dedicated Hosts:
      -  which are physical hosts dedicated for your use for EC2. These are usually for meeting certain compliance requirements and nobody else will share tenancy of that host.
## Scaling plans(scale the EC2 based on the demand):
  - Dynamic scaling responds to changing demand.
  - Predictive scaling automatically schedules the right number of Amazon EC2 instances based on predicted demand.
## Directing traffic with Elastic Load Balancing:
  - A load balancer acts as a single point of contact for all incoming web traffic to your Auto Scaling group. This means that as you add or remove Amazon EC2 instances in response to the amount of incoming traffic, these requests route to the load balancer first. Then, the requests spread across multiple resources that will handle them. For example, if you have multiple Amazon EC2 instances, Elastic Load Balancing distributes the workload across the multiple instances so that no single instance has to carry the bulk of it.
  - Although Elastic Load Balancing and Amazon EC2 Auto Scaling are separate services, they work together to help ensure that applications running in Amazon EC2 can provide high performance and availability.
  - This load balancer runs in the regional level.
## Messaging and Queue:
- Amazon Simple Notification Service (Amazon SNS)
    - Works on with publisher and subscriber model where the subscriber can subscribe all the components and wait
    - Amazon SNS is a publish/subscribe service. Using Amazon SNS topics, a publisher publishes messages to subscribers. 
- Amazon Simple Queue Service (Amazon SQS)
    - Works based on the Queue process, eg(buffer: even if the receiver end is in troyuble it will manage and send the message from the queue once the receiver end issue solved)
 
## MCQ Based
AMI ----> template for creating virtual machines
Cloud front ----> CDN and caching
How does AWS S3 achieve high availability?---> Through replication across Availability Zones
Which algorithm is NOT typically used in AWS Load Balancing? --->  Random Distribution
Snapshots in AWS are best described as:--->  Incremental backups of a storage volume
What is the purpose of Reserved Instances in AWS EC2?--->To reduce cost for predictable workloads
You observe that your web application is facing slow performance during peak traffic hours. Which AWS service can help improve application response times?---> AWS CloudFront
What is a key benefit of AWS CloudFront's caching mechanism?--->  It reduces EC2 instance load.
What is the significance of the "least connections" algorithm in AWS Load Balancing?---> Sends requests to the server with the fewest active connections
What should you consider before choosing a Reserved Instance plan in EC2?--->. Expected application workload consistency

If you want to restrict an IAM user to specific IP addresses, which feature should you use?--> Condition Keys

Your team uses S3 to store sensitive files. How can you ensure data is encrypted in transit?
2.  
Use HTTPS for all S3 requests.
If a Load Balancer is configured to use the "round-robin" algorithm, how does it route traffic?--->  Alternates requests to each server sequentially

Your application requires consistent throughput for traffic spikes. Which load balancing algorithm should you use?--->Weighted Round-Robin

If you need to block access to an EC2 instance for a specific IP, what should you use?--> security group rule
How does AWS CloudFront enhance the security of content delivery?---> By using signed URLs and signed cookies for access control

A developer wants to enable detailed monitoring for an EC2 instance. Which service should they use?----> A developer wants to enable detailed monitoring for an EC2 instance. Which service should they use?
  
