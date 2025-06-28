
# Project History & Challenges

## Project Background
This project was started to create a proof-of-concept for a reusable, white-label voice interface powered by ElevenLabs. The initial goal was to build a system that could be deployed on a WordPress site, capture the full conversation, and log it to a central portal (Base44) for review and analysis.

## Key Decisions Made
- **Decision 1: Use a Node.js MCP Server:** An intermediary server was chosen to securely handle API keys and act as a proxy, rather than exposing keys on the client-side.
- **Decision 2: Dynamic Plugin Generation:** A generator was built inside Base44 to create the full WordPress plugin on-demand. This allows for easy configuration and deployment for different clients without manual coding.
- **Decision 3: Base44 for Backend/Portal:** The Base44 platform was used for the admin UI, data storage (ConversationLog entity), and backend Deno functions to accelerate development.

## Major Challenges Faced
- **Challenge 1: Caching on WordPress:** The client-side widget was aggressively cached by WordPress, preventing updates from being loaded.
  - **Resolution:** The plugin's PHP file was updated to enqueue the script with a version number based on the current timestamp (`time()`), forcing a fresh download on every page load.
- **Challenge 2: Duplicate Audio / Echo:** The widget script was initializing twice, causing the agent's voice to echo.
  - **Resolution:** A global flag (`window.jesschat_initialized`) was added to the widget JS to act as a lock, ensuring it can only run once per page load.
- **Challenge 3: Incomplete Conversation Logging:** Initial versions only logged "start" and "end" events, not the actual transcript.
  - **Resolution:** This is the current primary focus. The widget and MCP server logic are being updated to handle and persist the full message stream from the WebSocket.

## Technical Debt & Known Issues
- **Issue 1: Monolithic Widget:** The `jesschat-widget.js` file contains all logic for UI, WebSocket connection, audio handling, and logging. This should be refactored into smaller, more manageable modules.
- **Issue 2: Tight Coupling to WordPress:** The system is currently designed specifically for WordPress. It needs to be refactored into a platform-agnostic JavaScript SDK with thin adapters for different platforms (WordPress, Wix, etc.).
- **Issue 3: Lack of Automated Tests:** There is currently zero test coverage.

## Lessons Learned
- Caching is a major consideration in WordPress plugin development.
- Robust initialization guards are crucial for embeddable widgets to prevent conflicts.
- A clear separation between the core SDK and platform-specific adapters is essential for building a truly reusable product.
