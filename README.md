# Azure Static Web App

A React application built with Vite, ready to be deployed to Azure Static Web Apps.

## Project Structure

```
azure-static-web-app/
├── .github/
│   └── workflows/
│       └── azure-static-web-apps.yml   # CI/CD pipeline for Azure Static Web Apps
├── src/
│   ├── App.jsx
│   ├── App.css
│   ├── main.jsx
│   └── index.css
├── azure-static-web-app.config.json    # App configuration
├── index.html
├── package.json
└── vite.config.js
```

## Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn

### Local Development

```bash
cd azure-static-web-app
npm install
npm run dev
```

The app will run at `http://localhost:5173`

### Build

```bash
npm run build
```

The built output will be in the `dist/` directory.

## Deployment to Azure Static Web Apps

### Step 1: Set up GitHub Repository

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
gh repo create azure-static-web-app --public --push --source=.
```

### Step 2: Create Azure Static Web App

You'll need an Azure subscription. Visit [portal.azure.com](https://portal.azure.com) to create one if you don't have it.

```bash
# Login to Azure
az login

# Create resource group
az group create --name <resource-group-name> --location <location>

# Create static web app
az staticwebapp create --name <app-name> --resource-group <resource-group-name> --location <location>

# Link GitHub repository
az staticwebapp github connect --name <app-name> --repo <your-username>/<repo-name> --branch main

# Get the API token for GitHub secrets
az staticwebapp secrets list --name <app-name> --query "properties.apiKey" -o tsv
```

### Step 3: Add GitHub Secret

1. Go to your GitHub repository
2. Navigate to **Settings > Secrets and variables > Actions**
3. Add a new repository secret named `AZURE_STATIC_WEB_APPS_API_TOKEN` with the value from the previous command

### Step 4: Push and Deploy

```bash
git push origin main
```

The GitHub Actions workflow will automatically build and deploy your app.

## Azure Static Web Apps Features

- **Automatic CI/CD**: Push to `main` triggers deployment
- **Preview Environments**: Each PR gets a preview URL
- **Custom Domains**: Support for custom domains
- **Authentication**: Built-in auth with Microsoft, GitHub, Twitter
- **APIs**: Serverless API functions support

## Resources

- [Azure Static Web Apps Documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/)
- [Vite Documentation](https://vitejs.dev/)
- [React Documentation](https://react.dev/)