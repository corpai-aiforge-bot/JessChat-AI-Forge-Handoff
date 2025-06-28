
## GitHub Repository URL: https://github.com/corpai-aiforge-bot/JessChat-AI-Forge-Handoff

## Basic Information
- **Current Status:** deployment_ready
- **Completion Percentage:** 85%
- **Project Description:** JessChat is a versatile, white-label voice interface module designed for easy integration into websites (initially WordPress). It connects to a custom MCP (Model Context Protocol) server for conversation logging, lead capture, and routing to a Base44 portal.

## Technical Specifications
- **Technology Stack:** Node.js (Express.js), WordPress (PHP, JS, CSS), Base44 (React, Deno), ElevenLabs API, Render.com
- **Architecture Overview:** See `docs/02_architecture.md`
- **Database Schema:** A single "ConversationLog" entity in Base44. See schema details in `docs/02_architecture.md`.
- **External Dependencies:** ElevenLabs API, Render.com Hosting, Base44 Platform

## Environment & Setup
- **Required Environment Variables:** See `docs/03_setup_guide.md`
- **Setup Instructions:** See `docs/03_setup_guide.md`

## Implementation Status
- **Completed Features:** Voice agent creation (ElevenLabs), MCP Server for signed URL proxy, Conversation logging (start/end events), Dynamic WordPress plugin generation, Fixes for audio playback and widget display.
- **In-Progress Features:** Full conversation transcript capture and logging.
- **Pending Features (The Missing 15%):**
  - Robust, real-time transcript capture from WebSocket stream.
  - CRM-agnostic routing hub on MCP server.
  - Platform-agnostic JS SDK (decoupling from WordPress).
  - Automated testing suite.
- **Known Issues & Technical Debt:** See `docs/01_history.md`
