#sso #single-sign-on #azure #active-directory
### Initial Setup

1. Access Azure Portal at [Azure Portal](https://portal.azure.com/).
2. Log in using a Microsoft365 organizational account or any Microsoft Account (including free tier).
3. Navigate to **Azure Active Directory** via the search bar.
4. In the **Basics** tab, select your Microsoft Entra ID.
5. Under the **Configuration** tab, enter:
   - Organization name
   - Domain name
6. Post-creation, search for **App registrations** and click **New registration**.

### Application Registration

7. Provide the following details:
   - Name
   - Tenant type
   - Redirect URI (Type: Web)
8. Post-registration, record the Application (Client) ID and Directory (Tenant) ID.
9. In **Certificates & secrets**, create a new client secret with a description and expiry period. Note the value and ID.

### Configuration Adjustments

10. In the **Manage** tab, select **Manifest** and modify `accessTokenAcceptedVersion` to `2` in the .json file. Save changes.
11. In the **Manage** tab, go to **Expose an API** > **Add a scope**. Use the suggested scope and save.
12. Fill in the following scope details and set State to Enabled:
    - Scope name
    - Who can consent
    - Admin/User consent display name
    - Admin/User consent description
    - State

### Open API OAuth2 Setup

13. Repeat steps 6, 7, and 8 for Open API OAuth2 setup:
    - Name
    - Tenant type
    - Redirect URI (Type: SPA)
14. Enable Open API-backend communication via **API permissions** in the **Manage** tab. Add the permission for the scope created in step 12.

### Additional Resources

- For more details on setup and usage with FastAPI, visit [FastAPI Azure Auth](https://intility.github.io/fastapi-azure-auth/single-tenant/azure_setup).
