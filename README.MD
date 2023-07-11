# Introducing "CloudGuard" or "ComplianceWatch"!

##### call it whatever you like\_:)

This project is focused on governance and optimization of AWS resources using Lambda functions. It revolves around various aspects of cloud computing, specifically focused on Function as a Service (FaaS), cloud engineering, FinOps (Financial Operations), and cloud optimization.

**The main objective of this project is to automate compliance checks, enforce policies, and improve the security, compliance, and cost-efficiency of your AWS infrastructure.!**

![high-level architecture diagram](/architecture/ComplianceWatch%20CloudGuard%20architecture%20diagram.drawio_28876545_1.jpg)

## Use Case: Automated Amazon EFS Cleanup

### Description

In this use case, the objective is to optimize costs by automatically identifying and deleting Amazon EFS resources that have been unused for more than 30 days. By implementing this automated cleanup process, you can prevent unnecessary costs associated with idle or unused EFS file systems.

### Solution Flow

1.  **CloudWatch Event**: Configure a CloudWatch Event rule to trigger a Lambda function on a scheduled basis (e.g., daily or weekly). This rule is set to trigger the Lambda function at the desired interval.
2.  **AWS Lambda Function**: Create an AWS Lambda function that will be triggered by the CloudWatch Event rule. The Lambda function will handle the cleanup process.
3.  **Python Script Execution**: Inside the Lambda function, write a Python script to perform the following steps:

    a. **Retrieve EFS resources**: Use the AWS SDK or API to fetch a list of all Amazon EFS file systems within the AWS account.

    b. **Iterate through the EFS resources**: For each EFS resource, check the last access timestamp (metadata) of the file system.

    c. **Determine idle duration**: Calculate the duration between the current date and the last access timestamp of the EFS resource.

    d. **Delete idle resources**: If the idle duration exceeds 30 days, delete the EFS resource using the appropriate AWS SDK/API call.

### Execution Result

After the Lambda function is executed by the CloudWatch Event trigger, it will identify and delete any Amazon EFS file systems that have remained idle for more than 30 days.

```markdown
> At the heart of the serverless paradigm is the Function as a Service (FaaS) model, a category of services that make it ridiculously easy to run code in the cloud without provisioning any compute infrastructure.
```

## Project Goals

CloudGuard aims to achieve the following goals through governance and optimization of AWS resources:

1.  **Cost Optimization**: Implement cost optimization strategies by identifying unused or underutilized resources, rightsizing instances, and leveraging AWS pricing models. This helps reduce unnecessary expenses and maximize cost efficiency.
2.  **Compliance and Security**: Ensure compliance with regulatory standards and organizational policies by automating compliance checks, enforcing security measures, and implementing governance controls. This enhances data security, mitigates risks, and maintains regulatory compliance.
3.  **Resource Governance**: Streamline resource provisioning and management processes by implementing standardized resource templates, defining naming conventions, and enforcing tagging policies. This ensures consistent and well-governed resource usage across the organization.
4.  **Operational Efficiency**: Improve operational efficiency by automating routine tasks, such as resource provisioning, configuration management, and compliance checks. This reduces manual effort, increases productivity, and minimizes the risk of human errors.
5.  **Performance Optimization**: Optimize the performance of AWS resources by monitoring and analyzing performance metrics, identifying bottlenecks, and implementing performance enhancements. This leads to improved application performance and better user experiences.
6.  **Scalability and Flexibility**: Design and implement scalable architectures that can handle varying workloads effectively. Leverage AWS services like Auto Scaling, Elastic Load Balancing, and serverless computing to dynamically scale resources and ensure high availability.
7.  **Real-time Monitoring and Alerting**: Implement robust monitoring and alerting mechanisms using AWS CloudWatch, enabling proactive identification of issues, quick response to incidents, and efficient troubleshooting.
8.  **Resource Lifecycle Management**: Implement effective resource lifecycle management practices, including resource decommissioning, data archiving, and backup strategies. This ensures optimized resource usage and data retention while minimizing costs.
9.  **Continuous Improvement**: Establish a feedback loop to gather insights, analyze performance metrics, and continuously optimize AWS infrastructure based on evolving business needs. This facilitates ongoing improvement and keeps the infrastructure aligned with organizational goals.
10. **Transparent Reporting**: Generate comprehensive reports and dashboards to provide stakeholders with visibility into AWS usage, costs, compliance status, and performance metrics. This enables informed decision-making and fosters transparency across the organization.

## Dependencies

To run the Lambda function and execute the automated cleanup process, you will need the following dependencies:

- **boto3**: The AWS SDK for Python, which provides a high-level interface to interact with various AWS services, including EC2, CloudWatch, and more. It allows you to programmatically manage and interact with AWS resources.
  > **Note:** Please ensure that you have the necessary dependencies installed and configured properly before running the Lambda function..

## steps performed

1.  Go to the AWS console and create a new Lambda function named "EBS Volume Check" with Python 3 runtime. Choose to create a new role with basic Lambda permissions.
2.  Verify the Lambda function by testing the default basic Lambda function provided by AWS using the "Deploy and Test" option.
3.  Navigate to CloudWatch and create a rule to trigger the Lambda function.
4.  Create a rule in CloudWatch Events with service "EC2" and event type "EBS volume notification". Specify the event as the creation of any volume and provide the volume ARN.
5.  Configure the rule to target the Lambda function by giving it the name "ebs_volume_check" and providing a description.
6.  Verify that the CloudWatch rule triggers the Lambda function when a volume creation event occurs.
7.  Optionally, perform a dummy run to ensure that CloudWatch can successfully access the Lambda function.
8.  Check the CloudWatch log groups to see if the Lambda function is triggered and examine the logs for basic verification.
9.  Write the Python code to convert the EBS volume type from GP2 to GP3.
10. Modify the default Lambda handler (event, context) to include your Python logic. Access the necessary information, such as the volume ID, from the event details in the log stream.
11. Use an online JSON formatter for better readability of the event JSON.
12. Extract the volume ID by writing a separate function.
13. Utilize the boto3 library to interact with AWS resources, specifically for modifying the EBS volume.
14. Update the documentation to reflect the usage of boto3 and provide instructions for extracting the volume ID.
15. Ensure the Lambda function's IAM role has the necessary permissions to access EBS resources.
16. Grant the appropriate permissions to the IAM role associated with the Lambda function to avoid any access issues.
17. Create a volume and verify that it is successfully converted to GP3. Check the logs for any errors if the conversion does not occur as expected.

By following these steps, you have configured the AWS CloudWatch rule to trigger the Lambda function upon EBS volume creation and implemented the necessary Python logic to convert the volume type.

## Conclusion

Furthermore, it is important to note that this project is just a starting point. The concept of using AWS Lambda and event-driven architecture opens up vast and endless application scenarios. With the ability to trigger Lambda functions based on various events and integrate with other AWS services, developers have the flexibility to build powerful and customized solutions tailored to their specific needs.

The potential applications of this project extend far beyond EBS volume type conversion. Organizations can leverage similar approaches to automate various tasks, such as resource provisioning, data processing, monitoring, and much more. The combination of AWS Lambda and event-driven architecture provides the foundation for creating scalable, efficient, and event-responsive applications in the AWS ecosystem.
