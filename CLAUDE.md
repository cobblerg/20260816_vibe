# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository is a single self-contained static HTML page: [index.html](index.html). It implements "발표 순서 뽑기" (Presentation Order Picker) — a Korean-language utility where a user pastes a list of student names (one per line) into a textarea and clicks a button to generate a randomly shuffled presentation order.

There is no build system, package manager, dependency, server, or test suite. The entire app — markup, CSS, and JS — lives in this one file and runs by opening it directly in a browser.

## Development

- **Run it**: open `index.html` directly in a browser (double-click, or `file://` URL). No server or build step is needed.
- **Edit it**: all styles are in the `<style>` block and all logic is in the inline `<script>` block at the bottom of the file. Since everything is in one file, changes are visible on a simple browser refresh.
- There is no linter, formatter, or test runner configured for this project.

## Architecture

The script (bottom of `index.html`) is a single IIFE with three pure/DOM functions wired to one click handler:

- `parseNames(text)` — splits textarea input on newlines, trims, and drops blank lines.
- `shuffle(arr)` — Fisher-Yates shuffle, returns a new array (does not mutate input).
- `renderOrder(names)` — rebuilds the `#orderList` `<ol>` from scratch given an ordered name array; shows an empty-state message when the list is empty.
- `drawOrder()` — the click handler for `#drawBtn`: reads `#nameInput`, parses, shuffles, and renders.

All state is transient and derived directly from the textarea's current value at click time — there is no persisted state, storage, or data model beyond the DOM itself.
