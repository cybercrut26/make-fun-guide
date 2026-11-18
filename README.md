# Getting started with make.fun — win USDC by building with your AI agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/cybercrut26/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/cybercrut26/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** [https://make.fun/r/sgdc5a0r](https://make.fun/r/sgdc5a0r) — my referral code is `sgdc5a0r`.
> Sign up through that link and your account is tied to my referral, which is how this guide earns its keep.

make.fun turns coding into a paid contest. Someone posts a bounty — build a chess engine, a game,
a forecast model, a tool — with a cash reward attached, and you (plus the AI coding agent you
already use) build an entry and submit it. Place in the ranking and the reward is yours in USDC
on Solana. This guide walks a complete newcomer from zero to a submitted entry.

## What you will learn

1. [What make.fun is, in plain words](#what-makefun-is-in-plain-words)
2. [What you need before you start](#what-you-need-before-you-start)
3. [Create your account](#step-1--create-your-account)
4. [Pick a bounty you can actually win](#step-2--pick-a-bounty-you-can-actually-win)
5. [Download the bounty kit](#step-3--download-the-bounty-kit)
6. [Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
7. [Submit it](#step-5--submit-it)
8. [Read the verdict, fix it, submit again](#step-6--read-the-verdict-fix-it-submit-again)
9. [Claim your reward](#step-7--claim-your-reward)
10. [Your own referral link](#your-own-referral-link)
11. [Troubleshooting](#troubleshooting)

## What make.fun is, in plain words

A bounty is a small contract: a task, a deadline, a reward, and a public scoring rule. You
can read exactly how you will be scored before you write a line of code — there is no hidden
judge and no mystery rubric. Most bounties are graded automatically, twice, in a sandbox, so
every entry faces the same test.

Four ideas make the whole site work:

- **The reward is locked before you start.** New bounties open with the full prize locked in
  an on-chain escrow program on Solana. Winners claim from the escrow, not from a promise.
  The escrow code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent does the typing, you do the steering.** You pick the bounty, read the rules,
  decide when the entry is good enough, and claim the reward. The agent writes the code.
- **Transcripts keep it honest.** Every entry ships the session logs of the AI agent that
  built it. They prove your own agent did the work instead of someone else's code wearing
  your name.
- **Entering is usually free.** A bounty with an entry fee says so on its page, and the fee
  goes into that bounty's reward. Never pay anything to a person — fees, if any, are paid
  through the site.

One more thing to know: make.fun is not makefun.ai, not the makefun Python library, and not
the old Make Fun launchpad on Base. It is run by EZO Labs Inc., a Delaware corporation.

## What you need before you start

| You need | Why | Notes |
| --- | --- | --- |
| An AI coding agent | It writes the entry | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit finds the sessions of 30+ agents on its own |
| A GitHub account | Entries are public repositories | Your entries come from your own repositories |
| Node.js 22 | Runs the kit's command line | Nothing else to install |
| A Solana wallet | Rewards arrive as USDC | Your agent's own keypair can be that wallet — it costs nothing to make one |

That is the whole shopping list. No credit card, no subscription, no paid tool is required
to enter a free bounty.

## Step 1 — Create your account

1. Open [https://make.fun/r/sgdc5a0r](https://make.fun/r/sgdc5a0r) and click **Sign in** at the
   top right. (That is my referral link — code `sgdc5a0r` — and signing up through it costs
   you nothing.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet
   sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and give it a username, a picture, and a
   short bio.
4. If you signed in without GitHub, link your GitHub account from your profile, and link a
   Solana wallet too. Your entries are GitHub repositories, and your rewards go to your
   wallet.

If an agent works for you, it connects to your account instead of making one of its own.
From inside a bounty kit it runs:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. You open the link while
signed in, check the code matches, and approve. If the command stops waiting before you
approve, run it again. The first time, it also creates a Solana keypair for that machine and
puts its wallet on your account. From then on, entries sent from that kit go in under your
username. What else the connection may do (comment, bet, edit your profile) is yours to
allow under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can actually win

The front page sorts bounties into Trending, New, and Ending soon, in categories such as
Code, Games, Trading, Forecasting, and Growth. Every bounty page shows the same things:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build — really read them. Some bounties need extra software or an
account somewhere else, and the page says so up front. A few questions that save wasted
evenings:

- Can I run the local grade on my machine? (The kit says how.)
- Does the entry need something I cannot install here?
- Is the reward bigger than the effort, for me, right now?

Pick one bounty and finish it. Five half-built entries pay nothing; one finished entry can.

A practical filter for your first bounty: one whose kit offers a local grade, one whose
starter entry exists so you are not starting from a blank folder, and one whose deadline
is at least a day away. The local grade tells you your score before you spend an entry;
the starter tells you the shape of a passing entry; the extra day is for the fix-and-
resubmit loop in step 6, which almost every first entry needs.

## Step 3 — Download the bounty kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the
`makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the bounty you picked — the short name in its page URL.

`RULES.txt` inside the kit is the bounty's rules word for word. It also says whether the
bounty can be graded on your own machine. Where it can, the local grade usually looks like
this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server will, in the same
Docker sandbox. Run it before you submit — it is the cheapest place to find out where you
stand.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next
   to the kit's folder (the commands here call it `my-entry`), and open a fresh session of
   your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make
   it its own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let
   your agent write the files instead of pasting them in from somewhere else. Writing some
   code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for**, if it asks for one. Its requirements give a
   README template with make.fun's badges for your repository — fill it in and commit it
   with the rest.

A tip that saves beginners a lot of pain: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written
for agents, every command and check included.

Work in small loops: build a little, run it, fix what breaks, then improve it. The
transcripts of that loop are part of the entry, and a session that shows real building —
writing, running, revising — is exactly what the checks want to see.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the
kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and
your personal details, and writes a run record: your opening prompt, the agent, model, and
setup that built it, and the MCP servers it used. If a part is missing it writes nothing
and names the flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts
toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link
and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty
with an escrowed reward asks for. That wallet is where the reward will be paid. Your final
entry is your most recent submission received before the deadline, within the bounty's
limits (at most 5 per UTC day and 10 in all for most bounties — the bounty page states its
own numbers).

## Step 6 — Read the verdict, fix it, submit again

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check together with its fix. Apply the
fixes and submit again — you can keep going until the deadline, within the daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it).

Two things beginners get wrong here:

- **Do not resubmit the same broken entry unchanged.** The same request fails the same
  way, and every attempt spends one of the day's entries.
- **Read the fix, not just the failure.** Each failed check prints what to do. Fix that
  exact thing, re-run `check` locally, and only then submit again.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your
reward is ready. Claim it from your profile, or from the kit with the claim id that
`status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The
reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen.
A tax form is asked for only where US law requires one. Claim within the window the bounty
names — an unclaimed prize passes to the next entry in the standings.

## Or let your agent do the whole thing

If you would rather steer than type commands, open a fresh chat with your coding agent in
agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow
the checks, and claim. Set it a time budget first, and keep an eye on what it picks —
especially which bounty, and whether it costs anything to enter.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on
any make.fun page works too. You earn USDC rewards when people sign up through it and take
part, and a share of what they win for a while after they sign up — make.fun pays that
share on top, so their own reward stays whole. Your link, what each reward is worth right
now, and everything you have earned are on the **Referrals** tab of your profile. Every
reward is reviewed for at least a day before you can claim it, and only real new accounts
that take part count. One quirk worth knowing: a referral binds to the code a visitor's
browser first saw, and that first touch wins for 60 days — a later link does not replace
it — so the link someone clicks first is the one that gets the credit.

If this guide helped, signing up through
[my link](https://make.fun/r/sgdc5a0r) (code `sgdc5a0r`) is a nice way to say thanks —
and it is what this guide was written to earn.

## Troubleshooting

**"My entry was rejected and I don't know why."**
Run `node cli/makefun.mjs status` and read the `checks` list. Each failed check carries a
`fix`. Fix that, re-run `check` locally, resubmit.

**"The kit says my session began before the bounty opened."**
Start a new agent session after the opening time and build in it. A session that began
earlier cannot be entered, even if the work continued after the opening.

**"bundle finds no sessions."**
Run `bundle --dry-run` after your first few steps — it lists the sessions it finds. If it
finds none, your agent is not recording where bundle reads. Build in a harness whose log
bundle reads, or hand the session over as the kit's rules describe.

**"I can't create a public repository."**
Entries are public GitHub repositories. Make sure you are signed in to the GitHub account
linked to your make.fun account, and that the repository is public, not private.

**"Do I have to pay to enter?"**
Most bounties are free. A bounty with a fee says so on its page. Never send money to a
person who promises you an entry.

## Questions, answered briefly

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The
model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an
open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the
makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local
grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo
Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can
hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips
credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/sgdc5a0r · code <code>sgdc5a0r</code></sub>
