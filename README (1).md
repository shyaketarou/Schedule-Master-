# LCY LinkedIn Calendar - GitHub Pages + Azure backend

This is the package for the architecture we agreed:
- GitHub = source code
- GitHub Pages = website
- Azure Functions = backend
- Azure Table Storage = persistent shared schedule + audit log

## Before the site can work

1. Create an Azure Storage Account.
2. Create an Azure Function App using Node.js 20.
3. Set Function App application setting:
   AzureWebJobsStorage = your Storage Account connection string.
4. In GitHub repository Settings -> Secrets and variables -> Actions, add:
   AZURE_FUNCTIONAPP_NAME
   AZURE_FUNCTIONAPP_PUBLISH_PROFILE
5. Push the repository. GitHub Actions deploys backend and frontend.
6. After the Function App is live, copy its HTTPS URL into `frontend/config.js` as API_BASE_URL.
7. Commit the config change. GitHub Pages redeploys.
8. Share the GitHub Pages URL.

## Important

Do not put Azure connection strings or publish profiles into frontend code.
`config.js` contains only the public HTTPS API URL.

The starter API is anonymous so anyone with the link can edit. For internal production, put Entra ID / Easy Auth in front of the API.
