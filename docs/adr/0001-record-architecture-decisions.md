# 1. Record architecture decisions

Date: 2026-06-09

## Status

Accepted

## Context

This is a Lane-2 product-intuition project built via grill → docs → issues → AFK. The
durable value is the judgment, so decisions need to be captured where future-me (and AFK
agents) can read the reasoning, not just the outcome.

## Decision

We will record architecturally significant decisions as ADRs in `docs/adr/`, numbered
sequentially. Lightweight (Nygard-style): Context, Decision, Consequences.

## Consequences

- Agents picking up issues have a documented rationale to align to.
- Reversals are explicit (a new ADR supersedes an old one) rather than silent drift.
