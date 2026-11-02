# Holding HQ (showcase)

Public showcase for a private project. The source code is not published here.

Holding HQ is the control layer I built to run several small "studios" with AI agents and limited human attention. A manager agent checks on each studio, enforces a budget and a policy, verifies evidence of work, and reports to me in short messages.

## The problem

I run more than one thing at once: a website-building business, a Roblox game, and a software-delivery lane. AI agents can do a lot of the work, but unattended agents have predictable failure modes: they spend money, report work as done without proof, collide on the same repo, and fill a backlog just to look busy. I wanted agents that move the studios forward without me babysitting, inside hard limits.

## How it works

Three layers:

0. **Watchdog (no AI).** A scheduled script every ten minutes restarts services, flags agents that are in error or late, and writes alerts.
1. **Manager.** On a schedule, an agent reads each studio's state, checks the budget, unblocks or chases the studio agents, verifies evidence, updates a dashboard and writes a daily report.
2. **Studios.** Each studio has its own agents (a lead plus a team) and a small set of files: a vision (what I want it to become), a goal (what success means now), a state file and a playbook.

I can send requests to the manager over WhatsApp. They become tasks. A morning summary and replies go back the same way.

## Design notes

- **Policy as a file, enforced in code.** The rules (no pay-per-use API keys, no direct pushes to the main branch, no force-push, no touching credentials, no publishing the game to production without a veto window) are written in a policy document and also enforced by a pre-tool-use hook that blocks the commands. The manager cannot talk its way around them.
- **Budget before spending.** Each studio gets a share of the weekly subscription quota. A guard script returns GO or STOP before AI work is dispatched.
- **Evidence or it did not happen.** A task is only done with proof: passing tests, a screenshot, a PR, a ledger line.
- **Agents never edit my working folders.** They work in separate git worktrees on their own branches and deliver by pull request. Auto-merge exists only for those branches, only with a reviewer agent's approval on the current commit, and only when checks are green.
- **Fewer tasks, each with a reason.** Every task must say what it is for and what "done" looks like. Limits per agent and per studio stop backlog inflation. Tasks assigned to me follow a four-line format: what it is, what for, why it needs me, first step.
- **No polling of metered services.** The automation plan has a monthly execution cap, so everything is push-based. A polling loop once burned a large share of the cap in hours.
- **Append-only ledgers** record runs, decisions, quota use and blocked actions.

## Architecture

Node scripts and systemd units on a small always-on Linux machine; an agent orchestration tool for the agent companies and tasks; n8n for the WhatsApp in/out and outreach workflows; a local dashboard; GitHub Actions for checks; Playwright for reel and screenshot generation.

## Stack

Node.js (ESM, `node --test`), shell and PowerShell, Claude Code and Codex CLI agents, n8n, GitHub CLI, Playwright, ffmpeg.

## Status

In use since 20 October 2026, running on a mini PC since 26 October 2026. It is operational tooling for my own studios, not a product. The studios it manages are early and I am not claiming results from it here.

## What is shown and what is kept private

Only this README is public. The source is private because it contains business internals (outreach logic, cost data, operating ledgers). The ideas above are the part worth sharing.
