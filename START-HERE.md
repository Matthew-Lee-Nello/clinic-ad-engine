# Start here, Daniel

This is your setup guide. Read it top to bottom once, then follow the steps. It takes about 20 to 30 minutes the first time.

Tip: you can paste this whole file into Claude Code and say "walk me through this step by step" and it will do each step with you.

---

## What this actually is

It is a media-buyer that lives inside Claude Code. You give it a client's Google Drive folder, a treatment, and a country. It does the front-of-funnel work you normally do by hand: the research, the market sizing, the competitor and swipe work, the angles, the copy, the video scripts, the static concepts, and it can build the paused campaign in Meta. It runs the Jeremy Haynes method, writes copy off Eugene Schwartz's Breakthrough Advertising, and it will not break Singapore's advertising rules.

The big idea: it does the **research first**, produces one standard brief, and you approve that brief before it writes a single ad. Same process every client, every treatment. That is the part that lets you scale.

## What it can do (honest)

- **Research (the strong part).** For any treatment it builds a full Market and Strategy Brief: who the doctor is and their real edge, the treatment and the patient's real questions, the **TAM** (market size) in that country with the working shown, what competitors run, winning concepts swiped from any market, where the gap is, and the game plan. This is genuinely good and it is the same every time.
- **Angles and copy.** 25 to 30 genuinely different angles from the approved brief, plus 5 headlines and 5 body copies and a short film-it script per angle. Compliant.
- **Swipe.** Point it at any winning ad, anywhere (image or video), and it reads the concept and rewrites it as yours, compliantly.
- **Statics.** It can generate static images, but see the honest limits below.
- **Launch.** It can build the campaign in Meta, paused: one cold campaign, three ad sets, the same ads in each, ABO budgets, auto-features off, using the exact upload method Matt uses on his own accounts.

## What it cannot do yet (also honest, so you are not surprised)

- **It does not run itself.** You drive it in Claude Code, step by step. It is a very good assistant, not a robot that replaces you.
- **It does not optimise your live campaigns.** The scaling loop (duplicate, keep the no-reach ads, pull the winners) is a plan you follow, not something it does automatically.
- **The static images are the weak part.** AI images of medical ads come out average. The video scripts (your doctor films them) are far stronger. Treat the AI statics as rough starts, not finished ads.
- **Compliance is lowered, not guaranteed.** It checks every line against the Singapore rules, but your doctor still signs off every ad. It reduces your risk, it does not remove it.
- **The Meta launch step is new.** The upload method is the same one Matt runs daily, but this specific build has not been run on a live account yet. Do the first launch on a small budget and eyeball it.

---

## Before you start, you need

- **Claude Code** installed and working (you already use it).
- **A Meta ad account** you can access, and the ability to make a token for it (below).
- Four keys: **Meta**, **Apify**, **Exa**, **OpenAI**. Where to get each is in Step 2.
- **Composio** with **Google Drive connected** (you have Composio already). This is how it reads each client's folder.

---

## Step 1: Get the repo onto your machine

Matt will send you access to the private repo `Matthew-Lee-Nello/clinic-ad-engine`. Once you have access:

```
gh repo clone Matthew-Lee-Nello/clinic-ad-engine
cd clinic-ad-engine
```

If you do not use `gh`, download the folder Matt sends and open it in Claude Code.

## Step 2: Set your keys

The engine reads these from your environment. Put them in a `.env` file in the repo, or export them in your shell. Never share them.

| Key | What it is for | Where to get it |
|---|---|---|
| `META_ACCESS_TOKEN` | Building and reading Meta campaigns | See "Connecting Meta" below |
| `APIFY_TOKEN` | Scraping the Meta Ad Library + building the Mark Builds Brands corpus | apify.com → Settings → Integrations → API token |
| `EXA_API_KEY` | Web research (treatment, market, TAM) | exa.ai → dashboard → API key |
| `OPENAI_API_KEY` | Generating the static images | platform.openai.com → API keys |

### Connecting Meta (two ways)

- **Easiest to start (Pipeboard one-click):** go to pipeboard.co, log in with your Meta account, copy the token it gives you, and set it as `PIPEBOARD_API_TOKEN` instead of `META_ACCESS_TOKEN`. Then open `.mcp.json` and change the one line under `meta-ads` from `META_ACCESS_TOKEN` to `PIPEBOARD_API_TOKEN`. A two-minute login.
- **What Matt runs (proven, a bit more setup):** create a **system-user token** for your ad account in Meta Business Settings (Business Settings → Users → System Users → add → generate token, give it the ads permissions and your ad account). Set it as `META_ACCESS_TOKEN`. This is the exact setup Matt uses on his own accounts.

Start with Pipeboard if you want to move fast. Switch to a system-user token later if anything is off.

### Connecting Google Drive (Composio)

In your Composio, connect the **Google Drive** app and authorise it. The engine's `client-core` step uses that connection to read a client's folder. If you would rather not use Composio for a client, you can also just download that client's Drive folder to your machine and point the engine at the local path.

## Step 3: Restart Claude Code

Close and reopen Claude Code in the repo folder so it loads the tools from `.mcp.json`.

## Step 4: Run the bootstrap (one time)

In Claude Code, say: **"run BOOTSTRAP.md"**.

It will check your keys, build the Mark Builds Brands knowledge base (scrapes his channel, a few minutes), and then run a full self-test on a sample clinic so you can see it work end to end. It never launches anything live. When it prints the green checklist, you are ready.

---

## Step 5: Run your first real client

1. Make sure the client's Drive folder is connected in Composio (doctor photos, videos, onboarding notes, their point of difference).
2. In Claude Code, say: **"run /clinic-campaign for &lt;treatment&gt; in &lt;country&gt;, client folder &lt;drive folder link or name&gt;"**.
3. It does the research first and writes the brief to `clients/&lt;client&gt;/00-brief.md`. **Read it.** This is the moment that matters. Check the TAM, the positioning, the game plan. If it is right, tick the approval box in the brief. If not, tell it what to fix.
4. Once you approve, it writes the 25 to 30 angles, the copy, the video scripts, and the static concepts.
5. Your doctor films the video angles (the scripts are ready for them).
6. When you are ready, say **"run /launch"**. It builds the campaign in Meta **paused**. You open Meta, look at it, and only you set it live.

That is the whole loop. Every new treatment or client, same steps.

## Using the pieces on their own

You do not have to run the whole thing. Any of these work standalone:
- **"/market-research"** or "build the brief for X" - just the research and the brief.
- **"/market-sizing"** or "what's the TAM for X in Y" - just the market size.
- **"/swipe &lt;ad link&gt;"** - read one winning ad and get a compliant version for your treatment.
- **"/ask-hormozi"** - pressure-test an offer or a hook.
- **"/copywriter"** - write or fix copy using the Breakthrough Advertising method.
- **"/ask-mark"** - creative and brand-style direction (once his corpus is built).

## The golden rules (do not break these)

- Compliance always wins. If a great line breaks the Singapore rules, it gets cut. The rules are in `knowledge/singapore-ad-compliance.md`.
- Your doctor signs off every ad before it runs. The engine lowers the risk, you and the doctor own it.
- Nothing goes live in Meta without you clicking it. The engine only ever builds paused.
- No made-up numbers, results, or testimonials. Ever. If it cannot back a claim, it does not make it.

## When to message Matt

- The bootstrap self-test comes back red on something.
- A key will not connect (Meta, Composio, Apify).
- The first live launch looks off.
- You want it pointed at a new niche outside clinics, or a country other than Singapore (the compliance rail is Singapore-specific right now).

That is it. Start with the bootstrap, then run one real client end to end. The research brief is where the value is, so spend your attention there.
