# AWS Certified: Cloud Practitioner (CLF-C02)

Demonstrate foundational knowledge of core data concepts related to Amazon AWS data services.

- ### AWS SkillBuilder Learn [link](https://skillbuilder.aws/learning-plan/8UUCEZGNX4/exam-prep-plan-aws-certified-cloud-practitioner-clfc02--english/1J2VTQSGU2)

## Domain 1: Cloud Concepts

### AWS Cloud Benefits and Concepts

- **AWS Overview**:
  - Comprehensive cloud platform with over 200 services.  
  - Used for cost reduction, agility, and faster innovation.  

- **Cloud Computing Criteria**:  
  - **On-Demand Self-Service**: Provision resources without human intervention.  
  - **Network Connectivity**: Access resources via multiple protocols.  
  - **Resource Pooling**: Shared resources across multiple customers, abstract location.  
  - **Elasticity**: Scale resources up or down with demand.  
  - **Monitored and Billed Usage**: Pay for actual usage, no need for pre-provisioning.  

- **AWS Infrastructure**:  
  - **Regions and Availability Zones**: Geographic distribution for redundancy.  
  - **Edge Locations**: Content delivery closer to users.  

- **High Availability vs. Fault Tolerance**:  
  - **High Availability**: Quick recovery from failures, potential brief downtime.  
  - **Fault Tolerance**: Continuous operation despite failures, usually more costly.  

- **Disaster Recovery**:  
  - Essential pre-planned strategies for quick system recovery during disasters.  

- **Scaling**:  
  - **Vertical Scaling**: Resize instances to larger sizes, can cause disruptions.  
  - **Horizontal Scaling**: Add more instances, typically more cost-effective.  

- **Elasticity**:  
  - Automate scaling to match capacity with fluctuating demand using AWS tools.  

- **AWS Well-Architected Framework Pillars**:  
  - Focus on **Performance Efficiency**, **Operational Excellence**, and **Cost Optimization**.  

- **Exam Tips**:  
  - Understand differences between vertical and horizontal scaling.  
  - Recognize elasticity as automated scaling aligned with demand.

### AWS Well-Architected Framework: Key Design Principles

#### Overview  

- **AWS Well-Architected Framework**: A set of best practices and core strategies for architecting systems in the cloud. It aims to help design, build, and operate reliable, secure, efficient, and cost-effective systems, increasing the likelihood of success.  

#### Six Pillars of AWS Well-Architected Framework  

1. **Operational Excellence**:  
   - **Design Principles**:  
     - Perform operations as code.  
     - Make frequent, small, reversible changes.  
     - Refine operations procedures frequently.  
     - Anticipate failure.  
     - Learn from all operational failures.  

2. **Security**:  
   - **Design Principles**:  
     - Implement a strong identity foundation.  
     - Maintain traceability.  
     - Apply security at all layers.  
     - Automate security best practices.  
     - Protect data in transit and at rest.  
     - Keep people away from data.  
     - Prepare for security events.  

3. **Reliability**:  
   - **Design Principles**:  
     - Automatically recover from failure.  
     - Test recovery procedures.  
     - Scale horizontally to increase availability.  
     - Stop guessing capacity.  
     - Manage change in automation.  

4. **Performance Efficiency**:  
   - **Design Principles**:  
     - Democratize advanced technologies.  
     - Go global in minutes.  
     - Use serverless architectures.  
     - Experiment more often.  
     - Consider mechanical sympathy.  

5. **Cost Optimization**:  
   - **Design Principles**:  
     - Cover under Domain 4 (billing, pricing, and support).  

6. **Sustainability**:  
   - **Design Principles**:  
     - Understand your impact.  
     - Establish sustainability goals.  
     - Maximize utilization.  
     - Adopt efficient hardware and software.  
     - Use managed services.  
     - Reduce downstream impact.  

#### General Design Principles  

- Stop guessing capacity; use auto scaling.  
- Test systems at production scale.  
- Automate architecture for easier experimentation.  
- Allow evolutionary changes; use data for improvements.  
- Conduct game days to test systems at production level.  

#### Practical Application  

- Understand best practices for each pillar.  
- Design for failures, decouple components, implement elasticity, security, and parallelization.  
- **Parallelization**: Divide tasks into simpler forms and distribute them to multiple components for efficiency.  

#### Exam Focus  

- Familiarity with AWS Well-Architected Framework and its pillars is crucial for AWS Certified Solutions Architect Associate certification.  
- Be prepared to choose design principles for specific requirements or use cases in AWS.  

### Understand the benefits of and strategies for migration to the AWS Cloud

**AWS Cloud Adoption Framework (CAF):**  

- Provides a comprehensive approach to cloud adoption.  
- Identifies organizational capabilities for successful cloud transformations.  
- Capabilities are grouped into six perspectives: business, people, governance, platforms, security, and operations.  
- Benefits include reduced business risk, enhanced performance and security, increased operational efficiency, and growth opportunities.  

**Migration Strategies:**  

- **Project Stage**: Evaluating AWS suitability for requirements.  
- **Foundation Stage**: Initial migration and framework deployment.  
- **Migration Stage**: Establishing roles, a Cloud Center of Excellence (CCOE), and preparing for cloud operations.  
- **Reinvention Stage**: Starting new projects in AWS.  

**Seven Migration Strategies:**  

1. **Retire**: Decommissioning applications.  
2. **Retain**: Keeping applications in the source environment.  
3. **Rehost**: Migrating applications without changes (lift and shift).  
4. **Relocate**: Moving large numbers of servers.  
5. **Repurchase**: Opting for new versions/products with more value.  
6. **Replatform**: Optimizing applications for AWS capabilities.  
7. **Refactor**: Using cloud-native features for agility, performance, and scalability.  

**AWS Services for Migration:**  

- Consider Amazon EFS or Amazon RDS for applications requiring low latency and constant data changes.  
- Use Amazon DynamoDB for scalable and reliable NoSQL databases.  

**Cost Optimization:**  

- For Microsoft SQL Server, consider using Amazon EC2 with a Windows AMI bundled with SQL Server Standard for cost savings compared to Amazon RDS.  

**Data Backups:**  

- Amazon S3 Glacier offers low-cost storage for archiving data, with retrieval fees and times to consider.  

---  

### Cloud Economics Concepts  

- **Shift Technical Resources**: Moving to AWS allows you to shift away from managing on-premises infrastructure, freeing up resources for other priorities like optimizing resource utilization and enhancing end-user experiences.  
- **Consumption Model**: AWS promotes a pay-as-you-go model, reducing costs associated with running data centers and enabling better tracking and analysis of cost and usage.  
- **Economies of Scale**: AWS offers lower costs due to economies of scale, allowing organizations to reduce the total cost of ownership.  

**Total Cost of Ownership (TCO) Components:**  

1. **Operational Expenses (OpEx)**: Daily operating costs like utilities and office supplies.  
2. **Capital Expenses (CapEx)**: Long-term investments such as buildings, servers, and equipment.  
3. **Labor Costs**: Staffing for on-premises environments, including technicians for server management.  
4. **Software Licensing**: Consideration of current licenses when migrating to AWS, including potential transferability or AWS-managed alternatives.  

**Cost Reduction Strategies:**  

- **Automation**: Implement automation to reduce costs and improve efficiency.  
- **Benchmarking and Performance Testing**: Focus on these instead of provisioning for peak demand.  
- **Horizontal Scaling**: Scale horizontally to meet demands rather than maintaining peak capacity.  
- **Data Segmentation and Targeted Reporting**: Helps reduce compliance scope and save audit time.  
- **Managed Services**: Utilize AWS Managed Services to reduce technical workload and costs.  

**Exam Tips:**  

- Understand the trade-off between capital expenses and variable expenses when migrating to AWS.  
- Focus on right-sizing, adding automation, ensuring compliance, and leveraging AWS Managed Services as outlined in the AWS Well-Architected Framework.

## Domain 2: Security and Compliance

### Introduction to Security and Compliance

- **AWS Shared Responsibility Model**:
  - Understand which security responsibilities fall to AWS and which fall to the customer.  
  - AWS manages security "of" the cloud, including infrastructure, while customers are responsible for security "in" the cloud, such as managing their data and configuring security settings.

- **Key Focus Areas**:  
  - **Security and Compliance Concepts**: Learn when and how security measures need to be implemented, recognizing that AWS abstracts some technical details but does not absolve users from security responsibilities.  
  - **Access Management**: Customers are always responsible for managing access to their AWS environment, regardless of the service used.  
  - **Security Features**: Familiarize yourself with available AWS security features and when you need to activate them, although detailed step-by-step instructions are not required for the exam.  

- **Preparation for the Exam**:  
  - Recognize the varying levels of responsibility based on the AWS service.  
  - Understand general security features in AWS and their appropriate application.  


---  

### AWS Shared Responsibility Model  

- **AWS Responsibilities**: AWS manages security "of" the cloud, which includes the global infrastructure (Regions, Availability Zones, edge locations), hardware, network, compute, storage, databases, and the software that supports these services. AWS handles the security and management of these foundational elements.  

- **Customer Responsibilities**: Customers are responsible for security "in" the cloud, which involves managing their data, applications, operating systems, network configurations, and firewall settings. Specific responsibilities include:  
  - Client-side data encryption and integrity.  
  - Server-side encryption.  
  - Protecting network traffic, such as using SSL certificates.  
  - Identity Access Management (IAM).  
  - Customer data security and backups.  

- **Examples of Responsibility**:  
  - **Amazon EC2**: Customers are responsible for patching, managing the operating system, and configuring security settings.  
  - **Amazon RDS**: AWS handles patching and maintenance as it is a managed service, reducing customer responsibilities.  

- **Understanding Service Levels**: The level of customer responsibility changes based on whether the AWS service is managed or unmanaged. Managed services (like Amazon RDS) require less customer involvement in security tasks compared to unmanaged services (like Amazon EC2).  

- **Exam Preparation**: Know the distinctions between customer and AWS responsibilities for various services, including Amazon RDS, Amazon EC2, Amazon DynamoDB, and AWS Lambda.  

---

### AWS Cloud Security, Governance, and Compliance  

- **Compliance Information:**  
  - **AWS Artifact**: Use this service for on-demand access to AWS security and compliance documents and reports.  
  - Compliance requirements vary by service; understanding where to find compliance information is crucial.  

- **Security Services:**  
  - **AWS WAF**: A web application firewall that protects applications from common exploits.  
  - **Amazon GuardDuty**: A threat detection service monitoring for malicious activity.  
  - **AWS Shield**: Provides managed DDoS protection for applications running on AWS.  
  - Other services include Amazon Inspector, AWS Security Hub, etc.  

- **Encryption:**  
  - Understand encryption for data in transit (moving between locations) and data at rest (stored data).  
  - Knowing who is responsible for enabling encryption ties back to the AWS shared responsibility model.  

- **Logging and Monitoring Services:**  
  - **Amazon CloudWatch**: Used for monitoring and collecting operational data.  
  - **AWS CloudTrail**: Logs events related to AWS resource creation and management; useful for auditing and compliance.  
  - **AWS Config**: Takes inventory of resource configurations and ensures they maintain correct settings.  

- **CloudTrail Use Case:**  
  - Use CloudTrail to identify actions such as an IAM user deleting an EC2 instance in production.  

- **Access Management:**  
  - Implement least-privileged access, granting users only the permissions they need.  

---
