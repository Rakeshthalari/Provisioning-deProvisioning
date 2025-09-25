<h1>User Provisioning & Deprovisioning Automation in Okta</h1>



<h2>Project Overview</h2>
Automating user provisioning and deprovisioning ensures secure, efficient, and compliant identity lifecycle management. This project demonstrates how to integrate Okta with an HR system (or Active Directory) to:<br>
Automatically create new users in Okta.<br>
Assign applications and groups based on roles and departments.<br>
Automatically deactivate and deprovision users upon termination.<br>
Keep identity lifecycle events logged for audit and compliance.
<br/>


<h2>Key Features</h2>
Event-Driven Provisioning: Triggered when a new hire record is created in HR system.<br>
Attribute Mapping: Department, Job Title, and Location mapped to Okta attributes.<br>
Group-Based Access: RBAC rules applied for app access.<br>
Automated Deprovisioning: Disabled accounts synced back from HR termination.<br>
Audit Logging: JSON logs stored for compliance.

<h2>Implementation</h2>
Trigger: New employee record from HRIS or AD feed.<br>
Actions: <br>
Create Okta user.<br>
Assign groups based on department.<br>
Provision into target apps.

<h2>Deprovisioning Workflow</h2>
Trigger: HR system marks employee as terminated.<br>
Actions:<br>
Suspend user in Okta.<br>
Remove group assignments.<br>
Deactivate from all integrated applications.

<h2>Sample Okta API Script (Python)</h2>
import requests<br>

OKTA_DOMAIN = "https://your-okta-org.okta.com"<br>
API_TOKEN = "your_api_token"<br>

headers = {<br>
    "Authorization": f"SSWS {API_TOKEN}",<br>
    "Content-Type": "application/json"<br>
}<br>

def create_user(first_name, last_name, email, department):<br>
    url = f"{OKTA_DOMAIN}/api/v1/users?activate=true"<br>
    payload = {<br>
        "profile": {<br>
            "firstName": first_name,<br>
            "lastName": last_name,<br>
            "email": email,<br>
            "login": email,<br>
            "department": department<br>
        },<br>
        "credentials": {<br>
            "password": {"value": "TempPass@123"}<br>
        }<br>
    }<br>
    response = requests.post(url, headers=headers, json=payload)<br>
    return response.json()<br>

Example Usage<br>
user = create_user("John", "Doe", "john.doe@example.com", "Engineering")<br>
print(user)<br>


