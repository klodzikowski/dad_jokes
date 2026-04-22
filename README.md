# Dad Jokes

Tell it about your day. It finds a dad joke in it.

A single static HTML page hosted on GitHub Pages. Bring your own OpenAI API key — it lives in your browser session only, never stored on a server, never billed to anyone but you.

## Try it

[klodzikowski.github.io/dad_jokes](https://klodzikowski.github.io/dad_jokes/)

## How it's built

Forked from my [LLM assistant template](https://github.com/klodzikowski/lmt-chatbot), then stripped down to just the essentials: no admin drawer, no model picker, no sampling sliders. One system prompt, one job.

Under the hood:

- `gpt-4o-mini` via the OpenAI Chat Completions API, streamed token-by-token
- Dry British dad in the system prompt
- Pastel "heeler" palette, cartoonish title, a confetti burst for every reply
- Your API key stays in `sessionStorage` (tab-lifetime only, never committed, never synced)
