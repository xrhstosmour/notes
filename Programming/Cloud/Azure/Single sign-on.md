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
	    - **Use `user_impersonation` as Scope name in case of `Single Tenant` application, because it is the only option which seems to be working**
    - Who can consent
    - Admin/User consent display name
    - Admin/User consent description
13. Navigate to **Authorized client applications**, select **Add a client application**. Enter the Client ID and ensure the Authorized scope is checked before adding the application.
14. Under **API permissions** in the **Manage** tab, choose **Add a permission**. In the **Microsoft APIs** section, select **Microsoft Graph**. Choose **Delegated permissions**, navigate to **Directory**, and select **Directory.AccessAsUser.All** and **Directory.Read.All**. Click **Add permissions**. Finally, grant admin consent for these new permissions.
15. In the same section, click **Add a permission**, then go to **APIs my organization uses**. Select your API created in step 1, opt for **Delegated permissions**, and select the scope defined in step 12. Conclude by granting admin consent for these new permissions.

### Open API OAuth2 Setup

16. Repeat steps 6, 7, and 8 for Open API OAuth2 setup:
    - Name
    - Tenant type
    - Redirect URI (Type: SPA)
17. Enable Open API-backend communication via **API permissions** in the **Manage** tab. Add the permission for the scope created in step 12.

### Workflow

1. **Initiate Login Process**
   - Get the constructed Azure login URL.

2. **User Authentication**
   - Upon receiving the response, open the provided URL in a web browser.
   - Log in using your Microsoft account credentials.

3. **Consent and Authorization**
   - Follow the prompts to provide consent and authorize the application.

4. **Retrieve Authorization Code**
   - After authorization, a code will be sent back as a query parameter in the redirect URI.

5. **Token Exchange**
   - Exchange the received code for a Bearer token.

### Additional Resources

- For more details on setup and usage with FastAPI, visit [FastAPI Azure Auth](https://intility.github.io/fastapi-azure-auth/single-tenant/azure_setup).
