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
