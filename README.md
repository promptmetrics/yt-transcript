# yt-transcript

A small bash wrapper around [yt-dlp](https://github.com/yt-dlp/yt-dlp) that turns a YouTube (or any yt-dlp-supported) URL into a clean, plain-text transcript. It fetches subtitles, strips the VTT formatting (timestamps, tags, duplicate cue lines), and prints readable prose your coding agent can work with.

Human-written subtitles are preferred; auto-generated captions are the fallback.

## Requirements

- `yt-dlp` on your PATH ([install instructions](https://github.com/yt-dlp/yt-dlp/wiki/Installation))
- `bash`, plus the standard `sed`, `awk`, and `find` (present on macOS and Linux)

## Install

```bash
curl -o ~/.local/bin/yt-transcript https://raw.githubusercontent.com/promptmetrics/yt-transcript/main/yt-transcript
chmod +x ~/.local/bin/yt-transcript
```

Make sure `~/.local/bin` is on your PATH.

## Usage

```
yt-transcript [-l LANG] [-t] [-o FILE] URL
```

Flags go before the URL. Quote the URL.

| Flag | Meaning |
| --- | --- |
| `-l LANG` | Subtitle language (default: `en`) |
| `-t` | Keep timestamps, one `[mm:ss] text` line per cue |
| `-o FILE` | Write to `FILE` instead of stdout |
| `-h` | Print usage |

## Examples

Print a transcript to the terminal:

```bash
yt-transcript "https://www.youtube.com/watch?v=VIDEO_ID"
```

Save it to a file:

```bash
yt-transcript -o talk.txt "https://www.youtube.com/watch?v=VIDEO_ID"
```

Keep timestamps:

```bash
yt-transcript -t "https://www.youtube.com/watch?v=VIDEO_ID"
```

German subtitles:

```bash
yt-transcript -l de "https://www.youtube.com/watch?v=VIDEO_ID"
```

## Notes and limitations

- **It depends on yt-dlp, which breaks when sites change.** If a fetch fails, update yt-dlp first (`yt-dlp -U`, or reinstall via pip). The maintainers point regular users at the nightly builds.
- **Respect terms of service.** Downloading content you don't own may violate a platform's terms. Your own recordings are fine; public transcripts and metadata for research are generally defensible; bulk-scraping is not.
- **Exit codes:** `1` if no subtitles exist for the requested language, `2` on a usage error.

## License

[MIT](LICENSE)

---

Built by [Izzy Aly](https://github.com/iiizzzyyy) at [PromptMetrics](https://github.com/promptmetrics).
