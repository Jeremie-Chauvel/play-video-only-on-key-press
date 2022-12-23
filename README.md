# Play video only on key press

The video `my_video.mp4` is played only when the spacebar is pressed and reset back to the start on key release.

## Installation

[Install nodejs](https://nodejs.org/en/download/) (version 18) and [install pnpm](https://pnpm.io/installation).

## Developing

Install dependencies with `pnpm install`, start a development server:

```bash
pnpm  dev
```

## Building

To create a production version of your app:

```bash
pnpm build
```

## Running the app

```bash
pnpm preview
```

Click the "start experiment button and then press the spacebar.

To change the video:

- update the video in `static/my_video.mp4` and rebuild the app and rerun preview
