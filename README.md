# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- **Game's Purpose:** This is a number guessing game built with Streamlit where players try to guess a secret number within a range determined by difficulty level (Easy: 1-20, Normal: 1-50, Hard: 1-100). The game provides hints ("Go HIGHER" or "Go LOWER"), tracks attempts, awards scores based on performance, and includes features like new game resets and developer debug info.

- **Bugs Found:** 
  - Hints were inverted: "Go LOWER" when guess was too low and "Go HIGHER" when too high.
  - No range validation: Accepted guesses outside the difficulty's number range.
  - Attempts didn't reset on new game: Session state wasn't properly updated, causing attempts to carry over.
  - Attempt limits were incorrect for each difficulty.

- **Fixes Applied:** 
  - Corrected hint logic by swapping the messages in check_guess function.
  - Added range checking in parse_guess to reject invalid inputs.
  - Fixed session state handling for attempts and secret number to persist across reruns.
  - Adjusted attempt limits (Easy: 8, Normal: 6, Hard: 5).
  - Refactored parse_guess and check_guess into logic_utils.py for better organization.
  - Expanded tests in test_game_logic.py to cover edge cases and ensure functions work correctly.

## 📸 Demo

- [ ] [Insert a screenshot of your fixed, winning game here]
![alt text](<Screenshot 2026-03-15 at 10.14.17 PM.png>)
## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here]
