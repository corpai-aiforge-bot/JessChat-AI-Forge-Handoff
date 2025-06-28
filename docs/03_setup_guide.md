
# Development Setup Guide

## Prerequisites
- **Node.js:** v16 or later
- **WordPress:** A local or remote development environment.
- **Accounts:**
    - GitHub account
    - Render.com account
    - ElevenLabs account with an API key
    - Base44 account

## Environment Variables (for MCP Server on Render.com)
Create a `.env` file in the root of the Node.js project or set these in the Render.com dashboard.
```env
# Your ElevenLabs API Key
ELEVENLABS_API_KEY=sk_...

# The ID of the ElevenLabs agent to use
AGENT_ID=your_elevenlabs_agent_id

# The secure webhook URL for logging conversations to your Base44 portal
# (e.g., https://app.base44.com/functions/YOUR_APP_ID/logConversation)
BASE44_LOGGING_WEBHOOK_URL=https://app.base44.com/functions/...
```

## Installation Steps

### 1. MCP Server Setup
1.  Clone the repository from GitHub.
2.  Navigate to the `/src/mcp-server` directory.
3.  Install dependencies: `npm install`
4.  Create a `.env` file and populate it with the variables above.

### 2. WordPress Plugin Setup
1.  Generate the latest version of the plugin from the "WordPress Plugin Generator" page in the Base44 portal.
2.  Install the downloaded .zip file as a new plugin in your WordPress admin dashboard.
3.  Activate the plugin.
4.  Go to **Settings -> JessChat** in your WordPress admin and configure:
    - **MCP Server URL:** The URL of your deployed Render.com application.
    - **Client ID:** A unique identifier for this website.
    - **Agent ID:** The ElevenLabs agent ID you want to use.

## Running the Application
- **MCP Server (Development):** `npm run dev` (if nodemon is installed) or `node server.js`
- **WordPress Plugin:** Activate it in WordPress.

## Deployment
The MCP server is set up for continuous deployment from GitHub to Render.com.
1.  Connect your GitHub repository to a new "Web Service" on Render.com.
2.  Set the environment variables in the Render dashboard.
3.  Set the Build Command to: `npm install`
4.  Set the Start Command to: `node src/mcp-server/server.js`
5.  Any push to the main branch will automatically trigger a new deployment.
