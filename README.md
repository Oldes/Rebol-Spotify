[![Rebol-Spotify CI](https://github.com/Oldes/Rebol-Spotify/actions/workflows/main.yml/badge.svg)](https://github.com/Oldes/Rebol-Spotify/actions/workflows/main.yml)

# Rebol/Spotify

A Spotify API module for [Rebol3](https://github.com/Oldes/Rebol3).

## Usage:

```rebol
spotify: import %spotify.reb

;; Get detailed profile information about the current user (including the current user's username).
probe spotify/GET %me
```

For more usage examples see the [test file](spotify-test.r3).
