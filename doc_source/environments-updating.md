# Configuration changes<a name="environments-updating"></a>

When you modify configuration option settings in the **Configuration** section of the [environment management console](environments-console.md), AWS Elastic Beanstalk propagates the change to all affected resources\. These resources include the load balancer that distributes traffic to the Amazon EC2 instances running your application, the Auto Scaling group that manages those instances, and the EC2 instances themselves\.

Many configuration changes can be applied to a running environment without replacing existing instances\. For example, setting a [health check URL](environments-cfg-clb.md#using-features.managing.elb.healthchecks) triggers an environment update to modify the load balancer settings, but doesn't cause any downtime because the instances running your application continue serving requests while the update is propagated\.

Configuration changes that modify the [launch configuration](command-options-general.md#command-options-general-autoscalinglaunchconfiguration) or [VPC settings](command-options-general.md#command-options-general-ec2vpc) require terminating all instances in your environment and replacing them\. For example, when you change the instance type or SSH key setting for your environment, the EC2 instances must be terminated and replaced\. To prevent downtime during these processes, Elastic Beanstalk applies these configuration changes in batches, keeping a minimum number of instances running and serving traffic at all times\. This process is known as a [rolling update](using-features.rollingupdates.md)\.

[Immutable updates](environmentmgmt-updates-immutable.md) are an alternative to rolling updates where a temporary Auto Scaling group is launched outside of your environment with a separate set of instances running on the new configuration, which are placed behind your environment's load balancer\. Old and new instances both serve traffic until the new instances pass health checks, at which time the new instances are moved into your environment's Auto Scaling group and the temporary group and old instances are terminated\.

**Warning**  
During managed platform updates with instance replacement enabled, immutable updates, and deployments with immutable updates enabled all instances are replaced\. This causes all accumulated [Amazon EC2 Burst Balances](https://docs.aws.amazon.com/AWSEC2/latest/DeveloperGuide/burstable-performance-instances.html) to be lost\.


**Supported Update Types**  

| Rolling update setting | Load balanced environments | Single\-instance environments | Legacy Windows server environments† | 
| --- | --- | --- | --- | 
|  Disabled  |  ✓  |  ✓  |  ✓  | 
|  Rolling Based on Health  |  ✓  |  ☓  |  ✓  | 
|  Rolling Based on Time  |  ✓  |  ☓  |  ✓  | 
|  Immutable  |  ✓  |  ✓  |  ☓  | 

† For the purpose of this table, a *Legacy Windows Server Environment* is an environment based on a [Windows Server platform configuration](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.net) that use an IIS version earlier than IIS 8\.5\.

**Topics**
+ [Elastic Beanstalk rolling environment configuration updates](using-features.rollingupdates.md)
+ [Immutable environment updates](environmentmgmt-updates-immutable.md)