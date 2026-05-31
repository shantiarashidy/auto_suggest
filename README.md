# Smart Auto-Suggest for Persian Search

An intelligent auto-suggestion system for Persian text inputs, capable of handling typos, keyboard layout mistakes (English typed instead of Persian), and partial queries — built for real-world search experiences.

## Problem Statement

When users type in a search box, traditional auto-suggestions only match strings that start with the typed query. This project goes further by:

- Correcting **common typos**
- Detecting when the user typed in **English** (e.g., `fhfg` → `زاهدان`)
- Suggesting both **Persian and English** city names
- Learning from **real user search behavior**

The model is trained on actual search logs and suggests the most likely destinations a user intends.

## Dataset

- `mrbilit_search.json` – Training data with:
  - `ServiceType` (bus, taxi, flight, hotel, etc.)
  - `TypedStrings` – sequence of user inputs over time
  - `AcceptString` – what the user finally selected

- `test_data.json` – Test queries (just the typed string)

- `iran_cities.csv` – List of Iranian cities (Persian & English names)

- `typo_char.csv` – Mapping between English and Persian keyboard layouts

## Approach

The solution combines:

1. **History-based matching** – If the exact typed string has been seen before, suggest the most frequently chosen cities.

2. **Keyboard layout correction** – Converts English characters to Persian based on the standard keyboard mapping.

3. **Prefix matching** – Falls back to cities starting with the corrected query.

4. **Popularity fallback** – If nothing matches, suggest the top 5 most frequently selected cities overall.
