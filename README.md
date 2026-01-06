# Voxa

**AI-powered voice receptionist that handles business calls using local LLM inference.**

Built a full-stack voice AI system that answers phone calls, understands customer questions, and responds naturally - all without sending data to external AI APIs. Designed to help small businesses automate their front desk.

---

## The Problem

Small businesses miss calls, lose customers, and can't afford 24/7 reception staff. Existing solutions are expensive, sound robotic, or require sending customer data to third-party AI services.

## The Solution

Voxa is a privacy-first AI receptionist that runs inference locally:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│   Incoming Call                                                         │
│        │                                                                │
│        ▼                                                                │
│   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                │
│   │   Twilio    │───►│   Speech    │───►│   Ollama    │                │
│   │   Voice     │    │   to Text   │    │  (Mistral)  │                │
│   └─────────────┘    └─────────────┘    └─────────────┘                │
│                                               │                         │
│                                               ▼                         │
│   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                │
│   │   Caller    │◄───│   Text to   │◄───│   Context   │                │
│   │   Hears     │    │   Speech    │    │  Injection  │                │
│   └─────────────┘    └─────────────┘    └─────────────┘                │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Technical Highlights

### Voice Pipeline
End-to-end voice processing:
1. **Twilio** receives incoming calls and handles telephony
2. **Transcription** converts caller speech to text
3. **LLM** processes the query with business context
4. **TTS** converts the AI response back to speech
5. **Caller** hears a natural response

### Local LLM Inference
- Uses **Ollama** with **Mistral 7B** for on-device inference
- No API costs after setup
- Customer conversations never leave your infrastructure
- Sub-second response times

### Context-Aware Responses
Business knowledge is injected into every prompt:
```json
{
  "business_name": "Mascara Beauty Salon",
  "services": [
    { "name": "Haircut", "price": "$45" },
    { "name": "Facial", "price": "$65" }
  ],
  "hours": "Mon-Sat 9am-7pm"
}
```

The AI understands your business and responds accurately to questions about services, pricing, and hours.

---

## Tech Stack

| Layer | Technologies |
|-------|-------------|
| **Frontend** | React Native, TypeScript |
| **Backend** | Express.js, TypeScript |
| **Voice** | Twilio (calls, transcription, TTS) |
| **AI** | Ollama, Mistral 7B |
| **Mobile** | iOS, Android |

---

## API Endpoints

| Endpoint | Description |
|----------|-------------|
| `POST /ask` | Text-based query (for testing) |
| `POST /voice` | Twilio webhook for incoming calls |
| `POST /handle-recording` | Processes voice recordings |
| `POST /handle-transcription` | Handles Twilio transcriptions |

---

## Running Locally

```bash
git clone https://github.com/druvsarin1/Voxa.git
cd Voxa

# Install Ollama and pull Mistral
brew install ollama
ollama pull mistral

# Backend
cd backend
npm install
npm run dev  # Runs on port 3000

# Frontend (separate terminal)
cd ..
npm install
npm run ios  # or npm run android
```

### Configure Twilio
1. Create a Twilio account
2. Get a phone number
3. Set webhook URL to your backend `/voice` endpoint

---

## Skills Demonstrated

- **Voice AI** - Full speech-to-speech pipeline
- **Local LLM** - Privacy-preserving inference with Ollama
- **Telephony Integration** - Twilio webhooks and voice APIs
- **Full-Stack TypeScript** - Type-safe frontend and backend
- **Cross-Platform Mobile** - React Native for iOS/Android

---

## Contact

**Dhruv Sarin** - [LinkedIn](https://linkedin.com/in/dhruvsarin) | [GitHub](https://github.com/druvsarin1)
