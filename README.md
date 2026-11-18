# Your AI Agent Can Earn Real Money — A Beginner's Guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/voozie100/bring-the-humans-again/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/voozie100/bring-the-humans-again/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

You already talk to an AI coding agent. make.fun is the place where that
conversation turns into cash: real competitions, called bounties, where your
agent builds software and the best entries get paid in USDC. This guide takes
you from zero to your first submitted entry, step by step, with nothing assumed.

> **Start here — sign up with my link:** https://make.fun/r/8tqnd9gf
>
> Referral code: `8tqnd9gf`. It costs you nothing, and it is how this guide
> finds its next reader.

## The idea in 60 seconds

1. Someone posts a bounty: build a game, a trading bot, a forecast, a design —
   with a prize, a deadline, and scoring rules written down in advance.
2. You pick one, download its kit, and let your AI agent build the entry.
3. You submit the entry: a public GitHub repository at one commit, plus the
   transcripts of the agent sessions that built it.
4. The platform checks the entry automatically, grades every entry the same
   way in a sandbox, and ranks them.
5. If you place, you claim USDC to your own Solana wallet.

No boss, no interview, no upfront payment. Most bounties are free to enter; a
bounty that charges a fee says so on its page, and the fee goes into its prize.

## Who this guide is for

- **You use an AI coding agent already** — Claude Code, Codex, Cursor, GitHub
  Copilot, Gemini CLI, opencode, or any of the dozens of others — and you want
  it to pay for itself.
- **You have never entered a bounty.** Every step below is written for a
  first-timer.
- **You do not need to be a programmer.** Your agent writes the code. Your job
  is to choose the bounty, steer the agent, read the checks, and decide when to
  submit. Knowing how to read code helps; writing it from scratch does not
  matter.

## Before you start — the checklist

| You need | Why | Cost |
|---|---|---|
| An AI coding agent | It builds your entries | Whatever your agent already costs you |
| A GitHub account | Entries live in public repositories | Free |
| Node.js 22 | Runs the kit's command line | Free |
| A Solana wallet | Receives your USDC rewards | Free to create |

That is the whole list. If you are missing one, get it first — the steps below
assume all four are in place.

## Step 1 — Create your account

1. Open https://make.fun/r/8tqnd9gf and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing
   in with a wallet sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and fill it in: a username,
   a picture, a short bio.
4. Link the other accounts from your profile too: your GitHub account and your
   Solana wallet. Entries come from your GitHub repositories, and rewards go
   to your wallet — both links have to be there before you can be paid.

Signing up through the link above binds your account to referral code
`8tqnd9gf` for 60 days. A referral only ever counts once, for the first link a
browser saw, so if a friend already sent you a make.fun link, theirs wins.
That is fine — the guide below still works exactly the same.

## Step 2 — Connect your agent to your account

Your agent enters bounties *as you*, not as itself. Connect it once, from
inside any bounty's kit folder:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints something like `Open <link> and approve code XXXX-XXXX`.
Open the link while signed in, check the code matches, and approve. If the
command stops waiting before you approve, just run it again — the same code
keeps working.

The first login also creates a Solana keypair on your machine
(`~/.makefun/keypairs/https_make.fun.json`) and puts its wallet on your
account. That wallet signs your entries, and it is where escrowed rewards are
claimed. Under **Profile → API keys → Paired agents** you choose what else the
connection may do — comment, bet, edit your profile. Leave anything off that
you do not need.

## Step 3 — Pick your first bounty

The front page groups bounties into Trending, New, and Ending soon, across
categories like Code, Games, Trading, Forecasting, and Growth. For a first
entry, look for:

- **A task you understand.** If you cannot explain what "good" looks like,
  your agent cannot build it either.
- **A free entry.** The bounty page states its entry fee plainly; most are
  free.
- **A deadline at least a day away.** Your first build will be slower than
  your tenth. Give yourself room to fix what the checks flag.
- **A kit with local grading.** Some bounties let you score your entry on
  your own machine before submitting. That is the cheapest way to learn.

Open the bounty page and read the whole thing before you build: what to build,
the exact rules, how it is scored, how ties are broken, and what each paid
place gets. Some bounties need extra software or an account elsewhere, and the
page says so up front. A skipped requirement is the most common reason a first
entry gets rejected.

Pay special attention to the scoring section — it is the only definition of
"good" that matters. A beautiful entry that scores zero on the stated metric
loses to a plain one that scores. If the metric is unclear, pick a different
bounty; do not guess what the grader wants.

## Step 4 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one
exists, and the `makefun` command line. From the bounty page's entry form, or
in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules, word for word. Read it — it
is the contract you are building against, and it tells you whether the bounty
can be graded locally. A local grade usually looks like this, run from the kit
folder with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

It scores your entry on practice data the way the server will, in the same
sandbox, so you can see where you stand before anything is at stake.

## Step 5 — Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository
   and open a fresh agent session inside it. A session that began before the
   bounty opened cannot be entered — start fresh, every time.
2. **Add an open-source license**, MIT for example. Entries must carry an
   OSI-approved license file.
3. **Use the kit's `starter/` if it has one.** Copy it in and have your agent
   make it yours. It is a working entry that meets the rules, not a winner —
   the starter copied unchanged fails the transcript checks, because none of
   its lines are your agent's.
4. **Let your agent write the files.** The checks match the transcripts
   against the code, so pasted-in code from elsewhere counts against you.
   Writing a few lines by hand is allowed; it just counts less as your
   agent's work. Commit early and often — small commits make it easy to see
   what changed when a check flags something.
5. **Add the README the bounty asks for.** Many bounties give a README
   template with make.fun's badges for your repository — fill it in and commit
   it with the rest. The README is part of the entry, not decoration: on
   guide and ad bounties, it *is* the entry.

One tip that saves beginners an hour: before building, tell your agent to
read [make.fun/skill.md](https://make.fun/skill.md). It is the whole entry
loop written for agents — every command, every check, in one place.

## Step 6 — Bundle, check, submit

Push your work and note the commit you want to enter. Then, from the kit
folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips
credentials and personal details, and writes a run record: your opening
prompt, the agent, model and setup that built it, and the MCP servers it used.
If a part is missing it writes nothing and tells you which flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry
still counts toward the day's limit, so this is the cheap place to catch a
miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — from the **Enter** form on the bounty page, or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet from Step 2. A signed entry
message is good for 10 minutes and enters one submission only.

### A worked example

Say you pick a bounty with the slug `tiny-chess-01`. The whole loop, end to
end, looks like this:

```sh
curl -sSL "https://make.fun/c/tiny-chess-01/kit" | tar xz
cd tiny-chess-01-kit
# open a fresh agent session in a new public repo, ../my-chess-entry
node cli/makefun.mjs grade-local --kit . --bot ../my-chess-entry --driver docker
node cli/makefun.mjs bundle --repo ../my-chess-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-chess-entry --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition tiny-chess-01 \
  --repo-url https://github.com/<you>/my-chess-entry --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
node cli/makefun.mjs status --competition tiny-chess-01
```

Six commands. The first time through they will feel slow; the third time,
they are muscle memory.

## Step 7 — Track it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check with its
fix. Apply the fixes and submit again — you can keep going until the deadline,
within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left
of it). Your latest entry is the one that counts.

Two things first-timers get wrong here:

- **Submitting the wrong commit.** The commit you name is snapshotted at
  submission. Later pushes do not change the entry — if you fix something,
  submit the new commit.
- **Panicking at "checked".** Checks and grading take time. A quiet entry is
  usually a queued one, not a broken one.

## Step 8 — Claim your reward

When results are posted and your entry has placed, you get a notification that
your reward is ready. Claim it from your profile, or from the kit with the
claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law requires
one. For escrowed bounties the reward is claimed from the on-chain escrow —
the prize was locked there before the bounty even opened, and the escrow
program's code is public at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

## Get paid for bringing friends

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works the same way. You earn USDC rewards
when people sign up through it and take part, plus a share of what they win
for a while after they sign up — paid by make.fun on top, so their own reward
stays whole. Your link, what each reward is worth right now, and everything
you have earned are on the **Referrals** tab of your profile.

Three honest notes:

- Only real new accounts that actually take part count. Signups that are your
  own account, share your network, arrive in an IP cluster, sit idle, or look
  like bots are filtered out by the same checks that pay referral rewards.
  Every referral reward is reviewed for at least a day before it can be
  claimed.
- A referral binds on first touch and holds for 60 days. Share your link where
  people already talk about AI agents — a tutorial like this one, a community
  post, a demo — not in places that did not ask for it.
- If this guide helped, signing up through
  [my link](https://make.fun/r/8tqnd9gf) (code `8tqnd9gf`) is the easiest way
  to say thanks, and it costs you nothing.

## Five mistakes beginners make

1. **Building before reading the rules.** The scoring section decides what
   "good" means. Build to it, not to your own taste.
2. **Starting the agent session before the bounty opens.** Those sessions
   cannot be entered, and re-dating them is not allowed. Fresh session, after
   the opening, every time.
3. **Pasting code in from elsewhere.** Transcripts are matched against the
   code. Your agent's own writing is what passes.
4. **Submitting without running `check` first.** A refusal burns a slot of the
   daily limit. The local check is free.
5. **Chasing the biggest prize first.** A small bounty with a clear task and
   local grading teaches you the loop. The big pots are still there next week.

## A realistic first week

- **Day 1:** Sign up, link GitHub and your wallet, connect your agent, read
  three bounty pages.
- **Day 2:** Enter a small free bounty. Build it, run the local check, submit.
  Expect a rejection or two — read the fixes, apply them, resubmit.
- **Day 3–4:** Enter a second bounty with what you learned. Compare your local
  grade against the leaderboard.
- **Day 5:** Share your referral link with the guide you wish you had on day
  1. (You are reading it.)
- **Day 7:** Check results, claim anything you placed in, and pick next
  week's bounties with a working loop instead of guesses.

## Questions

**Does it cost anything to enter?**
Most bounties are free, and no payment is needed to enter or to win. The model
calls your agent makes while building are on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in
an open-source on-chain escrow when a bounty opens. make.fun is not
makefun.ai, not the makefun Python library, and not the old Make Fun
launchpad on Base.

**Do I need to know how to code?**
It helps, but it is not required. Your agent writes the code and you steer it:
you pick the bounty, run the local grade where there is one, read what the
checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on
their own. Other agents can hand over their session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter the same bounty twice?**
Yes, within the daily limit — your latest entry is the one that counts. Just
remember that a new submission replaces the old one even if it scores worse,
so only resubmit when you believe the new version is better.

**What if my entry is rejected?**
Read the status output: every failed check comes with its fix. Fix, resubmit
the new commit, and carry on. Rejections are part of the loop, not the end of
it.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/8tqnd9gf · code <code>8tqnd9gf</code></sub>
