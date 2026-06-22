# REV Mix AI — Product & Engineering Plan

> Tagline: Your music. Mixed by AI.

---

## Table of Contents

1. [Product Vision](#1-product-vision)
2. [Main Features](#2-main-features)
3. [Recommended Tech Stack](#3-recommended-tech-stack)
4. [Streaming Architecture](#4-streaming-architecture)
5. [AI DJ Mode](#5-ai-dj-mode)
6. [Local AI Radio](#6-local-ai-radio)
7. [High-Performance Design](#7-high-performance-design)
8. [Kafka Events](#8-kafka-events)
9. [Microservices](#9-microservices)
10. [Database Tables](#10-database-tables)
11. [Web App Screens](#11-web-app-screens)
12. [Mobile App Screens](#12-mobile-app-screens)
13. [DevOps Plan](#13-devops-plan)
14. [MVP Timeline](#14-mvp-timeline)
15. [Best MVP Scope](#15-best-mvp-scope)

---

## 1. Product Vision

Build a high-quality and high-performance music app for web, Android, and iOS. The app should allow users to stream music, create playlists, generate AI-based mixes, and use a local AI radio feature.

**Main goals**
- High-quality music streaming
- Fast performance on web and mobile
- AI DJ playlist and mix generation
- Local AI radio
- Offline playback for mobile
- Same account across web, Android, and iOS

---

## 2. Main Features

### MVP Features
- User login with Google, GitHub, or email
- Home page with recommendations
- Music player with play, pause, seek, queue, and repeat
- Playlist creation
- Search songs, artists, and albums
- High-quality streaming
- AI playlist generator
- AI DJ mode
- Favorites and recently played
- Admin upload panel

### Advanced Features
- Offline downloads for mobile
- Crossfade between songs
- Beat matching and BPM-based mixing
- Mood-based radio
- Local AI radio
- Lyrics view
- Voice command support
- Share playlist links
- Creator or artist dashboard
- Subscription plans

---

## 3. Recommended Tech Stack

### Web App
- Next.js
- React
- TypeScript
- Tailwind CSS

### Mobile App
- React Native with Expo
- Android support
- iOS support
- Native audio playback support

### Backend
- Node.js with NestJS or Express
- PostgreSQL for user and music data
- Redis for cache and sessions
- Kafka for events
- S3, MinIO, or Cloudflare R2 for music file storage
- FFmpeg for audio processing
- Ollama, vLLM, or OpenRouter for AI features

---

## 4. Streaming Architecture

Use HLS streaming for smooth playback and adaptive quality.

### Audio Quality Levels

| Level | Codec | Bitrate |
|-------|-------|---------|
| Low | AAC | 96 kbps |
| Normal | AAC | 160 kbps |
| High | AAC | 256 kbps |
| Premium | AAC / FLAC | 320 kbps or lossless |

### Streaming Flow

1. User uploads or imports a track.
2. Backend stores the original file.
3. FFmpeg converts the file into multiple quality levels.
4. HLS playlist files are generated.
5. Audio files are stored in object storage.
6. CDN delivers the files to users.
7. App selects the best quality based on network and device.

---

## 5. AI DJ Mode

### User Examples
- Create a 45-minute gym mix.
- Mix Telugu and Hindi party songs.
- Create relaxing night drive music.
- Play local radio for Austin with upbeat songs.

### AI DJ Should Consider
- Mood
- Genre
- Language
- BPM
- Energy level
- Song key
- User listening history
- Requested duration

### AI DJ Output
- Playlist order
- Smooth transition suggestions
- Crossfade timing
- Intro and outro notes
- Optional AI voice DJ announcements

---

## 6. Local AI Radio

Local AI Radio should allow users to create live-style music stations.

### Flow
1. User selects location, mood, genre, or language.
2. AI generates a radio queue.
3. App plays songs continuously.
4. AI can insert short voice segments.
5. User can skip, like, dislike, or regenerate.

### Example Stations
- Austin Night Drive Radio
- Telugu Party Mix Dallas
- Focus Coding Beats
- PhD Study Radio
- Weekend Gym Radio

---

## 7. High-Performance Design

### Web Performance
- Use server-side rendering where useful.
- Use CDN for album images and audio files.
- Lazy-load heavy player components.
- Cache metadata in Redis.
- Use signed URLs for secure streaming.

### Mobile Performance
- Use native audio playback.
- Preload the next track.
- Cache album art locally.
- Support background playback.
- Support lock-screen controls.
- Add offline download manager.

### Backend Performance
- Use Kafka for music events.
- Use Redis for trending songs and user cache.
- Use PostgreSQL for permanent data.
- Use object storage for music files.

---

## 8. Kafka Events

| Event | Description |
|-------|-------------|
| song.played | A song started playing |
| song.liked | A user liked a song |
| song.skipped | A song was skipped |
| playlist.created | A new playlist was created |
| ai.mix.generated | An AI mix was generated |
| radio.session.started | A radio session began |
| download.completed | An offline download finished |

---

## 9. Microservices

| Service | Responsibility |
|---------|----------------|
| auth-service | Login, JWT, OAuth |
| music-catalog-service | Songs, albums, artists |
| streaming-service | Signed URLs and HLS access |
| playlist-service | Playlists and queues |
| ai-dj-service | AI mix generation |
| radio-service | Local AI radio |
| recommendation-service | Personalized suggestions |
| upload-transcode-service | FFmpeg processing |
| billing-service | Subscriptions |
| notification-service | Push and email alerts |

---

## 10. Database Tables

### Core Tables
- users
- artists
- albums
- songs
- song_files
- playlists
- playlist_songs
- listening_history
- likes
- downloads
- ai_mix_sessions
- radio_sessions
- subscriptions

### Important songs Fields

| Field | Description |
|-------|-------------|
| title | Track title |
| artist | Artist name or ref |
| album | Album name or ref |
| duration | Length in seconds |
| genre | Genre |
| language | Language |
| bpm | Beats per minute |
| song_key | Musical key |
| mood | Mood tag |
| energy_score | Energy level |
| file_url | Original file URL |
| hls_master_url | HLS master playlist URL |
| cover_image_url | Cover art URL |

---

## 11. Web App Screens

- Landing page
- Dashboard
- Music player
- Search
- Playlist builder
- AI DJ page
- Local Radio page
- Upload and admin page
- Subscription page

---

## 12. Mobile App Screens

- Login
- Home
- Search
- Library
- Now Playing
- Playlist Detail
- AI DJ Generator
- Local Radio
- Downloads
- Profile
- Subscription

---

## 13. DevOps Plan

Use the REV-APPS deployment style:

- Docker for all services
- Helm charts for Kubernetes
- K3s local deployment
- Jenkins CI/CD
- Cloudflare Tunnel for dev access
- PostgreSQL
- Redis
- Kafka
- Object storage
- Monitoring with Prometheus and Grafana
- Logging with Loki or ELK

### Environments

dev -> test -> stage -> prod

---

## 14. MVP Timeline

### Phase 1 - Foundation
- Set up monorepo
- Create web app shell
- Create mobile app shell
- Create auth service
- Create PostgreSQL schema
- Create music catalog API

### Phase 2 - Music Player
- Upload songs
- Generate HLS files
- Build web player
- Build mobile player
- Add playlist support
- Add search

### Phase 3 - AI DJ
- Add AI prompt engine
- Generate playlists by mood and duration
- Add BPM and genre-based ordering
- Add crossfade logic
- Save generated mixes

### Phase 4 - Local AI Radio
- Create radio session API
- Add location, mood, and genre selector
- Generate continuous queue
- Add AI voice intro and outro

### Phase 5 - Production
- Add subscriptions
- Add CDN
- Add offline downloads
- Add monitoring
- Prepare App Store and Play Store deployment

---

## 15. Best MVP Scope

The first version should include:

- Login
- Upload or import music
- Stream songs
- Create playlists
- AI DJ playlist generator
- Web app
- Android app
- iOS app
- Basic radio mode
- Admin panel

Avoid building too many features in the first version. First focus on playback quality, fast performance, and a strong AI mix experience.
