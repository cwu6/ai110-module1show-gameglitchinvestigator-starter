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

- [ ] Describe the game's purpose.

The game is a number guessing game where the player selects a difficulty range and tries to guess the randomly generated secret number from that range. The game diaplays higher or lower hints to help the user get closer to that secret number. 

- [ ] Detail which bugs you found.

I found bugs with the higher/lower hints, the secret number not alwas using the selected difficulty range, and the secret number being changed from an integer to a string during some guesses. All these bugs led to the game outputting the incorrect feedback for the user. The higher/lower bug led the user in the wrong direction as the correct message output for higher and lower were switched. The diificulty range bug could cause a game to generate a secret number outside the range of the selected difficulty. Additionally, the integer to string bug caused the game to compare the wrong data types, which lead to incorret comparisons.

- [ ] Explain what fixes you applied.

I corrected the higher/lower comparison logic, so then the game tells the user to go in the correct direction based on their guess. I just switched the output messages since they were flipped. I also changed the code to generate the secret number within the selected difficulty range, low to high. Originally, the game would always generate the secret number from 1 to 100, even when the player selected Easy or Hard. I also kept the secret number as an integer for every guess, so that the game uses the same data type when comparing guesses to the secret number. Originally, for every even number attempt, it would be converted to a string which led to incorrect comparisons. Moreover, I moved the guessing logic into logic_utils.py to seprate the game logic from the Streamlist interface and added tests to verify the guessing outcomes.


## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. User starts a Normal difficulty game 
2. User enters a guess of 40, and the game displays "Go HIGHER!"
3. User enters a guess of 60, and the game displays "Go LOWER!" 
4. User enters a guess of 50, and the game displays "Correct!"
5. Score updates correctly after each guess
6. Game ends after the correct guess

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
# ========================= X passed in 0.XXs =========================
```

================ test session starts ================
platform darwin -- Python 3.14.7, pytest-9.1.1, pluggy-1.6.0
rootdir: /Users/chlxe/ai110-module1show-gameglitchinvestigator-starter-1
plugins: anyio-4.15.1
collected 3 items                                   

tests/test_game_logic.py ...                  [100%]

================= 3 passed in 0.01s =================

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
