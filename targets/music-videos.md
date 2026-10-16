# Target notes: music videos

- **Family:** music-video.
- **Aliases** (a target named any of these uses this file):
  - music-videos, music video;
  - hello tomorrow, hello-tomorrow;
  - frutiger aero realm, frutiger;
  - не робей, ne robei, ne-robei;
  - slop, called it slop, juno;
  - captcha, ghost.
- **Projects in order** (for the `followup` lens):

  | Video | Folder | Finished |
  |---|---|---|
  | Hello Tomorrow | `music-videos/videos/hello-tomorrow/` | 2026-10-10 |
  | Frutiger Aero Realm | `videos/frutiger-aero-realm/` | 2026-10-10 |
  | Не робей | `videos/ne-robei/` | 2026-10-11 |
  | Slop | `videos/slop/` | 2026-10-11 |
  | Captcha ("Ghost") | `videos/captcha/` | not finished |

  All are under `~/antigravity-projects/music-videos/`.

## Repos

- **Rules repo:** `~/antigravity-projects/music-videos`, a git repo on main. It holds the shared guide, templates, tools and catalog.
- **Each video** in `music-videos/videos/<slug>/` is **its own git repo**, with its own `CLAUDE.md`, `docs/`, `specs/` and `aesthetic.md`. Check both repos for commits.
- **Session logs:**
  - Most are in `~/.claude/projects/-Users-me-antigravity-projects/`.
  - Older log-reading notes: `music-videos/tools/search_logs.py` lists the Hello Tomorrow sessions (`790d04df`, `05a46a41`, `3aff49b8`).

## Rule files

- **Rules repo:** `music-videos/CLAUDE.md`, `README.md`, `guide/*.md`, `template/*.md`, `CATALOG.md`.
- **Each video:** `videos/<slug>/CLAUDE.md`. `videos/<slug>/docs/*.md` is history, not rules.
- **Claude Code** (live, guarded) under `~/antigravity-projects/.claude/`:
  - `skills/new-music-video/SKILL.md`, `skills/youtube-thumbnails/SKILL.md`;
  - `agents/asset-builder.md`, `agents/video-worker.md`;
  - `hooks/stills_check.py`.
- **`.claude/` sync:** after editing live files, run `python3 -I tools/sync_claude_config.py` from `music-videos/`. It copies them into `music-videos/claude-config/` and commits. Never edit the copies.
- **User memory:** `~/.claude/projects/-Users-me-antigravity-projects/memory/MEMORY.md` and the files it links. Many music-video rules live there, for example renders, opening results and asset specs.

## Quality domain

3D characters and assets (faces, bodies, hands and grips, hair), animation and motion (contact, penetration, timing, the camera), sets, lyrics on screen, sync to the song, and render quality and speed.

## Test command

`cd ~/antigravity-projects/music-videos && python3 -I -m unittest discover -s tools/tests`

## Forbidden actions for appliers

- **Renders of any kind:** `npm run render*`, `tools/render_final.py`, `tools/cloud_render.py`, `remotion render`.
- **Stills sheets** (`tools/stills_sheet.py`) and asset sheets: these run Chromium, which is slow and heavy.
- **Starting Remotion Studio**, `npm install`.
- **The web:** Suno, YouTube, BrowserOS or any browser, uploads.
- **Opening any window**, including `open` without `-g`.

## Evals

- `evals/slop-replay.md`: replay with `/retro slop --replay a9bcb34`.
