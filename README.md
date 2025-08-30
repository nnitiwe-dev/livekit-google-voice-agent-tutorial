 # Building Your First Real-Time AI Voice Agent (PART 2)

 Welcome back to our LiveKit voice agent series! Last week, we explored the fundamentals of voice agents using a [Jupyter notebook tutorial](https://colab.research.google.com/drive/19jjRT40RVWTojwZQlr88dpWXoQrXwrIB?usp=sharing) where we built and tested a basic voice agent directly in the notebook environment. This gave us a solid foundation for understanding how LiveKit agents work with speech recognition, language models, and text-to-speech.

## What We're Building This Week

This week, we're taking a significant step forward by building a **production-ready, full-stack voice agent application** that includes:

- 🎙️ **Web-based React frontend** with real-time voice interaction
- 🐍 **Python backend** running LiveKit agents
- 🌐 **Real-time audio streaming** between browser and agent
- ⚡ **Production deployment** on a cloud server

## Why Move Beyond Notebooks?

While notebooks are excellent for learning and prototyping, real-world voice applications need:

1. **User-friendly interfaces** - A polished web interface that users can actually interact with
2. **Scalable architecture** - Separate frontend and backend that can handle multiple users
3. **Production readiness** - Proper deployment, error handling, and monitoring
4. **Real-time performance** - Low-latency voice interactions that feel natural

## What You'll Learn

By the end of this tutorial, you'll have:

- ✅ Set up a LiveKit Cloud project with proper authentication
- ✅ Built a React frontend with real-time voice capabilities
- ✅ Deployed a Python voice agent backend on a cloud server
- ✅ Integrated Gemini LLM, Google Speech-to-Text and Text-to-Speech API
- ✅ Configured production-ready deployment with proper error handling

## Architecture Overview

Here's how our full-stack voice agent will work:

```
┌─────────────────┐    WebRTC     ┌──────────────────┐
│  React Frontend │ ◄───────────► │  LiveKit Cloud   │
│  (Browser)      │               │  (Relay Server)  │
└─────────────────┘               └──────────────────┘
                                           │
                                           │ Agent Protocol
                                           ▼
                                  ┌──────────────────┐
                                  │  Python Agent    │
                                  │  (Your Server)   │
                                  └──────────────────┘
                                           │
                        ┌──────────────────┼──────────────────┐
                        │                  │                  │
                        ▼                  ▼                  ▼
              ┌─────────────────┐ ┌────────────┐ ┌──────────────────┐
              │    Google STT   │ │ Gemini LLM │ │    Google TTS    │
              │ (Speech-to-Text)│ │ (LLM)      │ │ (Text-to-Speech) │
              └─────────────────┘ └────────────┘ └──────────────────┘
```

## Tutorial Structure

We'll build this application step by step:

1. **LiveKit Cloud Configuration** - Create and configuring our LiveKit project and Sandbox environments (React Frontend)
2. **Server Environment Setup** - Setting up our development environment (installing libraries)
3. **Python Agent Development** - Building our voice agent backend
4. **Integration & Testing** - Connecting all components together
5. **Production Deployment** - Deploying to a cloud server

## STEPS

1. Visit [https://cloud.livekit.io/](https://cloud.livekit.io/) and create a project.
2. Add create a Sandbox and add to the project created. (no need for Video, Chat features).
3. Clone this Repo [https://github.com/nnitiwe-dev/livekit-google-voice-agent-tutorial](https://github.com/nnitiwe-dev/livekit-google-voice-agent-tutorial).
4. Setup your Environment Variables (save to `.env` file):
    ```
    GOOGLE_API_KEY = your_google_api_key
    ELEVEN_API_KEY = your_eleven_api_key
    LIVEKIT_URL = your_livekit_url
    LIVEKIT_API_KEY = your_livekit_api_key
    LIVEKIT_API_SECRET = your_livekit_api_secret
    GOOGLE_APPLICATION_CREDENTIALS = path_to_your_google_application_credentials_json_file
    ```
5. Visit [https://docs.astral.sh/uv/getting-started/installation/](https://docs.astral.sh/uv/getting-started/installation/) and install `uv`.
   UV is a next-generation Python package installer and resolver written in Rust by the team at Astral (creators of Ruff). It's designed to be a drop-in replacement for pip and other Python packaging tools, but significantly faster and more reliable.

   **Linux:**
   `curl -LsSf https://astral.sh/uv/install.sh | sh`

   **Mac:**
   `brew install uv`

   **Windows:**
   `powershell -c "irm https://astral.sh/uv/install.ps1 | more"`

   **using pip:**
   `pip install uv`

6. Install dependencies:
   ```console
    cd livekit-google-voice-agent-tutorial
    uv sync
   ```
7. Download certain models such as Silero VAD and the LiveKit turn detector:
   ```console
   uv run python src/agent.py download-files
   ```
8. To run the agent for use with a frontend or telephony, use the `dev` command:
  ```console
  uv run python src/agent.py dev
  ```
9. In production, use the `start` command:
  ```console
  uv run python src/agent.py start
  ```