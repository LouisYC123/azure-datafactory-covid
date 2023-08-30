# Managed Identities

Steps:
1. Azure portal -> create a resource -> User Assigned Managed Identity -> give name and create
2. Head to your data lake that you want to grant access with the Managed Identity
3. Head to `Access Control (IAM)`
4. Add -> Add role assignment -> storage blob data owner
5. Assign access to `User, group, or service principal`
6. Click `Select members` and find the Managed Identity you created in step 1
