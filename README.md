# Holding HQ (showcase)

Public showcase for a private project. The source code is not published here.

Holding HQ is the control layer I built to run several small companies ("studios") with AI agents and limited human attention. A manager agent checks on each studio, keeps it inside a budget and a set of rules, verifies that work was really done, and reports to me in short messages. From it I control Frontstep and OpenClaw HQ.

## The problem

I run more than one thing at once. AI agents can do a lot of the work, but unattended agents fail in predictable ways: they spend money, report work as done without proof, get in each other's way, and fill a backlog just to look busy. I wanted agents that move the studios forward without me babysitting, inside hard limits.

## How it works

Three layers:

1. **A simple watchdog**, with no AI, that notices when something stopped or is late and raises an alert.
2. **A manager agent** that, on a schedule, reads each studio's state, checks the budget, unblocks or chases the studio agents, verifies evidence, and writes a daily report.
3. **The studios.** Each one has its own agents and a short set of documents: what I want it to become, what success means now, where it stands, and how it operates.

I can send requests to the manager by message. They become tasks, and I get a morning summary and replies the same way.

## Principles

- **Rules the manager cannot talk its way around.** Spending limits, no direct changes to live systems, and no publishing without a veto window are enforced, not just written down.
- **Budget before spending.** Each studio gets a share of the weekly budget, and work only starts if there is room.
- **Evidence or it did not happen.** A task counts as done only with proof, such as passing tests, a screenshot or a review.
- **Agents never touch my own files.** They work on separate copies and deliver changes for review.
- **Fewer tasks, each with a reason.** Every task says what it is for and what done looks like, with limits so the backlog cannot inflate. Tasks for me are short: what it is, what for, why it needs me, first step.
- **Everything is recorded** in a log of runs, decisions and blocked actions.

## The idea

Build many small companies like this and have the agents report to me, so one person can run a holding.

## Status

In use on my own studios since October 2026. It is operational tooling, not a product, and I am not claiming results from it here.

## What is shown and what is kept private

Only this README is public. The source is private because it contains business internals.
