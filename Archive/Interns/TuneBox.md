Walkthrough37 minutes ago

Review

# TuneBox Project Walkthrough

This document provides a deep dive into the **TuneBox** project, a web-based music player application. It covers the high-level architecture, technology stack, and low-level implementation details.

## High-Level Overview

**TuneBox** is a client-side Single/Multi-Page Application (HTML/JS) that serves as a personal music library and player. It operates entirely in the browser without a backend server, utilizing **IndexedDB** for persistent storage of audio files and metadata.

### Core Features

- **Library Management**: Upload and store audio files directly in the browser.
- **Playlist System**: Create, organize, and manage custom playlists.
- **Audio Playback**: Full-featured player with seek, volume control, and track navigation.
- **Persistence**: Data is saved across sessions using IndexedDB.

### Technology Stack

- **Frontend**: HTML5, CSS3, JavaScript (Vanilla).
- **Storage**: IndexedDB (for large binary audio data and structured data), SessionStorage (for state passing between pages).
- **External Libraries**:
    - [FontAwesome](https://fontawesome.com/) (Icons)
    - [SweetAlert2](https://sweetalert2.github.io/) (Modals and Alerts)

---

## File Structure & Architecture

The project is structured as a static website with distinct pages for the library view and the player interface.

TuneBox/

├── assets/          # Static assets (images, logos)

├── css/             # Stylesheets

│   ├── home.css     # Styles for the library/home page

│   ├── player.css   # Styles for the player interface

│   ├── modal.css    # Styles for popup modals

│   └── ...

├── js/              # Application Logic

│   ├── home.js      # Logic for the library view (playlists, uploads)

│   └── player.js    # Logic for the audio player and playback controls

├── index.html       # Entry point (Library/Home view)

└── player.html      # Player interface view

### Data Flow

1. **User Upload**: User selects audio files via `audioUpload` input.
2. **Processing**: Files are converted to `ArrayBuffer/Blob`.
3. **Storage**: Audio blobs and metadata are stored in **IndexedDB** (`MusicDB`).
4. **Navigation**: When a user selects a song or playlist:
    - Metadata is saved to `sessionStorage` (`currentSong`, `currentPlaylist`).
    - Browser navigates to 
        
        player.html.
5. **Playback**: 
    
    player.html reads IDs from `sessionStorage`, fetches Blobs from **IndexedDB**, creates object URLs, and plays audio.

---

## Low-Level Implementation Details

### 1. Storage Layer (IndexedDB)

The application uses two distinct IndexedDB databases:

#### **MusicDB** (Store: `songs`)

Stores the actual audio data and song metadata.

- **Key**: `id` (Timestamp based)
- **Schema**:
    
    json
    
    {
    
        "id": 1700000000,
    
        "title": "Song Name",
    
        "audioBlob": [ArrayBuffer],
    
        "duration": 240,
    
        "dateAdded": "2024-..."
    
    }
    

#### **TuneBoxPlaylists** (Store: `playlists`)

Stores playlist definitions.

- **Key**: `id`
- **Schema**:
    
    json
    
    {
    
        "id": 1700000000,
    
        "name": "My Favorites",
    
        "description": "...",
    
        "songs": [array_of_song_ids],
    
        "coverImage": "assets/..."
    
    }
    

### 2. Application Logic

#### **Home Logic (

js/home.js)**

- **Initialization**: Opens DB connections and renders lists.
- **Song Upload**: Reads file input, converts to Blob, saves to `MusicDB`.
- **Playlist Management**: Handles creation and deletion of playlists.
- **Navigation**:
    - On song click: Sets `currentSong` and `currentPlaylist` (virtual "All Songs" playlist) in `sessionStorage` and redirects.
    - On playlist click: Sets `currentPlaylist` in `sessionStorage` and redirects.

#### **Player Logic (

js/player.js)**

- **State Hydration**: Reads `currentPlaylist` from `sessionStorage`.
- **Blob Retrieval**: Fetches song data from `MusicDB` based on IDs in the playlist.
- **Audio Context**: Uses `URL.createObjectURL(blob)` to generate a playable URL for the `<audio>` element.
- **Playback Control**: Manages `Audio` events (
    
    timeupdate, 
    
    ended, 
    
    play, 
    
    pause) to update UI (progress bar, icons).
- **Queue Management**: Auto-plays next song on 
    
    ended event.
- **Cleanup**: Revokes object URLs when switching songs to prevent memory leaks (partially implemented).

### 3. Key Findings & Issues

- **Missing File**: 
    
    player.html references `js/playlist-utils.js`, but this file does not exist in the directory. This looks like a leftover reference or missing code, though 
    
    player.js seems to handle playlist updates independently.
- **Memory Management**: The app uses `URL.createObjectURL`. While necessary for blob playback, heavy usage without aggressive revocation can lead to high memory usage in long sessions.

## walkthrough.md

This artifact documents the analysis of the TuneBox codebase.