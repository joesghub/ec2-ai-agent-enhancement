# ec2-ai-agent-enhancement
ServiceNow AI Agent that can identify EC2 instance IDs, and provide conversational remediation assistance to DevOps engineers at Netflix. It enhances the existing manual remediation system

## System Overview
Description of the enhanced EC2 remediation system with both manual and AI Agent capabilities

## Implementation Steps
Key configuration decisions for AI Agent integration with existing manual system

### [Step 1: Application Setup](https://github.com/joesghub/ec2-remediation-system?tab=readme-ov-file#step-1-application-setup)

### [Step 2: Table Setup](https://github.com/joesghub/ec2-remediation-system?tab=readme-ov-file#step-2-table-setup)

### [Step 3: AWS Integration Setup](https://github.com/joesghub/ec2-remediation-system?tab=readme-ov-file#step-3-aws-integration-configuration)

### [Step 4: UI Action and Script Include Setup](https://github.com/joesghub/ec2-remediation-system?tab=readme-ov-file#step-4-ui-action-and-script-include-implementation)

### [Step 5: EC2 Remediation Workflow Setup](https://github.com/joesghub/ec2-remediation-system?tab=readme-ov-file#step-5-flow-designer-workflow-creation)

In this version we stop our workflow at Action 4, in order to use the AI Agents capabilities. 

**Action 4:** Slack EC2 Instance Service Alert  

### Step 6: AI Agent Setup


![AI Agent Configuration]()

### Step 7: Script Tool Setup


![Script Tool Configuration]()

### Step 8: Agent Tool Setup


![Incident Record Lookup Agent Tool Configuration]()


![Incident Record Update Agent Tool Configuration]()



![Instance ID Lookup Agent Tool Configuration]()



### Step 9: Testing and Validation



![AI Agent Output]()


![Slack EC2 Instance Service Alert](https://github.com/joesghub/ec2-remediation-system/blob/main/screenshots/015%20flow%20a4%20slack%20issue.png?raw=true)

## Architecture Diagram
![Visual representation of the complete workflow](https://github.com/joesghub/ec2-ai-agent-enhancement/blob/main/Diagram.png?raw=true)

## Optimization


| Aspect                          | AI Agent Script                                                                             | Manual UI Action Script                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **Input Method**                | Takes **AWS `instance_id`** (e.g., `i-1234567890abcdef`), validates with regex.            | Takes **ServiceNow `sys_id`** (`sysparm_ec2_sys_id`) and looks up the related `instance_id`. |
| **Lookup Direction**             | Queries `x_snc_ec2_monito_0_ec2_instance` by **`instance_id`** to find matching record.   | Direct `.get(sys_id)` on `x_snc_ec2_monito_0_ec2_instance`, then retrieves `instance_id`. |
| **Return Format**               | Returns a **JavaScript object** (e.g., `{ success: "true", message: "..." }`).             | Returns a **JSON string** via `JSON.stringify()`, suitable for GlideAjax.                 |
| **Error Handling**              | Basic try/catch with simple message, logs errors but no stack trace.                       | Robust try/catch, logs **stack trace**, inserts remediation log even on exception.        |
| **Logging**                     | Creates remediation log, includes error message only on failure.                          | Creates remediation log with richer details, always logs error context/stack trace.      |
| **Best Use Case**               | Flows, Actions, or server-side scripts when AWS **instance ID is known upfront**.          | GlideAjax, UI Actions, or ServiceNow record-driven workflows where only **sys_id** is known. |



## DevOps Usage
Instructions for Netflix DevOps engineers on using both manual remediation and AI Agent conversation for different scenarios
