# AWS-cloud-IAM-Deployment-and-Configuration

## Project Overview
This project demonstrates the application of **cloud security controls in AWS**, focusing on **Identity and Access Management (IAM)**.  
The objective was to implement a **least-privilege policy**, assign it to a user group, and validate that access restrictions worked correctly on two tagged Amazon EC2 instances: **Audit** and **Sales**.

---

## Tools & Concepts
- **AWS IAM**: Users, groups, policies, account alias  
- **Amazon EC2**: Instance tagging and lifecycle actions  
- **JSON IAM Policies**: Effect, Action, Resource  
- **Principle of Least Privilege**: Restrict users to only necessary actions  
- **Policy Testing**: Verifying expected vs. actual access behavior  

---

## Tagging Strategy
Two EC2 instances were tagged for policy enforcement:

| Instance | Tag Key     | Tag Value |
|----------|-------------|-----------|
| audit    | Environment | Audit     |
| sales    | Environment | Sales     |

---

## IAM Policy
A custom JSON policy was created to **block stop/start actions on the Audit instance** while allowing them on the Sales instance.  
This policy enforces the least-privilege principle by restricting sensitive resources.

---

## IAM Configuration
1. **Account Alias**: Set a custom account alias for easier user login.  
2. **IAM Group**: Created a group named `Developers`.  
3. **Policy Attachment**: Attached the custom policy (`CybertechAuditEnvPolicy`) to the group.  
4. **IAM Users**: Added individual users requiring controlled EC2 access.  

---

## Access Methods
- **AWS Management Console** – via the custom alias URL  
- **AWS CLI** – using programmatic access keys  

---

## Testing the Policy
Policy behavior was tested on EC2 lifecycle actions:

| Test Action         | Expected Result | Actual Result             |
|----------------------|----------------|---------------------------|
| Stop Audit instance | Denied         | Access denied error shown |
| Stop Sales instance | Allowed        | Instance stopped          |
| Start Audit instance| Denied         | Access denied error shown |
| Start Sales instance| Allowed        | Instance started          |

---

## Conclusion
This project validated how **IAM policies, tagging, and least-privilege principles** can be applied to secure cloud environments in AWS.  
By restricting actions based on resource tags, security teams can ensure that critical infrastructure (e.g., the Audit server) remains protected while maintaining operational flexibility for less sensitive resources.  
