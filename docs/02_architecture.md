
# System Architecture

## High-Level Overview
The JessChat system is a three-part architecture designed for modularity and security:
1.  **Frontend (WordPress Plugin):** A lightweight client-side widget that manages user interaction and the voice/audio stream.
2.  **Backend (Node.js MCP Server):** A secure intermediary that handles API key management, conversation session logic, and data routing.
3.  **Admin Portal (Base44):** A central hub for configuration, data viewing (conversation logs), and management tools like the WordPress Plugin Generator.

## Component Breakdown
- **Frontend:** A WordPress plugin containing a JavaScript widget (`jesschat-widget.js`). It communicates with the MCP server to get a temporary WebSocket URL from ElevenLabs and sends log data.
- **Backend:** A Node.js Express application deployed on Render.com. It has two primary roles:
    1.  Acts as a secure proxy to get a signed WebSocket URL from ElevenLabs, protecting the main API key.
    2.  Provides a `/conversation-log` endpoint that receives data from the widget and forwards it to the Base44 portal via a secure webhook.
- **Database:** A NoSQL-style data store within the Base44 platform. It uses a single primary entity: `ConversationLog`, which stores all session data, transcripts, and metadata.
- **External Services:**
    - **ElevenLabs:** Provides the core Conversational Voice AI API.
    - **Render.com:** Hosts the Node.js MCP server.
    - **GitHub:** Hosts the MCP server source code for CI/CD with Render.

## Data Flow
1. User clicks the chat widget on a WordPress site.
2. Widget JS calls the MCP server's `/signed-url` endpoint.
3. MCP server calls ElevenLabs with the secret API key and gets a temporary WebSocket URL.
4. MCP server returns the temporary URL to the widget.
5. Widget establishes a WebSocket connection with ElevenLabs using the temporary URL.
6. As the conversation happens, the widget sends transcript snippets (user and agent messages) to the MCP server's `/conversation-log` endpoint.
7. MCP server forwards this data to a Base44 Deno function (`logConversation`).
8. The Base44 function processes the data and saves it as a `ConversationLog` entity in the database.
9. Admins can view the formatted logs in the Base44 portal.

## Security Considerations
- The main `ELEVENLABS_API_KEY` is stored securely as an environment variable on the Render.com server and is never exposed to the client.
- The client-side widget only ever receives a temporary, time-limited WebSocket URL, minimizing risk.
- Communication between the MCP server and Base44 portal is done via a secure webhook URL.
