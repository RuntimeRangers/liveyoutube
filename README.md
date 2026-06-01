YouTube Live Profile Card

A lightweight "Link-in-bio" style web app that automatically detects when your YouTube channel goes live, dynamically updating the UI (red neon effect, pulsing "On Air" icon) and the destination link.

Designed with a robust backend architecture to minimize Google API quota consumption and handle high traffic spikes (e.g., mass clicks from Instagram) without instability.

Key Features

Smart Deep Linking: If a user clicks from a mobile device during a live stream, the script bypasses in-app browsers (like Instagram or TikTok's WebViews) and opens the video directly in the native YouTube App using URI Schemes (iOS/Android).
Strategic Caching (Anti-Quota Ban):** Direct calls to the YouTube API are strictly limited to once every 15 minutes. All visitors in the meantime are served from a lightning-fast local cache.
Safe Concurrency: Implements atomic File Locking (`LOCK_EX`) in PHP. Even with thousands of simultaneous clicks, the cache file will never corrupt.
Security by Design: Includes `.htaccess` directives to block direct public access to sensitive configuration files and backend cache logic.

Requirements

To run this project on your server, you need:
* A web server (Apache/Nginx) supporting **PHP 7.4 or higher**.
* The `cURL` extension enabled in PHP.
* A **YouTube Data API v3 Key** (obtainable for free via the Google Cloud Console).
* Your YouTube **Channel ID**.

Installation and Configuration

Follow these steps carefully to prevent security issues or data corruption.

1. API Configuration
Open the `config.php` file and insert your credentials:

<?php
return [
    'youtube_api_key' => 'YOUR_API_KEY_HERE',
    'channel_id'      => 'YOUR_CHANNEL_ID_HERE'
];
?>
