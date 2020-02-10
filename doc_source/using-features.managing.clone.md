# Clone an Elastic Beanstalk environment<a name="using-features.managing.clone"></a>

You can use an existing Elastic Beanstalk environment as the basis for a new environment by cloning the existing environment\. For example, you might want to create a clone so that you can use a newer version of the solution stack used by the original environment's platform\. Elastic Beanstalk configures the clone with the same environment settings used by the original environment\. By cloning an existing environment instead of creating a new environment, you don't have to manually configure option settings, environment variables, and other settings\. Elastic Beanstalk also creates a copy of any AWS resource associated with the original environment\. However, during the cloning process, Elastic Beanstalk doesn't copy data from Amazon RDS to the clone\. After you create the clone environment, you can modify environment configuration settings as needed\.

**Note**  
Elastic Beanstalk doesn't include any unmanaged changes to resources in the clone\. Changes to AWS resources that you make using tools other than the Elastic Beanstalk console, command\-line tools, or API are considered unmanaged changes\.

## AWS management console<a name="using-features.managing.clone.CON"></a>

**To clone an environment**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. From the region list, select the region that includes the environment that you want to work with\.

1. Navigate to the [management page](environments-console.md) for your environment\.

1. On the environment dashboard, choose **Actions**, and then do one of the following: 
   + Choose **Clone Environment** to clone the environment without any changes to the solution stack version\.
   + Choose **Clone with Latest Platform** to clone the environment, but with a newer version of the original environment's solution stack\.

1. On the **Clone Environment** page, review the information in the **Original Environment** section to verify that you chose the environment from which you want to create a clone\.

1. In the **New Environment** section, you can optionally change the **Environment name**, **Environment URL**, **Description**, **Platform**, and **Service role** values that Elastic Beanstalk automatically set based on the original environment\.
**Note**  
For **Platform**, only solution stacks with the same language and web server configuration are shown\. If a newer version of the solution stack used with the original environment is available, you are prompted to update, but you cannot choose a different stack, even if it is for a different version of the same language\. For more information, see [Elastic Beanstalk supported platforms](concepts.platforms.md)\.  
![\[Elastic Beanstalk clone environment configuration page\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-env-clone-env-latest.png)

1. When you are ready, choose **Clone**\.

## Elastic Beanstalk command line interface \(EB CLI\)<a name="using-features.managing.clone.CLI"></a>

Use the eb clone command to clone a running environment, as follows\.

```
~/workspace/my-app$ eb clone my-env1
Enter name for Environment Clone
(default is my-env1-clone): my-env2
Enter DNS CNAME prefix
(default is my-env1-clone): my-env2
```

You can specify the name of the source environment in the clone command, or leave it out to clone the default environment for the current project folder\. The EB CLI prompts you to enter a name and DNS prefix for the new environment\.

By default, eb clone creates the new environment with the latest available version of the source environment's platform\. To force the EB CLI to use the same version, even if there is a newer version available, use the `--exact` option\.

```
~/workspace/my-app$ eb clone --exact
```

For more information about this command, see [eb clone](eb3-clone.md)\.