# Dad Jokes

Tell it about your day. It finds a dad joke in it.

A single static HTML page hosted on GitHub Pages. Bring your own OpenAI API key — it lives in your browser session only, never stored on a server, never billed to anyone but you. Optional Supabase config keeps your chat history across reloads, with a sidebar drawer for switching between conversations.

## Try it

[klodzikowski.github.io/dad_jokes](https://klodzikowski.github.io/dad_jokes/)

## How it's built

Forked from my [LLM assistant template](https://github.com/klodzikowski/lmt-chatbot), then stripped down to just the essentials: no admin drawer, no model picker, no sampling sliders. One system prompt, one job — plus a chat drawer for past conversations.

Under the hood:

- `gpt-5.4-mini` via the OpenAI Chat Completions API, streamed token-by-token
- Dry British dad in the system prompt
- Pastel "heeler" palette, cartoonish title, a confetti burst for every reply
- OpenAI key in `sessionStorage` (tab-lifetime only, never committed, never synced)
- Supabase URL + anon key in `localStorage`, used to persist threads and messages

## Persistent chat history (optional)

Click the **Chats** chip top-left to open the drawer. New chats live there; click any to switch. Without Supabase configured, the app still works — chats just stay in this tab and vanish on close.

To enable persistence, run this SQL once in your Supabase project's SQL Editor (the same modal that asks for the OpenAI key shows it inline):

```sql
create table dad_jokes_threads (
  id          uuid primary key default gen_random_uuid(),
  user_id     text default 'demo',
  title       text default 'New chat',
  created_at  timestamptz default now(),
  updated_at  timestamptz default now()
);
create table dad_jokes_messages (
  id          bigserial primary key,
  thread_id   uuid references dad_jokes_threads(id) on delete cascade,
  user_id     text default 'demo',
  role        text,
  content     text,
  created_at  timestamptz default now()
);
alter table dad_jokes_threads disable row level security;
alter table dad_jokes_messages disable row level security;
```

Then paste the project URL and anon key into the settings modal (key chip top-right).
