# IAM Roles

**1.Primitive Roles**:- Prior to Cloud IAM, primitive roles like Owner, Editor, and Viewer existed at the project level, providing coarse-grained access controls. 
- **viewer role**:- grants read-only access.
- **Editor role**:- Viewer permissions +  ability to modify the state of a resource.
- **Owner role**:- Editor permissions + permissions to manage roles along with setting up billing for a project.
#### Note:- 
- Primitive roles are acceptable only for Coarse-grained access controls[access is primarily determined by the assigned role rather than specific permissions or attributes]. Permissions are broader and less granular.
- If primitive roles are used in a project, they grant viewer, editor, and owner access to objects in **Cloud Storage**	

**2.Predefined Roles**:- These roles are generally associated with **AppEngine or BigQuery**. BigQuery uses fine-grained permissions on BigQuery resources[refer to a more granular level of access control where permissions are assigned at a detailed and specific level].

**3.Custom Roles**:- you can assign one or more permissions to a role and then assign that role to a user, group, or service account.
Custom roles are especially important when implementing the principle of least privilege, which states that users should be granted the minimal set of permissions needed for them to perform their jobs.**IAM is additive only**. 
- Users must have the **iam.roles.create permission** to be able to **create a custom role**.
- It means permissions cannot be revoked at a higher level(Folder) if they were granted at a lower level(Resource).
- Organization---->Folders--->Projects---->Resources

**Principle of least Privilege**:- It is the practice of limiting user access to only the resources and actions that are necessary for them to perform their job.

-  NAT purpose of a NAT (Network Address Translation) gateway is to allow private network resources to access the internet while maintaining security and preserving their private IP addresses.
- It is primarily used for translating private IP addresses to public IP addresses and enabling communication between private networks and the internet.

**Access Control Lists(ACL's)**:- They are used to control access to resources within a project or organization.
ACLs define the permissions that a user or group has to perform specific actions on resources such as instances, disks, networks, and buckets.
- when you need to control access to **individual objects**, you may need to use **access control lists (ACLs)**.

**Hash-based Message Authentication Code** (HMAC) keys are used to authenticate access to **Cloud Storage**. The permissions for 
HMAC keys include creating, deleting, and listing keys as well as getting and updating metadata

![Alt text](userVsJobusers.png)

## Service Account:-
- Service accounts are a type of identity often used with **VM instances and applications**, which are able to **make API calls** authorized by roles assigned to the service account.
- Service accounts **do not have passwords** and cannot be used to log in interactively via a browser. These accounts are **authenticated by a pair of public/private keys**.

- Use **service accounts** to grant permissions **to applications and processes running on non-human entities**,They are commonly used for authenticating and authorizing applications to access GCP services and resources without requiring human intervention.
- while use **IAM** to manage access control for **human users** and to set permissions for specific actions on GCP resources. It is used to manage who can do what in GCP and set permissions for actions like creating, modifying, or deleting resources.

### Bigtable and IAM
Access controls for Cloud Bigtable can be configured at the project, instance, or table level.

- Predefined roles for Cloud Bigtable include:
  - **Admin Role**: Administer any instance in a project, including creating new instances.
  - **User Role**: Allows for read and write access to tables.
  - **Reader Role**: Allows for read-only access to data in tables.
  - **Viewer Role**: Restricted to accessing the GCP console for Bigtable.
  - **roles/bigtable.reader** provides **read access to actual Bigtable data at the project or instance level via the Bigtable APIs**.
  - **roles/bigtable.viewer** only **allows viewing the Bigtable section** in the GCP Console UI.But **roles/bigtable.viewer does NOT grant permission to use the Bigtable client libraries or APIs to access any data**.

### DataFlow and IAM
  - **roles/dataflow.admin:** Gives permissions to create and manage jobs
  - **roles/dataflow.developer**: Gives permissions to execute and modify jobs
  - **roles/dataflow.viewer**: Gives permissions for read-only access to all Cloud Dataflow resources
  - **roles/dataflow.worker**: Gives permissions to a Compute Engine service account to execute work units of a pipeline

### Encryption at Rest

- Data at rest is encrypted by default in Google Cloud Platform.
- Data is encrypted at multiple levels, including the application, infrastructure, and device levels.
- Data is encrypted in chunks. Each chunk has its own encryption key, which is called a data encryption key.
- Data encryption keys are themselves encrypted using a key encryption key.

### Encryption in Transit(motion):-
- GCP uses a combination of authenticating sources and encryption to protect data in transit
- Data within the boundaries of the Google network is authenticated but may not be encrypted. 
- Data moving into and out of the physical boundaries of the Google network is encrypted
- Google uses **Application Layer Transport Security (ALTS)** for **authentication and encryption** within the Google Cloud Infrastructure.
- GCP offers encryption at rest and encryption in transit by default

**Server-side encryption**: Server-side encryption is a method where the encryption and decryption processes are handled by the cloud service provider (GCP) on the server side.When server-side encryption is enabled, GCP automatically encrypts the data at rest, meaning the data stored on disks or in backups.
GCP provides multiple options for server-side encryption, including:	

 **1.Google-managed encryption keys**: GCP generates and manages the encryption keys used to encrypt the data.

 **2.Customer-supplied encryption keys (CSEK)**: The encryption keys are generated and managed entirely by the customer including storage, who is responsible for providing the keys during encryption and retaining them for decryption.The keys are passed as arguments in API calls and stored in memory, but customer-supplied keys are not written to storage.

 **3.Customer-managed encryption keys (CMEK)**: The encryption keys are created and managed by the customer, who retains control over the keys but do not need keys to reside on their own key management infrastructure. **while GCP handles the encryption and decryption operations**. It enables customers to generate and store keys in GCP. They refer KMS based keys for the encryption. Cloud KMS keys can be destroyed, but there is a **24-hour delay** as a safety measure in case of accidental deletion or malicious intent. Cloud KMS keys can be used for application-level encryption in GCP services, including **Compute Engine, BigQuery, Cloud Storage, and Cloud Dataproc**.

**Client-side encryption**: Client-side encryption is a method where the encryption and decryption processes are performed by the client (application or user) before the data is sent to the server (GCP).With client-side encryption, the data is encrypted on the client side using encryption algorithms and keys chosen by the client. Since the encryption process occurs before the data reaches the server, GCP only sees and stores the encrypted data without having access to the encryption keys or the ability to decrypt the data


**Data Loss Prevention(DLP) API**:- It is a service that can detect sensitive information in text and images, redact or mask sensitive information, and perform risk analysis. Two types of Data Loss Prevention jobs: 
- **Inspection jobs** scan content for sensitive information using InfoTypes that you specify and generate reports on the location and type of sensitive information found.
- **Risk analysis jobs** calculate the likelihood that data could be re-identified.

**Health Insurance Portability and Accountability Act (HIPAA)**:-It is a federal law in the United States that protects individuals’ healthcare information.

**Children’s Online Privacy Protection Act(COPPA)**:-It is a federal law in the United States to define and enforce regulations regarding children’s online privacy.

**Federal Risk and Authorization Management Program(FedRAMP)**:-It is designed to ensure that cloud systems used 
by governments are adequately secure, reduce duplication of effort, and reduce risk management costs

**General Data Protection Regulation(GDPR)**:- The purpose of this regulation is to standardize privacy protections across the EU, grant controls to individuals over their private information, and specify security practices required for organizations holding private information of EU citizens.

**datalab vs dataprep**

1. **Cloud Datalab**:
   - Cloud Datalab is an interactive development environment for data exploration, analysis, and machine learning.
   - It allows data analysts, data scientists, and developers to work with big data using Jupyter notebooks.
   - Datalab provides support for various programming languages like Python, SQL, and JavaScript, making it versatile for data manipulation and visualization.
   - Users can run queries against BigQuery, analyze data, create visualizations, and develop machine learning models all within the same environment.

2. **Cloud Dataprep**:
   - Cloud Dataprep, previously known as Trifacta, is a data preparation tool that helps clean, transform, and enrich raw data from diverse sources.
   - It offers a visual interface for data wrangling, allowing users to clean and reshape data without writing code.
   - Dataprep provides automated data transformation suggestions and highlights potential data quality issues, making the data preparation process more efficient.
   - The tool can handle data from various sources, such as CSV, Excel, JSON, and relational databases.
   -  Cloud Dataprep is used to build and maintain the transformation recipes, and execute them on a scheduled basis

