---
title: "AWS CloudWatch: Monitoring & Alarms"
date: "2020-08-31"
categories: 
  - "aws"
  - "devops"
tags: 
  - "alarms"
  - "aws-cloudwatch"
  - "iops"
  - "kibana"
  - "logging"
---

AWS CloudWatch is a fully-managed service for monitoring AWS services and workloads. For websites, apps, and microservices that are entirely hosted on AWS, this is a great cloud logging solution.

As a fully-managed service, it is very easy to manage log retention periods, which can be configured on a per-group basis. By default, CloudWatch stores the log data indefinitely. Another advantage of CloudWatch is that it allows you to easily monitor host performance of AWS services. For instance, if you install the CloudWatch Agent on an EC2 instance, this will allow you to easily replace an entire third-party monitoring stack. CloudWatch receives and provides metrics for all Amazon EC2 instances and should work with any operating system currently supported by the EC2 service. Finally, CloudWatch is flexible enough not just for host monitoring, but also allows you to monitor your application as well.

You can easily pipe local logs up to CloudWatch using the CloudWatch Agent to extract data and create custom app metrics. One use case of CloudWatch is that you can monitor AWS services and get real-time alerts when certain criteria are exceeded. For instance, consider a company that needs to monitor the read and write IOPS metrics for their General Purpose SSD storage type. The company wants to send real-time alerts to their team when the IOPS exceeds 2,800 IOPS so that they can determine whether the performance stress will allow them to better calibrate their I/O credit balance and/or increase the volume of their storage type.

#### CloudWatch Alarms

CloudWatch alarms allows you to watch metrics and trigger events when the metrics deviate from a user-define standard of deviation. Events that CloudWatch alarms can trigger include sending an SNS notification or triggers an action that increases the size of an autoscaling group. A CloudWatch alarm has three states: `INSUFFICIENT_DATA`, `OK`, and `ALARM`.

The `OK` state means that the metric is within the user-define range. The `ALARM` state is when the metric falls outside of that range (either too low or too high). The `INSUFFICIENT_DATA` state means that the data needed to make the decision is missing or incomplete. When this happens, you may need to decrease the data point threshold or you may need to increase the evaluation period so that more data can be gathered. By default, CloudWatch alarm history is stored for 14 days.

#### CloudWatch Namespaces and Dimensions

Namespaces are containers for metrics, and are isolated from each other so that metrics from different applications are not mistakenly aggregated into the same statistics. All namespaces follow the convention `AWS/<service>`. For instance, `AWS/EC2` and `AWS/ELB`. Keep in mind that there is no default namespace. Each data you put into CloudWatch must specify a namespace.A dimension is a name/value pair that partially and uniquely identifies a metric. For example, you can see that the following has two dimensions:

```powershell
Dimensions: Server=Prod, Domain=Frankfurt, Unit: Count, Timestamp: 2016-10-31T12:30:00Z, Value: 105
```

CloudWatch is a powerful tool that is optimized for the AWS ecosystem. With it, you can gain powerful insight into the AWS services and applications that you run, which will help you to debug and monitor your AWS presence.
