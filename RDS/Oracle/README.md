# AWS CloudFormation templates for Oracle databases migration.
AWS CloudFormation provides a common language to describe and provision all the infrastructure resources in AWS cloud environment. CloudFormation allows the use of a simple text file to model and provision, in an automated and secure manner, all the resources needed for the migration across all regions and accounts. Following are AWS CloudFormation templates for **the Oracle databases migration (using DataPump + S3 bucket)**. https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.html#Oracle.Procedural.Importing.DataPump.S3 for more details.

![picture](https://github.com/VNSNY/Cloudformation/blob/master/RDS/Oracle/DB_Migration_AWS.jpg)

## Description
- **1_AWS_S3_Creation.yml**: Creates the Amazon S3 bucket needed for the database migration. 
- **2_AWS_Integration_S3_RDS.yml**: Creates the Amazon role for the S3 integration with a Amazon RDS instance
- **3_AWS_OptionGroup_Creation.yml**: Creates the Amazon RDS Option Group for the Amazon RDS instance
- **4_AWS_RDS_Creation.yml**: Creates the Amazon RDS Oracle instance (target database) (https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-rds-database-instance.html for more details)

## Prerequisites
Below are the parameteres for the Amazon RDS instance CloudFormation template:

 Parameter Name | Description | Type | Required
--------------- | ----------- | ---- | --------
 pAWSUser	|	Name of the user creating/runing the CF template file	|	String	|	Yes
 pAllocatedStorage	|	 Allocated Storage Size (GB)	|	String	|	No
 pCharacterSetName	|	 Character Set to associate with the DB intance	|	String	|	Yes
 pDBInstanceClass	|	 Name of the compute and memory capacity classes of the DB instabce	|	String	|	Yes
 pDBInstanceIdentifier	|	 Name for the DB instance	|	String	|	Yes
 pDBName	|	 Name of the DB instance	|	String	|	No
 pDBParameterGroupName	|	 Name of an exisiting DB parameter group	|	String	|	No
 pDBSubnetGroupName	|	 A DB subnet group to associate with the DB instance	|	String	|	No
 pDeletionProtection	|	 Indicates wether the DB instance should have deletion protection enabled	|	Boolean	|	No
 pEnableCloudwatchLogsExports	|	 List of log types that need to be enabled for exporting to CloudWatch logs	|	String	|	No
 pEnablePerformanceInsights	|	 If set to True, enables Performance Insights for the DB instance	|	Boolean	|	No
 pEngine	|	 The database engine that the DB instance uses	|	String	|	Conditional
 pEngineVersion	|	 The version number of the DB engine that the DB instance uses	|	String	|	No
 pIops	|	 The number of I/O operations per second that the database provisions	|	Integer	|	Conditional
 pKmsKeyId	|	 The ARN of the AWS KMS master key that's used to encrypt the DB instance	|	String	|	No
 pLicenseModel	|	 The license model of the DB instance	|	String	|	No
 pMasterUsername	|	 The master user name for the DB instance	|	String	|	Conditional
 pMasterUserPassword	|	 The master password for the DB instance	|	String	|	Conditional
 pMonitoringInterval	|	 The interval, in seconds, between points when Amazon RDS collects enhanced monitoring metrics for the DB instance	|	Integer	|	Conditional
 pMonitoringRoleArn	|	 The ARN of the AWS Identity and IAM role that permits Amazon RDS to send enhanced monitoring metrics to Amazon CloudWatch	|	String	|	Conditional
 pMultiAZ	|	 Specifies if the database instance is a multiple Availability Zone deployment	|	Boolean	|	No
 pOptionGroupName	|	 The option group that this DB instance is associated with	|	String	|	No
 pPerformanceInsightsKMSKeyId	|	 The AWS KMS key identifier for encryption of Performance Insights data	|	String	|	No
 pPerformanceInsightsRetentionPeriod	|	 The amount of time, in days, to retain Performance Insights data	|	Integer	|	No
 pPort	|	 The port for the instance	|	String	|	No
 pPubliclyAccessible	|	 Indicates whether the DB instance is an internet-facing instance	|	Boolean	|	No
 pStorageEncrypted	|	 Indicates whether the DB instance is encrypted	|	Boolean	|	Conditional
 pVPCSecurityGroups	|	 A list of the VPC security group IDs to assign to the DB instance	|	List Of String	|	No
 pTagsKey	|	 Tag Key Name	|	String	|	No
 pTagsValue	|	 Tag Key Value	|	String	|	No
 pDeletionPolicy	|	 Deletion Policy 	|	List Of String	|	No


The following **parameters need to be existing before** the creation/execution of the Amazon RDS instance through the **4_AWS_RDS_Creation.yml** file.
- pDBParameterGroupName
- pKMSKeyId
- pMonitoringRoleArn
- pPerformanceInsightKMSKeyID
- pVPCSecurityGroups

## Steps
1. Create then run the **1_AWS_S3_Creation.yml** file in the Amazon CloudFormation console. 
2. Create then run the **2_AWS_Integration_S3_RDS.yml** file in the Amazon CloudFormation console. 
3. Create then run the **3_AWS_OptionGroup_Creation.yml** file in the Amazon CloudFormation console. 
4. Create then run the **4_AWS_RDS_Creation.yml** file in the Amazon CloudFormation console. 

## Post-Template action(s)
1. Affect manually the Amazon S3 integration managed IAM role to the Amazon RDS instance
