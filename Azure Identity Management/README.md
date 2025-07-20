# Proof of Concept: Identity & Access Management for Victoria Police



---

## Scenario

Victoria Police is planning a cloud-based modernization of its internal IT systems to:

- Strengthen identity security and reduce internal risk.  
- Centralize user and role management using Microsoft Azure Entra ID.  
- Enforce Multi-Factor Authentication (MFA) for high-risk roles like system administrators and detectives.  
- Organize staff into security groups based on operational divisions (e.g., Patrol, Investigations, Admin Support).  

This proof of concept offers a secure and scalable identity management structure for real law enforcement use cases.

**Note:** This is a self-directed project inspired by the real-world needs of government agencies such as Victoria Police. It is not affiliated with or commissioned by Victoria Police.

---

## Requirements

1. Create an Azure Entra ID tenant with users and departments.  
2. Organize users into department-based security groups.  
3. Assign Role-Based Access Control (RBAC) where appropriate.  
4. Enforce MFA for high-privilege roles (e.g., Global Admin, Detective).  
5. Demonstrate a secure sign-in process with screenshots.  
6. Document the structure and benefits.

---

## Core Technologies and Benefits

### 1. Azure Entra ID (formerly Azure Active Directory)

**Key Features:**

- Central identity store for users and groups  
- Supports secure sign-in  
- Integrates with Conditional Access & MFA  

**Benefits:**

- Single sign-on (SSO) for all users  
- Simplifies user management  
- Enables scalable and secure access policies  

---

### 2. Security Groups in Entra ID

**Key Features:**

- "Assigned" membership for manual user control  
- Can be used in RBAC and Conditional Access  

**Benefits:**

- Easier management of permissions  
- Reduces administrative overhead  
- Supports least privilege principle  

---

### 3. Role-Based Access Control (RBAC)

**Key Features:**

- Over 70 built-in roles  
- Assignable at resource, resource group, or subscription level  

**Benefits:**

- Fine-grained access control  
- Follows the principle of least privilege  
- Logs all access for auditing  

---

### 4. Multi-Factor Authentication (MFA)

**Key Features:**

- Enforced per user or via Conditional Access  
- Supports phone call, SMS, or app notifications  

**Benefits:**

- Stronger account protection  
- Prevents unauthorized access, especially for high-risk users  
- Meets compliance requirements  

---

### 5. Conditional Access

**Key Features:**

- If-then rules (e.g., “If user is admin, require MFA”)  
- Integrated with risk signals  

**Benefits:**

- Enforces targeted security without disrupting all users  
- Essential for real-world enterprise security  
- Prevents over-permission and misuse  

---

## Internal User List

| Display Name | UPN / Email Address | Job Title | Role | Description | Security Group Name | Access Risk Level |
|--------------|----------------------|-----------|------|-------------|-------------|--------------------|
| Alice Taylor | Alice.Taylor@xxx.onmicrosoft.com | Detective Sergeant | Storage Blob Data Reader | Investigates complex crimes, moderate access to sensitive case files | SG-Investigations-STD | Medium |
| Ben Singh | Ben.Singh@xxx.onmicrosoft.com | Digital Forensics Officer | Storage Blob Data Contributor | Access to digital evidence, tools, devices | SG-DigitalOps-STD | High |
| Cara Jones | Cara.Jones@xxx.onmicrosoft.com | Admin Assistant | Reader | Handles internal admin docs | SG-AdminSupport-LTD | Medium |
| David Tan | David.Tan@xxx.onmicrosoft.com | ICT Systems Admin | Contributor | Full admin access to Azure resources | SG-ITAdmin-High | High |
| Emma Zhao | Emma.Zhao@xxx.onmicrosoft.com | Senior HR Advisor | Storage Blob Data Contributor | Access to personnel records | SG-HR-STD | High |
| Grace Li | Grace.Li@xxx.onmicrosoft.com | Communications Officer | Reader | Press releases, media access | SG-Media-LTD | Medium |
| Henry White | Henry.White@xxx.onmicrosoft.com | Cyber Threat Analyst | Monitoring Contributor | Monitors alerts, high-risk access | SG-CyberSec-High | High |
| Jason Baker | Jason.Baker@xxx.onmicrosoft.com | Traffic Officer | None | Mobile access only, no sensitive systems | SG-FieldOps-LTD | Low |

**Naming convention for security group:**  
`SG-<Department/Function>-<AccessLevel>`

**Access Levels:**

- **High:** Full admin control  
- **STD:** Standard user access (only what they need to perform role)  
- **LTD:** Read-only access  

---

## Steps

### 1. Prerequisites

- Active Azure Subscription  
- Role as Global Administrator or Privileged Role Administrator  

---

### 2. Create Users

1. Go to **Azure Portal > Microsoft Entra ID > Users**  
2. Select **+ New user > Create user**  
3. Fill in:
    - UPN: `e.g., Jason.Baker`
    - Display Name: `Jason Baker`
    - Password: Auto-generated or manual  
    - Job Title: `Traffic Officer`  
    - Location: `Australia`  
![Alt Text](assets/p1.png)
![Alt Text](assets/p2.png)
![Alt Text](assets/p3.png)
![Alt Text](assets/p4.png)
4. Click **Create**  
5. Repeat for all users  

---

### 3. Enforce MFA

- Go to **Users > Multi-Factor Authentication**  
- Select users and enable MFA  
![Alt Text](assets/p5.png)

---

### 4. Create Security Groups

1. Go to **Entra ID > Groups > + New Group**  
2. Type: **Security**  
3. Name: e.g., `SG-ITAdmin-High`  
4. Description: e.g., `IT Admins – full access`  
5. Membership: **Assigned** 
![Alt Text](assets/p6.png) 
6. Click **Create**  
7. Add members after creation  
8. Repeat for all groups  

---

### 5. Add Users to Security Groups

1. Go to each group (e.g., SG-ITAdmin-High)  
2. Click **Members > + Add**  
3. Select relevant users  
4. Click **Select**  
![Alt Text](assets/p7.png)
![Alt Text](assets/p8.png)
5. Repeat for other groups  

---

### 6. Create a Resource (e.g., Storage Account)

1. Go to **Azure Portal > Create a Resource > Storage account**  
2. Name: `vicpolstorage01`  
3. Region: `Australia East`  
![Alt Text](assets/p9.png)
4. Click **Review + Create > Create**  

---

### 7. Assign RBAC Roles to Groups

1. Open the Storage Account > **Access Control (IAM)**  
2. Click **+ Add > Add role assignment**  
3. Role: e.g., `Reader`, `Contributor` 
![Alt Text](assets/p10.png) 
4. Assign to: **Group**, not individual  
5. Select relevant group (e.g., SG-ITAdmin-High)  
![Alt Text](assets/p11.png)
6. Click **Review + assign**  
7. Repeat as needed using least privilege  

---

### 8. Test Login

- Use **InPrivate/Incognito** window  
- Sign in as a test user (e.g., `Jason.Baker`)  
- Complete MFA and password reset  
![Alt Text](assets/p12.png)
- Verify access restrictions  
![Alt Text](assets/p13.png)

---

## Lessons Learned

- Enforcing MFA significantly enhances security.  
- Clear naming conventions reduce errors and improve manageability.  
- Security groups + RBAC streamline access control and auditing.  
- PowerShell and Cloud Shell improve automation for bulk provisioning.  
- Always apply least privilege at the group level for efficiency and security.  

---

## Outcomes

- Developed a secure, scalable Microsoft Entra ID structure  
- Demonstrated identity and access management best practices  
- Applicable to government agencies, law firms, and regulated industries  
