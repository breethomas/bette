---
name: analyze-video
description: Analyze video content (YouTube, local files). Use when user says "analyze this video", "watch this video", "process this video", "video analysis", "what's in this video", or pastes a YouTube/video URL with a request to analyze. Downloads via yt-dlp, transcribes via Memorex, and synthesizes key themes and insights. Requires Memorex + yt-dlp installation.
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."


# Analyze Video

Download and analyze video content. Generates transcript + keyframes via Memorex, then synthesizes themes, insights, and action items.

## Prerequisites

This skill requires:
- **Memorex** (Go binary for transcription + keyframes)
- **yt-dlp** (video downloader)
- **whisper.cpp model** at `~/.cache/whisper/ggml-base.bin`

If any are missing, report which prerequisite is not installed and stop.

## Argument

`$ARGUMENTS` = YouTube URL, video URL, or local file path. May include analysis instructions (e.g., "focus on product strategy").

## Paths

- **Memorex:** `~/go/bin/memorex` (or wherever installed)
- **yt-dlp:** available on PATH or `/opt/homebrew/bin/yt-dlp`
- **Video cache:** `{Home Directory}/videos/.cache/`
- **Memorex output:** `{Home Directory}/videos/`
- **Synthesis output:** `{Home Directory}/drafts/`

## Workflow

### 1. Parse input

Extract from `$ARGUMENTS`:
- **Source:** URL or local file path
- **Analysis focus:** Any specific instructions. Default: general synthesis.

### 2. Check duration (if URL)

```bash
yt-dlp --print title --print duration_string "$URL" 2>&1
```

- **Under 30 minutes:** Proceed automatically.
- **30-60 minutes:** Warn {PM Name}. Ask if they want to proceed, run in background, or skip.
- **Over 60 minutes:** Recommend running in background or skipping.

### 3. Download video (if URL)

```bash
yt-dlp -f "bestvideo[height<=720]+bestaudio/best[height<=720]" \
  --merge-output-format mp4 \
  -o "{Home Directory}/videos/.cache/%(title)s.%(ext)s" \
  "$URL" 2>&1
```

### 4. Run Memorex

```bash
~/go/bin/memorex -o "{Home Directory}/videos/[slug]_memorex.md" "[video_file_path]"
```

This may take a few minutes. Use a generous timeout (10 minutes).

### 5. Read Memorex output

Read the generated `_memorex.md` file.

### 6. Synthesize

Adapt depth to content type:

**For product/strategy videos:**
- Key arguments and frameworks presented
- Contrarian or surprising points
- Relevance to current work (reference the strategic framework if applicable)
- Quotable lines worth saving

**For customer recordings / demos:**
- Customer pain points and requests
- Feature gaps or opportunities
- Sentiment and urgency signals

**For team demos / internal recordings:**
- What was demonstrated
- Technical decisions or trade-offs
- Follow-up items

**Always include:** Source, duration, one-paragraph summary, timestamped references.

### 7. Write to file

Write to: `{Home Directory}/drafts/video-analysis-YYYY-MM-DD-[slug].md`

```
# Video Analysis — [Title]

**Source:** [URL or file path]
**Date analyzed:** [today]
**Duration:** [from memorex output]

## Summary
[One paragraph]

## Key Themes
### [Theme 1]
[Details with timestamps]

## Notable Quotes / Moments
- [timestamp] — "[quote or description]"

## Relevance to Current Work
[How this connects to current strategy, if applicable. Skip if not relevant.]

## Raw Transcript
See: {Home Directory}/videos/[slug]_memorex.md
```

### 8. Return file path

Your final message MUST include:
```
VIDEO_FILE: {Home Directory}/drafts/video-analysis-YYYY-MM-DD-[slug].md
```

## Guardrails

- **No fabrication.** Only include content actually in the video transcript.
- **Conservative on quotes.** Whisper transcription isn't perfect — flag any quote that seems off with "(approximate)".
- **Concise first draft.** {PM Name} will ask to expand sections if needed.
- **Clean up on failure.** If yt-dlp or memorex fails, report the error clearly. Don't leave partial files.
