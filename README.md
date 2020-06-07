Part 1
Complete the following steps:

Data durability and recovery
In order to achieve the highest levels of durability and availability in AWS you must take advantage of multiple AWS regions.

Pick two AWS regions. An active region and a standby region.
Use CloudFormation to create one VPC in each region. Name the VPC in the active region "Primary" and name the VPC in the standby region "Secondary".
NOTE: Be sure to use different CIDR address ranges for the VPCs. SAVE screenshots of both VPCs after they are created. Name your screenshots: primary_Vpc.png, secondary_Vpc.png

Highly durable RDS Database
Create a new RDS Subnet group in the active and standby region.
Create a new MySQL, multi-AZ database in the active region. The database must:
Be a “burstable” instance class.
Have only the “UDARR-Database” security group.
Have an initial database called “udacity.”
Create a read replica database in the standby region. This database has the same requirements as the database in the active region.
SAVE screenshots of the configuration of the databases in the active and secondary region after they are created. SAVE screenshots of the configuration of the database subnet groups as well as route tables associated with those subnets. Name the screenshots: primaryDB_config.png, secondaryDB_config.png, primaryDB_subnetgroup.png, secondaryDB_subnetgroup.png, primaryVPC_subnets.png, secondaryVPC_subnets.png, primary_subnet_routing.png, secondary_subnet_routing.png

Estimate availability of this configuration
Write a paragraph or two describing the achievable Recovery Time Objective (RTO) and Recovery Point Objective (RPO) for this Multi-AZ, multi-region database in terms of:

Minimum RTO for a single AZ outage
Minimum RTO for a single region outage
Minimum RPO for a single AZ outage
Minimum RPO for a single region outage
SAVE your answers in a text file named "estimates.txt"

Demonstrate normal usage
In the active region:

Create an EC2 keypair in the region
Launch an Amazon Linux EC2 instance in the active region. Configure the instance to use the VPC's public subnet and security group ("UDARR-Application").
SSH to the instance and connect to the "udacity" database in the RDS instance.
Verify that you can create a table, insert data, and read data from the database.
You have now demonstrated that you can read and write to the primary database
SAVE the log of connecting to the database, creating the table, writing to and reading from the table in a text file called "log_primary.txt"

Monitor database
Observe the “DB Connections” to the database and how this metric changes as you connect to the database
Observe the “Replication” configuration with your multi-region read replica.
SAVE screenshots of the DB Connections and the database replication configuration. Name your screenshots: monitoring_connections.png, monitoring_replication.png

Part 2
Failover And Recovery
In the standby region:

Create an EC2 keypair in the region
Launch an Amazon Linux EC2 instance in the standby region. Configure the instance to use the VPC's public subnet and security group ("UDARR-Application").
SSH to the instance and connect to the read replica database.
Verify if you are not able to insert data into the database but are able to read from the database.
You have now demonstrated that you can only read from the read replica database.
SAVE log of connecting to the database, writing to and reading from the table in a text file called "log_rr_before_promotion.txt"

SAVE screenshot of the database configuration now, before promoting the read replica database in the next step. Name your screenshot: rr_before_promotion.png

Promote the read replica
Verify that if you are able to insert data into and read from the read replica database.
You have now demonstrated that you can read and write the promoted database in the standby region.
SAVE log of connecting to the database, writing to and reading from the database in a text file named "log_rr_after_promotion.txt"

SAVE screenshots of the database configuration after the database promotion. Name your screenshot: rr_after_promotion.png

Part 3
Website Resiliency
Build a resilient static web hosting solution in AWS. Create a versioned S3 bucket and configure it as a static website.

Enter “index.html” for both Index document and Error document
Upload the files from the GitHub repo (under /project/s3/)
Paste URL into a web browser to see your website.
Save the screenshot of the webpage. Name your screenshot "s3_original.png" You will now “accidentally” change the contents of the website such that it is no longer serving the correct content

You will now “accidentally” change the contents of the website such that it is no longer serving the correct content

Change index.html to refer to a different “season”
Re-upload index.html
Refresh web page
SAVE a screenshot of the modified webpage. Name your screenshot "s3_season.png"

You will now need to “recover” the website by rolling the content back to a previous version.

Recover the index.html object back to the original version
Refresh web page
SAVE a screenshot of the modified webpage. Name your screenshot "s3_season_revert.png"

You will now “accidentally” delete contents from the S3 bucket. Delete “winter.jpg”

SAVE screenshots of the modified webpage and of the existing versions of the file showing the "Deletion marker". Name your screenshots: s3_deletion.png, s3_delete_marker.png

You will now need to “recover” the object:

Recover the deleted object
Refresh web page
SAVE a screenshot of the modified webpage. Name your screenshot "s3_delete_revert.png"
