# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a simple static web application that helps Canadian Flesh and Blood (FAB) card game players search for singles across multiple Canadian retailers. The app is hosted on GitHub Pages.

**Key Features:**
- Store selection interface with checkboxes
- Bulk search across selected retailers
- Custom Chrome search engine support via query parameters (`?q=cardname`)
- No build process or dependencies—pure HTML/CSS/JavaScript

## Project Structure

- `index.html` - Single-file application containing all HTML, CSS, and JavaScript
- `README.md` - Documentation of supported stores
- `list.md` - Research/notes file with additional store URLs

## Common Development Tasks

### Deploying changes
The app is deployed to GitHub Pages at `http://alexgirarddev.github.io/fab_card_search`. Changes to `index.html` are automatically deployed when pushed to the `main` branch.

### Adding a new store
Stores are defined in the `stores` JavaScript object in `index.html` (around line 59). Add a new store object with `name` and `url` properties to the appropriate section (GameStores or TCGPlayer). The URL must include `{cardName}` placeholder which gets replaced with the encoded search term.

Example:
```javascript
{ name: "Store Name", url: "https://store.com/search?q={cardName}" }
```

### Testing search functionality
The app supports query parameters for testing. Use `?q=cardname` to auto-populate the search field and trigger immediate search with default stores.

Example: `http://alexgirarddev.github.io/fab_card_search?q=Bolt`

## Key Implementation Details

**Store URL Structure:**
- URLs use template placeholders `{cardName}` that are replaced with `encodeURIComponent()` values at runtime
- Each retailer has different URL structures; test custom search URLs in the browser before adding them

**Search Flow:**
1. User enters card name and/or selects stores
2. `openTabs()` function (line 132) is called
3. For each selected store, the URL template is filled with the encoded card name
4. Each URL opens in a new browser tab

**Store Sections:**
- Stores are grouped into sections (GameStores, TCGPlayer) in the stores object
- Each section gets select/deselect buttons automatically
- First section stores are checked by default on page load
