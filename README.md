i don't like compaction. why isn't something like this proof-of-concept the default?

```bash
uv venv anti-c --python 3.13
source anti-c/bin/activate
uv pip install --python anti-c/bin/python -r requirements.txt
```

Export `ANTHROPIC_API_KEY` in your shell (for example, in `~/.zshrc`), then run:

```bash
python app.py
```

<img width="1156" height="550" alt="image" src="https://github.com/user-attachments/assets/68e53431-bf96-484c-87f4-e25f75080441" />

1000 token "context window" for this demo. saves verbatim user/assistance messages at 25%, 50%, 75% and 95%. Summarizes at 100%. Stores turns and summaries in txt files.
