# Playlist Chaos

Your AI assistant tried to build a smart playlist generator. The app runs, but some of the behavior is unpredictable. Your task is to explore the app, investigate the code, and use an AI assistant to debug and improve it.

This activity is your first chance to practice AI-assisted debugging on a codebase that is slightly messy, slightly mysterious, and intentionally imperfect.

You do not need to understand everything at once. Approach the app as a curious investigator, work with an AI assistant to explain what you find, and make targeted improvements.

---

## How the code is organized

### `app.py`  

The Streamlit user interface. It handles things like:

- Showing and updating the mood profile  
- Adding songs  
- Displaying playlists  
- Lucky pick  
- Stats and history

### `playlist_logic.py`  

The logic behind the app, including:

- Normalizing and classifying songs  
- Building playlists  
- Merging playlist data  
- Searching  
- Computing statistics  
- Lucky pick mechanics

You will need to look at both files to understand how the app behaves.

---

## What you will do

### 1. Explore the app  

Run the app and try things out:

- Add several songs with different titles, artists, genres, and energy levels  
- Change the mood profile  
- Use the search box  
- Try the lucky pick  
- Inspect the playlist tabs and stats  
- Look at the history  

As you explore, write down at least five things that feel confusing, inconsistent, or strange. These might be bugs, quirks, or unexpected design decisions.

### 2. Ask AI for help understanding the code  

Pick one issue from your list. Use an AI coding assistant to:

- Explain the relevant code sections  
- Walk through what the code is supposed to do  
- Suggest reasons the behavior might not match expectations  

For example:

> "Here is the function that classifies songs. The app is mislabeling some songs. Help me understand what the function is doing and where the logic might need adjustment."

Before making changes, summarize in your own words what you think is happening.

### 3. Fix at least four issues  

Make improvements based on your investigation.

For each fix:

- Identify the source of the issue  
- Decide whether to accept or adjust the AI assistant's suggestions  
- Update the code  
- Add a short comment describing the fix  

Your fixes may involve logic, calculations, search behavior, playlist grouping, lucky pick behavior, or anything else you discover.

### 4. Test your changes  

After each fix, try interacting with the app again:

- Add new songs  
- Change the profile  
- Try search and stats  
- Check whether playlists behave more consistently  

Confirm that the behavior matches your expectations.

### 5. Optional stretch goals  

If you finish early or want an extra challenge, try one of these:

- Improve search behavior  
- Add a "Recently added" view  
- Add sorting controls  
- Improve how Mixed songs are handled  
- Add new features to the history view  
- Introduce better error handling for empty playlists  
- Add a new playlist category of your own design  

---

## Tips for success

- You do not need to solve everything. Focus on exploring and learning.  
- When confused, ask an AI assistant to explain the code or summarize behavior.  
- Test the app often. Small experiments reveal useful clues.  
- Treat surprising behavior as something worth investigating.  
- Stay curious. The unpredictability is intentional and part of the experience.

When you finish, Playlist Chaos will feel more predictable, and you will have taken your first steps into AI-assisted debugging.

---

## Changes Made to the Code

### Bug Fixes

#### 1. Fixed `hype_ratio` calculation in `compute_playlist_stats`
- **Location**: `playlist_logic.py`, line ~121
- **Issue**: The ratio was calculated as `len(hype) / len(hype)`, always returning 1.0 or 0.0
- **Fix**: Changed to `len(hype) / len(all_songs)` to calculate the actual proportion of hype songs
- **Impact**: The hype ratio now correctly shows what percentage of all songs are classified as hype

#### 2. Fixed `avg_energy` calculation in `compute_playlist_stats`
- **Location**: `playlist_logic.py`, line ~127
- **Issue**: Summed energy from only hype songs but divided by total song count, mixing two different populations
- **Fix**: Changed to sum energy from all songs: `sum(song.get("energy", 0) for song in all_songs)`
- **Impact**: Average energy now correctly represents the average across the entire playlist

### Refactoring

#### 3. Refactored `classify_song` function for readability
- **Location**: `playlist_logic.py`, lines 62-90
- **Changes**:
  - Renamed `is_hype_keyword` → `has_hype_genre_keyword` (clarifies it checks genre field)
  - Renamed `is_chill_keyword` → `has_chill_title_keyword` (clarifies it checks title field)
  - Extracted inline comparisons into named boolean variables:
    - `is_favorite_genre = genre == favorite_genre`
    - `is_high_energy = energy >= hype_min_energy`
    - `is_low_energy = energy <= chill_max_energy`
  - Added explanatory comments for classification logic
- **Impact**: No functional changes, but code is now more self-documenting and easier to understand

---

## Summary

The core concept students need to understand is that debugging involves investigating code behavior and using AI as a collaborator instead of an all knowing oracle. Students are most likely to struggle with distinguishing real bugs from code that does work, but may look confusing. They may also struggle with critically evaluating AI suggestions instead of simply accepting them. AI assistants can be helpful for explaining what code does and identifying math errors, but can be misleading by suggesting fixes for code that's already working as designed. That could lead to unintended changes. When guiding students, it would be helpful to ask them to trace through examples manually and explain what they expect to happen versus what actually happens, and encourage them to verify AI suggestions through testing rather than automatically trusting them. This  builds debugging skills and helps with critical thinking about AI development.
