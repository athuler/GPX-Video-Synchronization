# GPX/Video Synchronization

A simple web tool to synchronize a video file with a GPX track and export a retimed GPX. Everything runs locally in your browser — your files are never uploaded (only the CARTO/OpenStreetMap background tiles are fetched from the internet).

## Usage

Open `index.html` in a browser (directly, or via any static server such as `python3 -m http.server`).

1. **Select a video** and a **GPX file** (click or drag-and-drop).
2. Play or scrub the video — the red dot follows the corresponding position on the map.
3. Adjust the **GPX time offset** (slider, number field, or nudge buttons from ±0.1s to ±60s) until the dot matches what the video shows. Positive offset = the video starts later in the GPX recording. The coverage bar shows how the video span overlaps the GPX track.
4. Click **Export GPX** to download a retimed copy, trimmed to exactly the video's time span (interpolated points are added at the exact start/end boundaries). Elevation, heart rate, and other extensions are preserved.

### Export timestamp anchoring

Choose how the exported timestamps are anchored:

- **Shifted GPX times** (default) — keeps the GPX's own clock; the first exported point gets the time of the GPX position aligned with the video start.
- **Video file time** — anchors the first exported point to the video's recording start time (prefilled from the file's modification time, editable).
- **Epoch zero** — first exported point at `1970-01-01T00:00:00Z`, for a purely relative timeline.

### Advanced settings

- **GPX speed multiplier** — for timelapse videos: how many GPX seconds pass per video second (e.g. `8` for an 8× timelapse). The map dot honors it, and the export compresses timestamps by this factor.
- **Negate longitude** — fixes the Insta360 Studio bug that drops the minus sign from longitudes (the route appears mirrored east–west). Applies to both the map preview and the exported file.

## Requirements

- The GPX file must have `<time>` elements on its track points.
- Any modern browser; no installation or build step.
