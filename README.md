# Identity-and-Access-Management
<p align="center">
<img src="https://i.imgur.com/ACuztn7.png"/>
</p>

<h1>Project Overview</h1>
<h3> Client: StartupCo - a fast-growing tech startup </h3>
<h3> Product: Fitness Tracking Application </h3>
<h3> Cloud Provider: AWS </h3>
<h3> Time on AWS: 3 months </h3>
<h3> Primary Goal: Secure AWS environment and implement access control best practices </h3>
<i>StartupCo initially prioritized speed to launch their product, leading to poor cloud security practices such as shared root credentials and no access control. As their infrastructure matures, they need to adopt AWS Identity and Access Management (IAM) best practices, implement Multi-Factor Authentication (MFA), and apply the Principle of Least Privilege.</i> - Everyone accesses all services via the root account. 

<h2>Securing the Root Account</h2>
<h3> Problems Identified: </h3>

- Shared AWS root credentials via chat
- No MFA enabled
- Used for daily operations
  
<p>
<img src="https://i.imgur.com/4rwjFCn.png"/>
</p>

<p>
<img src="https://i.imgur.com/pPSMMlT.png"/>
</p>

<p>
<img src="https://i.imgur.com/33dNsTS.png"/>
</p>

<h3> Actions Taken: </h3>

- Enabled MFA on root account 
- Stored credentials in AWS Secrets Manager and restricted access
- Created an Admin IAM user for daily operations
- Root account is now only used for break-glass recovery scenarios

<i> Why: Root accounts should never be used for regular tasks due to the risk of complete account compromise. </i>

<h2>IAM Users and Groups Design</h2>
<h3> Naming Convention: </h3>

- Users:  firstname.groupname
- Groups:  dev-group, ops-group, finance-group, analyst-group

<p>
<img src="https://i.imgur.com/mKo7AFI.png"/>
</p>

<p>
<img src="https://i.imgur.com/qeZOVsn.png"/>
</p>

<h3> Actions Taken: </h3>

- Created 10 individual IAM users
- Assigned users to appropriate groups
- Used AWS-managed and custom IAM policies

<h2>Security Requirments Enforced</h2>

<p>
<img src="https://i.imgur.com/ckyHGpd.png"/>
</p>

<h3> MFA Enforcement </h3>

- Enforced via IAM settings and AWS Organizations policy
- Verified all users configured MFA apps (e.g., DUO Authenticator)

<p>
<img src="https://i.imgur.com/v6GhOWi.png"/>
</p>

<h3> Password Policy Implemented </h3>

- Minimum length: 14 characters
- Require upper, lower, number, and special character
- Password expiration: 90 days
- Prevent reuse of last 5 passwords

<h3> Principle of Least Privilege</h3>

- Each group has only the permissions required for their roles
- No user can see or access other teams’ resources unnecessarily

<h2>IAM Group Permissions Implementation</h2>

<p>
<img src="https://i.imgur.com/niJjlI6.png"/>
</p>

<h3> Developer Group (dev-group) </h3>
<h4> Permissions: </h4>

- AmazonEC2FullAccess
- AmazonS3FullAccess
- CloudWatchFullAccess

<p>
<img src="https://i.imgur.com/bGnPPNX.png"/>
</p>

<h3> Operations Group (ops-group) </h3>
<h4> Permissions: </h4>

- AmazonEC2FullAccess
- AmazonRDSFullAccess
- AWSSystemManagement
- CloudWatchFullAccess

<p>
<img src="https://i.imgur.com/9UxAPE7.png"/>
</p>

<h3> Finance Group (finance-group) </h3>
<h4> Permissions: </h4>

- AWSBillingReadOnly
- Billing

<p>
<img src="https://i.imgur.com/gB99fKx.png"/>
</p>

<h3> Analyst Group (analyst-group) </h3>
<h4> Permissions: </h4>

- AmazonRDSReadOnly
- AmazonS3ReadOnly

<h2> Why These Changes Were Made: </h2>

- To eliminate high-risk shared credentials
- To enforce identity accountability
- To reduce attack surface using least privilege
- To comply with AWS security best practices

<h2> Key Outcomes: </h2>

- Identity & Access Management now structured
- Secure root and user login flow
- Role-based access separated cleanly
- Future-ready for compliance and audits
