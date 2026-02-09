# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

French driving license quiz app ("Quiz Permis de Conduire"). A single-page progressive web app with zero external dependencies — pure HTML/CSS/JS in one file (`index.html`).

Hosted via GitHub Pages at https://dwursteisen.github.io/Quizz-voiture

## Running Locally

Open `index.html` directly in a browser. No build step, no server required.

## Architecture

Everything lives in `index.html` (~2800 lines):

- **Lines 1–242**: `<style>` block — all CSS including responsive layout and foreigner mode styling
- **Lines 244–281**: HTML body — minimal DOM with question display area, answer toggle, and config panel
- **Lines 282–2814**: `<script>` block containing:
  - `questionsFullData` array (lines 285–2662): 99 question sets (IDs "01"–"99"), each with three sub-questions:
    - `verification` (type VE or VI) — vehicle check questions
    - `qser` (type QSER) — road safety questions
    - `premier_secours` (type "1er secours") — first aid questions
  - Each sub-question has: `question`, `answer`, `answer_en` (English translation), `answer_simple` (simplified French)
  - Foreigner mode logic (lines 2664–2713): toggleable config panel stored in `localStorage`, supports modes: `english`, `simple`, `both`, `off`
  - Quiz logic (lines 2715–2812): random question selection (avoids repeating last question), answer show/hide

## Key Patterns

- **Single-file app**: all styles, markup, data, and logic are in `index.html`. No separate JS/CSS files.
- **No frameworks**: vanilla JS with direct DOM manipulation
- **PWA support**: `manifest.json` + icons in `images/` for installability
- **State**: `foreignerMode` persisted in `localStorage`; quiz state (`currentQuestionData`, `lastQuestionIndex`) is in-memory only

## Foreigner Mode

The "foreigner mode" feature (current branch `feat/foreigner-mode`) adds translations alongside French answers:
- English translations (`answer_en`) shown with blue background
- Simplified French (`answer_simple`) shown with yellow background
- Config gear icon in top-right corner toggles a panel to select mode
