# Azure OpenAI Real-time Voice Chat Application

## 1. Project Overview
This repository contains a sample program extracted from the JavaScript rt-client-0.5.0 code portion of Microsoft's aoai-realtime-audio-sdk.
It's designed with a simple structure to allow for easy experience and understanding of speech recognition and AI responses.

### 1.1 Purpose

- Demonstrate real-time voice chat functionality using Azure OpenAI.
- Implement a browser-based interactive voice dialogue system.

### 1.2 Key Features

- Real-time voice input and recognition
- Real-time two-way communication with Azure OpenAI
- Real-time voice output
- Customizable system messages
- Adjustable response temperature
- Configuration management via environment variables


## 2. Technical Specifications

### 2.1 Development Environment

- Node.js
- TypeScript
- Vite development server

### 2.2 Key Dependencies

- rt-client: Azure OpenAI real-time audio SDK
- @azure/identity: Azure authentication library
- AudioWorklet API: Low-latency audio processing

### 2.3 Audio Processing Specifications

- Sample rate: 24000Hz
- Input processing: Web Audio API
- Output processing: AudioWorklet
- Speech recognition: Whisper-1 model
- VAD (Voice Activity Detection): Server-side implementation


## 3. System Architecture

### 3.1 Core Components

1. Main Application (`main.ts`)
   - UI controls
   - Session management
   - Message processing
   - Audio stream control
   - Configuration loading from environment variables

2. Voice Recording System (`recorder.ts`)
   - Microphone input processing
   - Audio buffer management
   - AudioWorklet processing

3. Voice Playback System (`player.ts`)
   - Audio output control
   - Buffer playback management
   - Real-time speech synthesis

### 3.2 Communication Protocol

- WebSocket-based two-way communication
- Base64 encoding of binary audio data
- JSON-based messaging


## 4. User Interface

### 4.1 Configuration Items

- Endpoint URL (Environment Variable: `VITE_AZURE_OPENAI_ENDPOINT`)
- API Key (Environment Variable: `VITE_AZURE_OPENAI_KEY`)
- Deployment/Model Selection (Environment Variable: `VITE_AZURE_OPENAI_DEPLOYMENT`)
- System Message (Environment Variable: `VITE_AZURE_OPENAI_SYSTEM_MESSAGE`)
- Temperature Parameter (Environment Variable: `VITE_AZURE_OPENAI_TEMPERATURE`)
- Voice Selection (Environment Variable: `VITE_AZURE_OPENAI_VOICE`)
- Azure OpenAI Usage Flag (Environment Variable: `VITE_USE_AZURE_OPENAI`)

### 4.2 Operational Functions

- Start/Stop recording
- Clear text display
- Switch between Azure/OpenAI


## 5. Known Limitations

1. Graceful handling of connection errors is not yet implemented.
2. Voice selection functionality is implemented.
3. Keyless authentication using Entra is planned for a future update.


## 6. Setup and Execution

### 6.1 Prerequisites

1. Node.js installation
2. Environment capable of running a localhost web server

### 6.2 Execution Procedure

1. Install dependencies: `npm install`
2. Configure the `.env` file
3. Start the development server: `npm run dev`
4. Access via browser: `http://localhost:5173/`

### 6.3 Environment Variable Configuration

1. Create a `.env` file in the project root.
2. Set the following environment variables:

   ```
   VITE_AZURE_OPENAI_ENDPOINT=https://your-resource-name.openai.azure.com/
   VITE_AZURE_OPENAI_KEY=your-api-key
   VITE_AZURE_OPENAI_DEPLOYMENT=your-deployment-name
   VITE_AZURE_OPENAI_SYSTEM_MESSAGE="Instructions for the AI assistant"
   VITE_AZURE_OPENAI_TEMPERATURE=0.8
   VITE_AZURE_OPENAI_VOICE=en-US-JennyMultilingualNeural
   VITE_USE_AZURE_OPENAI=true
   ```

### 6.4 Operational Procedure

1. Verify that environment variables are correctly set.
2. Configuration values are automatically loaded into the form fields.
3. Adjust configuration values as needed.
4. Start the session with the "Record" button.


## License

MIT License
