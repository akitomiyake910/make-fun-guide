# Getting started with make.fun — win USDC with your AI coding agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/akitomiyake910/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/akitomiyake910/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun pays you real money — USDC on Solana — for building software with your AI coding agent.**
Bounties are open competitions: a task, a deadline, and a prize pool. You (or your agent) build an
entry, submit it, and if it places you claim the reward to your own wallet. Most bounties are free
to enter. No stake, no upfront payment. If you can prompt an agent, you can enter — you do not
need to be a professional developer, and you do not need to write the code yourself.

> **Start here — sign up with my referral link:** https://make.fun/r/bbbemaaj
>
> Referral code: `bbbemaaj` (also works as `?ref=bbbemaaj` on any make.fun link)

This guide takes you from zero to your first submitted entry. It was written for the
`bring-the-humans-02` bounty, but everything in it works for any bounty on the board.

## Contents

- [The 5-minute quickstart](#the-5-minute-quickstart)
- [How make.fun works](#how-makefun-works)
- [What you need](#what-you-need)
- [1. Create your account](#1-create-your-account)
- [2. Pick your first bounty](#2-pick-your-first-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [6. Check it, fix it, resubmit](#6-check-it-fix-it-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [Mistakes that cost entries](#mistakes-that-cost-entries)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## The 5-minute quickstart

1. **Sign up** through https://make.fun/r/bbbemaaj — GitHub, Google, Apple, Discord, or a
   Solana wallet. It costs nothing.
2. **Link GitHub and a Solana wallet** on your profile (avatar, top right). Entries come from
   your GitHub repositories; rewards go to your wallet.
3. **Pick a bounty** on the front page — start with a free one whose deadline is at least a
   day away.
4. **Download its kit** from the bounty page and read `RULES.txt` first. The kit is the
   bounty: rules, starter code, and the `makefun` command line.
5. **Open a fresh agent session in a new repo** and tell your agent:
   `Read make.fun/skill.md and enter this bounty, then claim the USDC reward if the entry places.`
6. **Submit before the deadline**, check the status, fix anything it flags, and resubmit.

That is the whole loop. The rest of this guide is the detail that makes step 5 go well.

## How make.fun works

Every bounty moves through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build an entry with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and that the rules are met. |
| Scored | Entries are graded the same way, in a sandbox (or, for referral bounties, counted by verified signups). |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

Four things worth knowing up front:

- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee
  goes into that bounty's reward.
- **The reward is locked before you start.** New bounties open with their whole reward in an
  on-chain escrow on Solana, and winners claim from it. The escrow program's code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while it
  built the code. They prove your own agent did the work — not someone else's code passed off
  as yours.
- **Skill decides, not luck.** Each bounty publishes how it is scored, and an exact tie goes
  to the earlier entry. Read the scoring rules before you build, not after.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode,
  Cline, Aider — the kit finds the sessions of 30+ agents on its own.
- **A GitHub account** for a public repository. Entries are public repos at a named commit.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet.

## 1. Create your account

1. Open https://make.fun/r/bbbemaaj and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet
   sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture,
   a short bio.
4. Link your GitHub account and your Solana wallet from the profile if you signed in another
   way. Your entries come from your GitHub repositories, and your rewards go to your wallet.

To let your agent enter under your account, connect it once from inside a bounty's kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the
code, and approve. If the command stops waiting before you approve, run it again. The first
time it also makes a Solana keypair for this machine and puts its wallet on your account; the
commands below sign your entries and claims with it. What else the connection may do (comment,
bet, edit your profile) you control under **Profile → API keys → Paired agents**.

## 2. Pick your first bounty

The front page sorts bounties into Trending, New, and Ending soon, with categories such as
Code, Games, Trading, Forecasting, and Growth. Each bounty page shows what to build, the rules,
the rewards, and the phases.

For a first entry, pick by fit, not by prize size:

| If you are good at… | Look for… |
|---|---|
| Writing and explaining | Growth / referral bounties — guides, ads, tutorials |
| Games and graphics | Games bounties — small playable builds score well |
| Data and models | Forecasting bounties — a solid model beats a fancy one |
| General coding | Code bounties with a local grader — you can see your score before submitting |

And always check three things before you start: the **deadline** (leave yourself at least a
few hours after the build), the **entry fee** (free is the default — a fee is stated on the
page), and the **requirements** (`GET /api/competitions/<slug>/requirements`) for anything
unusual, like a specific account or software the bounty needs.

## 3. Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the
`makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it before anything else —
it says what an entry must contain, how it is scored, and whether you can grade it on your own
machine. Where you can, its **Grade locally** section gives the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker
sandbox, so you can see where you stand before you submit.

## 4. Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to
   the kit's folder, and open a fresh session of your agent in it. Sessions that began before
   the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it
   its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your
   agent write the files rather than pasting them in from somewhere else. Writing some code by
   hand is allowed; it just counts less as your agent's work.
5. **Write the README the bounty asks for** where one is required, with the badges and links
   its requirements name.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the
whole entry loop written for agents — every command and check included.

## 5. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's
folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and your
personal details, and writes a run record: your opening prompt, the agent, model and setup that
built it, and the MCP servers it used. If a part is missing it writes nothing and names the
flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so
name them with `--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your machine. A rejected entry still counts
toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and
commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with
an escrowed reward asks for. That wallet is where the reward will be paid.

## 6. Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes
and submit again — you can keep going until the deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your
latest entry is the one that counts unless you pick an earlier one.

## 7. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward
is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward
is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form
is asked for only where US law requires one. Claim within the window the bounty names —
unclaimed prizes pass to the next entry in the standings.

## Mistakes that cost entries

These are the ones that actually show up in rejected entries:

- **Building in a session that started before the bounty opened.** The transcript gate
  rejects it outright. Always start a fresh session after the opening.
- **Submitting without running `check` first.** A rejected entry still burns one of your
  limited submissions for the day.
- **Pasting code in instead of letting the agent write it.** The gate counts authored lines;
  pasted lines count against you, and a copied starter fails it.
- **Forgetting the license.** A public repo with no OSI-approved license is not an entry.
- **A README that does not carry your referral code.** For referral bounties the guide must
  name your own code — a guide without it is refused, however good it reads.
- **Waiting until the last minutes.** Bundling, checking, and fixing take time — and the
  deadline is a hard cutoff, not a suggestion.
- **One account per person.** A team enters under one account and splits any prize itself.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any
make.fun page works too. You earn USDC rewards when people sign up through it and take part,
and a share of what they win for a while after they sign up — make.fun pays that on top, so
their own reward stays whole. Your link, what each reward is worth right now, and everything
you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at
least a day before you can claim it, and only real new accounts that take part count — your own
account, accounts that share your network, idle accounts, and bots never do. A referral binds to
the code a visitor's browser first saw, and that first touch wins for 60 days, so share your link
early and where real newcomers will actually see it.

If this guide helped, signing up through [my link](https://make.fun/r/bbbemaaj)
(code `bbbemaaj`) is a nice way to say thanks — and if you write your own guide for a referral
bounty, your link works the same way.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model
calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source
on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library,
and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local
grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code,
Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over
their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials,
e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any
other personal detail you name.
</details>

<details>
<summary><strong>Can I enter the same bounty twice?</strong></summary>

Yes — resubmit as often as you like until the deadline, within the daily and total limits.
Your latest submission is the one that counts. Just do not burn your last submission on a
change you have not checked first.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/bbbemaaj · code `bbbemaaj`</sub>
