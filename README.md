# Anti-compaction

A small Python terminal chat with Claude Haiku, transcript checkpoints, and summary compaction.

## Setup

Tested with Python 3.13 on macOS. The interface uses Python's built-in `curses` module.

```bash
uv venv anti-c --python 3.13
uv pip install --python anti-c/bin/python -r requirements.txt
```

Export `ANTHROPIC_API_KEY` in your shell (for example, in `~/.zshrc`), then run:

```bash
anti-c/bin/python app.py
```

The app reads the key from `os.environ`. Chat, token counting, and summarization use the Anthropic API.

## Using the chat

- Enter sends a message.
- Backspace edits the draft; Ctrl-U clears it.
- `/quit`, Ctrl-C, or Ctrl-D exits.
- Your messages are blue. Haiku's replies use black text on a light-grey background.

## Checkpoints and compaction

`CONTEXT_LIMIT` in `app.py` is currently **1,000 tokens** for testing. Change it to `10_000` for a larger window.

After each reply, the app counts the active conversation tokens. At 25%, 50%, 75%, and 95%, it updates one `turns/<session>.txt` file with all original user and assistant messages. One reply can cross several checkpoints.

At or above the limit, the app refreshes the transcript, asks Haiku to summarize it, and writes the latest summary to `summaries/<session>.txt`. It replaces the active model context with that summary and resets the checkpoints. The summary's tokens count toward the next window.

The limit is checked after complete replies, so usage can exceed it. Each compaction summarizes the full saved session transcript; this input grows as the session continues. If compaction fails, the active conversation is retained.

Each launch starts a new session. Transcripts are saved at checkpoints and before compaction; exiting does not save messages since the last checkpoint. The app does not resume saved sessions. Generated transcripts, summaries, and the virtual environment are ignored by Git.
