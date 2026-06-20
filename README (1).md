# StudyBuddy — AI Learning Tool

A simple single-page web app that sends text to Google's Gemini API and displays the AI's response. Built for **Task 1: Build Your First AI Tool**.

## What it does

You type or paste some text, pick one of 6 features, and the app sends a tailored prompt to the Gemini API and shows the response on the page. Every response is added to a running history so you can see your past results.

## Features included

1. **Explain a Concept** — explains a topic in a few clear paragraphs
2. **Summarize Text** — condenses a passage into 3–5 sentences
3. **Generate Quiz Questions** — writes 5 quiz questions with answers
4. **Bullet Points** — converts text into an organized bulleted list
5. **Explain Like I'm 5** — simplifies a concept using an analogy
6. **Generate Flashcards** — creates 5 Q/A flashcards from the text

(Only 3 were required — this has double, so you've got options to demo.)

## Bonus features implemented

- ✅ **Chat history** — every prompt/response pair stays visible, newest on top
- ✅ **Web interface** — plain HTML/CSS, no frameworks needed
- ✅ **Markdown rendering** — responses render bold text, lists, code blocks, etc. using `marked.js`
- ✅ **Loading animation** — a spinner shows while waiting on the API
- ✅ **Empty input handling** — clicking Generate with no text shows an inline error instead of calling the API

## How to run it

1. Get a free API key at **https://aistudio.google.com/apikey** (no credit card needed).
2. Open `index.html` in a text editor.
3. Find this line near the top of the `<script>` section:
   ```js
   const GEMINI_API_KEY = "PASTE_YOUR_GEMINI_API_KEY_HERE";
   ```
   Replace the placeholder with your actual key.
4. Save the file, then double-click `index.html` to open it in your browser (Chrome, Firefox, Edge — any modern browser works).
5. Pick a feature, type something in the box, and click **Generate →**.

No installation, no server, no npm, no payment — it's a single static HTML file using a free API.

## How it works (architecture)

```
User types text + picks a feature
         ↓
JS builds a prompt from a template, e.g.
  "Summarize the following text in 3-5 sentences: {user text}"
         ↓
fetch() sends the prompt to the Gemini API (generateContent endpoint)
         ↓
Gemini returns JSON containing the model's text response
         ↓
Response is parsed, rendered as Markdown, and added to the on-page history
```

Each "feature" in the code is just an object with a label and a function that wraps the user's input in a specific instruction — see the `FEATURES` array in `index.html` to add your own.

## Project structure

```
ai-tool/
├── index.html      # everything: HTML, CSS, and JS in one file
└── README.md        # this file
```

## Notes / limitations

- The API key is stored directly in the client-side JS, which is fine for a local class project but **not safe for a publicly deployed site** (anyone viewing the page source could see your key). For production use, you'd proxy the request through a backend server that holds the key secretly.
- Requires an internet connection to reach the Gemini API.
- If you'd rather use OpenAI or Anthropic instead of Gemini, swap out the `callGemini()` function and `GEMINI_URL` for the equivalent endpoint — the rest of the app (UI, history, prompts) doesn't need to change.

## Demo video

See `demo.mp4` (or linked submission) — a 2-minute walkthrough showing:
1. Empty input handling
2. Explain a Concept
3. Summarize Text
4. Generate Quiz Questions
5. Chat history building up across requests
