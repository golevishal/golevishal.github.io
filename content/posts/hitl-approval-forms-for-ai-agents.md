---
title: "Building Human-in-the-Loop Approval Forms for AI Agents"
date: 2026-05-22T00:00:00Z
draft: true
tags: ["AI Agents", "React", "TypeScript", "Agent UI", "Human-in-the-loop"]
summary: "A follow-up on designing structured approval forms for agent workflows, including validation, user responses, and backend handoff."
ShowToc: true
---

AI agents become much more useful when they can pause, ask for structured input, and continue with a human-approved decision. This post will explore how to design human-in-the-loop approval forms for agent workflows without coupling every approval path to a custom frontend component.

## The Interaction Model

An approval form needs a clear contract between the agent, the renderer, and the backend system. The agent should describe the requested action, the fields it needs, and the validation constraints. The renderer should collect input and emit a structured response.

## What The Agent Sends

The event payload should include enough information to render a useful form:

- the action being requested;
- field labels and types;
- required fields;
- validation rules;
- submit and cancel actions;
- context that helps the user make a decision.

## What The Renderer Owns

The frontend should own the product experience: layout, validation display, accessibility, loading states, and error handling. This keeps the protocol focused on intent instead of presentation details.

## What The Backend Receives

When the user submits, the backend should receive a predictable `USER_RESPONSE` event with the selected action and field values. That response can resume the agent workflow without relying on UI-specific callbacks.

## Open Questions

There are still interesting design questions around retries, expired approvals, audit trails, and partial form updates while an agent is still working. Those are the areas I want to dig into next.
