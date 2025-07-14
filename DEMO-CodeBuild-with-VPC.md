## DEMO - CodeBuild with VPC

1. Make sure you have a **codeCommit Repo** before starting with **CodeBuild**.
2. Create a CodeBuild Project, Use below image for reference.
   <img width="802" height="915" alt="Screenshot 2025-07-14 at 12 36 53 PM" src="https://github.com/user-attachments/assets/8edca0fd-874d-4809-952a-55bca02adc2f" />

3. Make sure you have a VPC created with private and public subnet setup with internet gateway and NAT - if not follow the documentation : [README.md](https://github.com/Ashutoshdikshit07/SecureScalableAWSDeployment/blob/bcdd932baf86020f773c9e29aa53b33cce2e7d26/README.md)
4. Look for additional configuration and select VPC and subnet that you just created and validate it- Refer below screenshot.
    <img width="890" height="808" alt="Screenshot 2025-07-14 at 1 13 49 PM" src="https://github.com/user-attachments/assets/957fdd3c-a544-4213-be9b-7a99571f9e82" />
5. Create build project. Now our build project can access resource within that VPC.
