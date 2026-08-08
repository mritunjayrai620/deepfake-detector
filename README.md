# AI Deepfake & Voice-Clone Detector
a
Full-stck platform for detecting AI-generated (deepfake) audio and video, with a live browser
extension for real-time detection during video calls.

## Architecture

```
Client (React dashboard / Chrome extension)
        |
        v
FastAPI Gateway (auth, routing, rate limiting)
        |
   -----+-----
   |         |
Audio       Video
Service     Service
   |         |
CNN model  CNN model
(ASVspoof) (FaceForensics++)
        |
        v
   PostgreSQL (logs)
```

## Project structure

```
deepfake-detector/
  backend/
    gateway/          # FastAPI gateway - auth, routing, rate limiting
    audio_service/    # Audio deepfake detection microservice
    video_service/    # Video deepfake detection microservice
  frontend/            # React dashboard
  extension/           # Chrome extension (Manifest V3) for live call detection
  ml/
    audio/             # Audio model training scripts
    video/             # Video model training scripts
  docker-compose.yml
```

## Getting started

### 1. Backend services (local dev, without Docker)

```bash
cd backend/gateway
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

Repeat similarly for `audio_service` (port 8001) and `video_service` (port 8002).

### 2. With Docker Compose (recommended)

```bash
docker-compose up --build
```

This starts the gateway, both ML services, and PostgreSQL together.

### 3. Frontend

```bash
cd frontend
npm install
npm run dev
```

### 4. Train the models

See `ml/audio/train_audio_model.py` and `ml/video/train_video_model.py` for training
scripts. Download ASVspoof and FaceForensics++ datasets separately (see comments in
each script for dataset links) — they are not included in this repo.

## Roadmap

See `ROADMAP.md` for the full week-by-week execution plan.

## Status

🚧 Work in progress — scaffolded services, model training pipelines, and API contracts in place.
Model weights not yet trained/included.

## License

MIT
