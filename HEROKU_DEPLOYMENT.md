# Heroku Deployment Guide

This repository includes Docker support and Heroku-specific configurations for easy deployment.

## Quick Deploy to Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Manual Heroku Deployment

### Prerequisites
- Heroku CLI installed
- Docker installed (for container deployment)
- Git configured

### Deployment Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/Anggahrm/Apiytdlp.git
   cd Apiytdlp
   ```

2. **Login to Heroku**
   ```bash
   heroku login
   heroku container:login
   ```

3. **Create a Heroku app**
   ```bash
   heroku create your-app-name
   ```

4. **Set environment variables** (optional, for Spotify features)
   ```bash
   heroku config:set SPOTIFY_CLIENT_ID=your_client_id
   heroku config:set SPOTIFY_CLIENT_SECRET=your_client_secret
   ```

5. **Deploy using Docker**
   ```bash
   heroku container:push web
   heroku container:release web
   ```

6. **Open your app**
   ```bash
   heroku open
   ```

## Local Development with Docker

### Build and run locally
```bash
docker build -t apiytdlp .
docker run -p 8000:8000 apiytdlp
```

### Or use Docker Compose
```bash
docker-compose up --build
```

Access the application at http://localhost:8000

## Configuration

### Environment Variables
- `PORT`: Port number (set automatically by Heroku)
- `SPOTIFY_CLIENT_ID`: Spotify Developer Client ID (optional)
- `SPOTIFY_CLIENT_SECRET`: Spotify Developer Client Secret (optional)

### Buildpacks
The app uses two buildpacks:
1. FFmpeg buildpack for video/audio processing
2. Python buildpack for the FastAPI application

## Troubleshooting

### Common Issues
1. **Build failures**: Ensure all dependencies in requirements.txt are valid
2. **FFmpeg not found**: The FFmpeg buildpack should handle this automatically
3. **Port binding issues**: Heroku automatically sets the PORT environment variable

### Logs
View application logs:
```bash
heroku logs --tail -a your-app-name
```

## Features Available on Heroku
- YouTube video/audio downloading
- Spotify playlist downloading (requires API keys)
- RESTful API with automatic documentation at `/docs`
- Web interface accessible at the root URL

## Limitations on Heroku
- Ephemeral filesystem: Downloaded files are temporary
- Dyno sleep: Free tier apps sleep after 30 minutes of inactivity
- Request timeout: 30-second limit for HTTP requests