# YouTube Playlist Player

A lightweight YouTube playlist player with two versions:

- Main — full playlist management using JSON files and browser saves.
- Straight — a simplified, self-contained version with built-in playlists,
  designed for devices where file management isn't practical.

## Quick Start

The easiest way to use the project is through GitHub Pages:

[Project Page]

Open the page, choose the version you want, and use it.

## Straight

Straight is the simple version.

Its playlists are built directly into the page, so it does not require:

- JSON files
- file pickers
- a local server
- Python
- Node
- filesystem access

This makes it suitable for devices such as VR browsers and managed
computers where normal file management isn't available.

The playlist that starts first can be configured in the source with:

const FirstPlaylistToPlay = "Tasklike";

## Main

Main is the customizable version.

It supports:

- importing playlist JSON
- named playlist saves
- exporting playlists
- queue management
- shuffle
- looping
- playback controls
- YouTube embeds

Main is intended for users who want to manage their own playlists.

## GitHub Pages

The project is designed to work as a static site and can be hosted
through GitHub Pages.

No local server is required when using the deployed version.

## Requirements

A modern web browser with JavaScript and YouTube access.

The YouTube embed player must be allowed to load.

## What it does

- Plays YouTube videos through YouTube's embed player.
- Does not download YouTube videos.
- Does not host the video files.
- Uses YouTube for video playback and thumbnails.

## Project Structure

├── Icons/
│   ├── BlueIcon.svg
│   ├── GreenIcon.svg
│   └── RedIcon.svg
├── Master/
│   ├── Main.html
│   └── Straight.html
├── LICENSE
├── README.md
└── index.html

## Usage Structure
You may copy, use, edit, change, modify, and republish this project in any way you want.

The main goal of this project is to give you something you can personalize however you like. Change the design, add features, remove features, or make it work the way you want.

# First uploaded to Github on September 10th, 2026.
