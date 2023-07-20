[![Rebol-Spotify CI](https://github.com/Oldes/Rebol-Spotify/actions/workflows/main.yml/badge.svg)](https://github.com/Oldes/Rebol-Spotify/actions/workflows/main.yml)

# Rebol/Spotify

A Spotify API module for [Rebol3](https://github.com/Oldes/Rebol3).

## Getting started
To start using the API under your own name, follow these steps:

1. Log into the [dashboard](https://developer.spotify.com/dashboard) using your Spotify account.
2. Create an app. Once you have created your app, you will have access to the app credentials (`client-id` and `client-secret`). These will be required for API authorization to obtain an access token. Include `http://localhost:8989/spotify-callback/` as one of the Redirect URIs!

To avoid going thru the authentication process between Rebol sessions, it is recomanded to use a built in persistent data storage:
1. Create a new Rebol user: `set-user/n Daniel` (you will be asked for an encryption password).
2. Authorize using the Spotify credentials:
```rebol
spotify: import spotify
spotify/authorize [
  client-id:     {XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX}
  client-secret: {YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY}
  scopes: [
  ;@@ In real app not all scopes may be required!
  ;@@ https://developer.spotify.com/documentation/general/guides/scopes/
    ;- Images                     
    @ugc-image-upload             ; Write access to user-provided images.
    ;- Spotify Connect            
    @user-read-playback-state     ; Read access to a user’s player state.
    @user-modify-playback-state   ; Write access to a user’s playback state
    @user-read-currently-playing  ; Read access to a user’s currently playing content.
    ;- Playback                   
    @streaming                    ; Control playback of a Spotify track. (Web Playback SDK and Premium only)
    @app-remote-control           ; Remote control playback of Spotify. (iOS and Android SDK only)
    ;- Users                      
    @user-read-email              ; Read access to user’s email address.
    @user-read-private            ; Read access to user’s subscription details (type of user account).
    ;- Playlists                  
    @playlist-read-collaborative  ; Include collaborative playlists when requesting a user's playlists.
    @playlist-modify-public       ; Write access to a user's public playlists.
    @playlist-read-private        ; Read access to user's private playlists.
    @playlist-modify-private      ; Write access to a user's private playlists.
    ;- Library                    
    @user-library-modify          ; Write/delete access to a user's "Your Music" library.
    @user-library-read            ; Read access to a user's "Your Music" library.
    ;- Listening History          
    @user-top-read                ; Read access to a user's top artists and tracks.
    @user-read-playback-position  ; Read access to a user’s playback position in a content.
    @user-read-recently-played    ; Read access to a user’s recently played tracks.
    ;- Follow                     
    @user-follow-read             ; Read access to the list of artists and other users that the user follows.
    @user-follow-modify           ; Write/delete access to the list of artists and other users that the user follows.
  ]
]
```
Running this code from Rebol, a default browser should display an authorization Spotify dialog, where you must agree the access as a part of the OAuth2 process.
Once authorized, the received access token is stored in the persistent user's data for later use. When needed, it is refreshed authomatically.

## Usage:

```rebol
set-user Daniel                ;; Rebol user with the Spotify credentials
spotify: import %spotify.reb   ;; Imports the Spotify module

;; Get detailed profile information about the current user (including the current user's username).
probe spotify/GET %me
```

For more usage examples see the [test file](spotify-test.r3).
