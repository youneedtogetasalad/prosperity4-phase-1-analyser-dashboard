# Prosperity 4 Log Analyzer Guide

This guide explains how to use the Prosperity 4 log analyzer tools to track algorithm performance, calculate ELO ratings, and analyze backtest/competition results.

## Overview

There are two analyzer tools available:

1. **log_analyzer.html** - Basic single-log analyzer with ELO calculation
2. **log_analyzer_elo.html** - Advanced ELO tracker with leaderboard and version comparison

Both tools work entirely in your browser - no server required!

---

## Quick Start

### Opening the Analyzers

1. Open your file browser and navigate to `C:\Users\hinyi\PycharmProjects\Prosperity4\`
2. Double-click either `log_analyzer.html` or `log_analyzer_elo.html`
3. The file will open in your default web browser

---

## log_analyzer.html - Basic Analyzer

### Features

- **Performance Summary**: Displays profit, round info, and final positions
- **ELO Rating**: Chess-style rating based on profit performance
- **Key Insights**: Auto-generated analysis of your results
- **Time-Based Analysis**: Early/Mid/Late game performance breakdown (if graph data available)
- **AI-Ready Summary**: Formatted text for copying to Claude

### Supported File Formats

- `.json` - Competition result files
- `.log` - Text log files with profit data

### How to Use

1. **Upload a Log File**
   - Drag and drop a file onto the upload area, OR
   - Click the upload area to browse for a file

2. **View Results**
   - The analyzer will automatically process your file
   - Results appear in sections below the upload area

3. **Copy Summary to Claude**
   - Scroll to "AI-Ready Summary" section
   - Click "Copy Summary to Clipboard" button
   - Paste directly into your Claude conversation

### Understanding the Output

| Section | Description |
|---------|-------------|
| **Performance Summary** | Key metrics including profit, rating, and positions |
| **ELO Rating** | Chess-style rating (1500 = baseline, higher = better) |
| **Key Insights** | Color-coded tags highlighting important findings |
| **Detailed Analysis** | Performance breakdown with time-based patterns |
| **AI-Ready Summary** | Formatted text for sharing with Claude |

### Performance Ratings

| Rating | Profit Range | Tier |
|--------|-------------|------|
| EXCELLENT 🌟 | 10000+ | Grandmaster |
| VERY GOOD ✅ | 8000-9999 | Master |
| GOOD 👍 | 6000-7999 | Diamond |
| MEDIUM 😐 | 4000-5999 | Platinum |
| FAIR 😕 | 2000-3999 | Gold |
| POOR 💔 | < 2000 | Silver |

---

## log_analyzer_elo.html - ELO Tracker

### Features

- **Algorithm Leaderboard**: Ranks all versions by ELO rating
- **Match Predictor**: Head-to-head win probability between top versions
- **Version History**: Track all submitted versions over time
- **ELO Tracking**: Automatic ELO updates when comparing versions
- **Claude Summary Generator**: Create summaries from stored data
- **Import/Export**: Save and restore your algorithm database

### How to Use

#### 1. Upload Your First Log

```
1. Open log_analyzer_elo.html in your browser
2. Drag & drop a competition log file (JSON or LOG format)
3. Optionally enter a version name (e.g., "v5_final") in the text field
4. Click "Upload Competition Log"
```

#### 2. View the Leaderboard

- **Rank**: Position in your version roster (1 = best)
- **Version Name**: Name you assigned (or filename)
- **ELO Rating**: Chess-style rating (higher = better)
- **ELO Change**: Recent change (+ or -)
- **Win Rate**: W-L record with percentage

#### 3. Compare Versions

Each new upload is automatically compared against all previous versions:
- Higher profit → ELO increases
- Lower profit → ELO decreases
- Win/loss record updates automatically

#### 4. Generate a Claude Summary

**From uploaded log:**
1. Upload a log file
2. Scroll to "Send to Claude" section
3. Click "Copy Claude Summary"
4. Paste into Claude

**From stored data:**
1. Find "Generate Claude Summary" section
2. Select version from dropdown
3. Click "Generate Claude Summary"
4. Click "Copy Summary" button

#### 5. Manage Your Data

**Export your data:**
1. Open browser developer tools (F12)
2. Go to Console tab
3. Type: `copy(localStorage.getItem('prosperity_algorithms'))`
4. Paste into a text file and save as JSON

**Import data:**
1. Click "Import Saved Data" button
2. Select your exported JSON file
3. Data merges with existing entries

**Clear all data:**
1. Click "Clear All Data" button
2. Confirm the dialog

---

## ELO Rating System

The ELO system works like chess ratings:

| Concept | Description |
|---------|-------------|
| **Base ELO** | 1500 (starting rating for new versions) |
| **K-Factor** | 32 (how much ratings change per match) |
| **Win Condition** | Higher profit = win |
| **Expected Score** | Calculated from rating difference |

### Example ELO Changes

| Scenario | ELO Change |
|----------|------------|
| Beat higher-rated version | +20 to +50 |
| Beat lower-rated version | +5 to +20 |
| Lose to higher-rated version | -5 to -20 |
| Lose to lower-rated version | -20 to -50 |

---

## Best Practices

### Naming Versions

Use consistent, descriptive names:
- ✅ Good: `v5_final`, `v19_maf`, `v21_ultimate`
- ❌ Bad: `test`, `final_v2`, `my_algo`

### Workflow Suggestion

1. Run backtest with new version
2. Upload result to ELO tracker
3. Copy Claude summary
4. Paste to Claude for analysis
5. Iterate based on insights

### Reading the Ratings

**ELO vs Profit:**
- ELO measures consistency across matchups
- Profit measures absolute performance
- A version with 8500 profit could have lower ELO than one with 8200 if it loses more matchups

**Time-Based Analysis:**
- Early game strength: Good opening strategy
- Mid game strength: Consistent performance
- Late game weakness: May need better EOD closing

---

## Troubleshooting

### File Won't Upload

- Check file is `.json` or `.log` format
- Ensure file isn't corrupted
- Try a different browser

### ELO Seems Wrong

- ELO is relative - first version starts at 1500
- Need 3+ versions for stable ratings
- Clear data and re-upload if needed

### Clipboard Copy Fails

- Check browser permissions
- Try manual copy: Select text → Ctrl+C
- Use Firefox or Chrome for best compatibility

### Data Not Saving

- Check browser's localStorage is enabled
- Don't use Incognito/Private mode
- Export data regularly as backup

---

## Tips for Competition Analysis

### What to Look For

1. **Profit Trend**: Is each version improving?
2. **ELO Movement**: Consistent gains = robust strategy
3. **Position Cleanliness**: Zero positions at end = good EOD
4. **Time Patterns**: Late-game drop? Add EOD close

### Generating Insights for Claude

Copy this template along with your summary:

```
Here's my latest Prosperity 4 backtest result. Please:
1. Compare with previous versions
2. Identify strengths/weaknesses
3. Suggest specific improvements
4. Recommend next iteration strategy

[PASTE SUMMARY HERE]
```

---

## File Locations

```
C:\Users\hinyi\PycharmProjects\Prosperity4\
├── log_analyzer.html          # Basic analyzer
├── log_analyzer_elo.html      # ELO tracker (recommended)
├── v12_*.py                   # Your algorithm versions
├── v13_*.py
├── ...                        # More versions
└── round2_data/               # Test data (if present)
```

---

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Open file | Ctrl+O (in browser file dialog) |
| Copy | Ctrl+C (after selecting text) |
| Paste | Ctrl+V |
| Developer tools | F12 (for export) |

---

## Summary: Which Analyzer Should I Use?

| Use Case | Recommended Tool |
|----------|-----------------|
| Quick single-log analysis | log_analyzer.html |
| Track multiple versions | log_analyzer_elo.html |
| Compare algorithm performance | log_analyzer_elo.html |
| Generate summaries for Claude | Either (both work) |
| Long-term project tracking | log_analyzer_elo.html |

---

## Need Help?

If something isn't working:

1. Check browser console for errors (F12 → Console)
2. Ensure you're using a modern browser (Chrome/Firefox/Edge)
3. Try clearing browser cache
4. Verify your log file format matches expected structure

---

## Version History

- **v1.0** - Initial release with basic analysis
- **v2.0** - Added ELO tracking system
- **v2.1** - Added leaderboard and match predictor
- **v2.2** - Added Claude summary generation from stored data

---

*Last Updated: Round 2 Development Period*
