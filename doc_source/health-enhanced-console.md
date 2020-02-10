# Enhanced health monitoring with the environment management console<a name="health-enhanced-console"></a>

When you have enabled enhanced health reporting in AWS Elastic Beanstalk, you can monitor environment health in the [environment management console](environments-console.md)\.

**Topics**
+ [Environment dashboard](#health-enhanced-console-overview)
+ [Environment health page](#health-enhanced-console-healthpage)
+ [Monitoring page](#health-enhanced-console-monitoringpage)

## Environment dashboard<a name="health-enhanced-console-overview"></a>

The [environment dashboard](environments-console.md#environments-dashboard) displays the [health status](health-enhanced-status.md) of the environment and lists events that provide information about recent changes in health status\.

**To view the environment dashboard**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Navigate to the [management page](environments-console.md) for your environment\.

For detailed information about the current environment's health, open the **Health** page by choosing **Causes**\. 

![\[A health warning on the Elastic Beanstalk environment dashboard\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-dashboard.png)

## Environment health page<a name="health-enhanced-console-healthpage"></a>

The **Health** page displays health status, metrics, and causes for the environment and for each Amazon EC2 instance in the environment\.

**Note**  
Elastic Beanstalk displays the **Health** page only if you have [enabled enhanced health monitoring](health-enhanced-enable.md) for the environment\.

The following image shows the **Health** page for a Linux environment\.

![\[Environment health page for a Linux environment\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-instances.png)

The following image shows the **Health** page for a Windows environment\. Notice that CPU metrics are different from those on a Linux environment\.

![\[Environment health page for a Windows environment\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-instances-win.png)

To display only instances that have a particular status, choose**Filter By**, and then choose a [status](health-enhanced-status.md)\.

To reboot or terminate an unhealthy instance, choose **Instance Actions**, and then choose **Reboot** or **Terminate**\.

![\[Environment health page showing the instance actions menu for rebooting or terminating unhealthy instances\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-instances-actions.png)

To hide detailed information about the environment and instances' health, choose **Hide Details**\. To show or hide the details for a single instance, use the arrow at the beginning of the row\.

![\[Showing or hiding a single instance on the environment health page\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-console-causes.png)

Elastic Beanstalk updates the **Health** page every 10 seconds\. It reports information about environment health for five categories\.

The first category, **Server**, displays information about each of the EC2 instances in the environment\. This includes the instance's ID and [status](health-enhanced-status.md), the amount of time since the instance was launched, and the ID of the most recent deployment executed on the instance\.

For more information about an instance, including its Availability Zone and instance type, pause on its **Instance ID**\.

![\[Server metrics on the environment health page with instance information tooltip\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-console-instance.png)

For information about the last [deployment](using-features.deploy-existing-version.md) to the instance, pause on the **Deployment ID**\.

![\[Server metrics on the environment health page with deployment information tooltip\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-console-deployment.png)

Deployment information includes the following:
+ **Deployment ID**—The unique identifier for the [deployment](using-features.deploy-existing-version.md)\. Deployment IDs starts at 1 and increase by one each time you deploy a new application version or change configuration settings that affect the software or operating system running on the instances in your environment\.
+ **Version**—The version label of the application source code used in the deployment\.
+ **Status**—The status of the deployment, which can be `In Progress`, `Deployed`, or `Failed`\.
+ **Time**— For in\-progress deployments, the time that the deployment started\. For completed deployments, the time that the deployment ended\.

The other categories provide detailed information about the results and latency of requests served by each instance, and load and CPU utilization information for each instance\. For details on these metrics, see [Instance metrics](health-enhanced-metrics.md)\.

If you [enable X\-Ray integration](environment-configuration-debugging.md) on your environment and instrument your application with the AWS X\-Ray SDK, the **Health** page adds links to the AWS X\-Ray console in the overview row\.

![\[Request metrics on the environment health page\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/enhanced-health-console-xray.png)

Choose a link to view traces related to the highlighted statistic in the AWS X\-Ray console\.

## Monitoring page<a name="health-enhanced-console-monitoringpage"></a>

The **Monitoring** page displays summary statistics and graphs for the custom Amazon CloudWatch metrics generated by the enhanced health reporting system\. See [Monitoring environment health in the AWS management console](environment-health-console.md) for instructions on adding graphs and statistics to this page\. 