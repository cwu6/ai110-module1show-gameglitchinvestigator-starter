# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it? 
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  
The first time I ran the game, the guessing logic was not outputting the correct higher/lower hint. When I guessed an answer lower than the secret number, it would tell me to go lower. Same thing happened but with higher number resulting in a higher hint. The hints were backwards and inconsistent. Also, the game would generate a secret number outside the selected difficulty range. When the difficulty was at a smaller range (Easy), it would sometimes still pick a secret number that was outside that range.


**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| Guess 60, secret 50 | It should display "Too High" and "Go LOWER" | The Higher/Lower hints are incorrect | No console output / error |
| Start a new game on a difficulty with a specific range | Secret should be generated within the selected difficulty range | The game used a fixed range of 1 to 100 across all difficulty ranges so the secret number was out of the selected range | No console output / error |
| Secret 91, guessed 92 and 90 | 92 should say "Go LOWER" and 90 should say "Go HIGHER"| Both guesses would output "Go HIGHER" | No console output / error |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

I used Claude as an AI tool to assist me on this project. AI helped me get a depper understanding on the bugs, how to refactor the game logic, and design tests. For example, one correct AI suggestion was to keep the secret number as an integer instead of converting the attempts to a string. For even number guesses, it would convert the number into a string, which led to inconsistent comparisons. I was able to verify the result because before the fix, if I gave a number higher than secret number, it would output "Go HIGHER." But after the fix, I tested it again. The secret number was 91 and when testing a guess of 92, the game correctly output "Go LOWER," and a guess of 90 correctly outputted "Go HIGHER." However, one suggestion I did not accept was to replace the entire logic_utils.py file into a simplified version. I rejected it because the file contained an outline of functions that were already there and replacing unrelated starter code was not neccessary. I verified my version by keeping my original structure and running the test with python3 -m pytest. All three of the test passes. Also, I ran the Streamlist app and made sure the game was outputting the correct behavior.
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided a bug was fixed by checking the test and playing around the actual Streamlit game. After updating the check_guess() function with the corrct higher/lower logic, I ran pytest to make sure that all three tests from test_game_logic passed. Originally, the test stored the entire check_guess() return value in result, but it was changed to separate the outcome and the message so that the tests could correctly check the result. The tests passed and it showed me that the higher/lower logic was working correctly, but I still needed to test the live game because the tests aren't able to catch all bugs, like the secret number changing into a string. So, I then ran streamlist run app.py and manually tested the game. AI helped me understand why the tests initally failed and guided me on how to test the higher/lower outcomes after fixing the bug.
---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

Streamlist reruns the Python code whenever the user interacts with the app, like starting a new game or submitting a guess. Session state allows the app to remmeber important information through the reruns instead of having to reset everything every time. For example, this game uses session state to remmeber the secret number, attempts, and score.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit from this project that I want to reuse in future projects is to test my codde fully. What I mean by this is to test with written test and the actual application instead of just fully relying on the tests passing. I also want to continue making multple commits of a project so I can look back at my reivisons and keep track of everything. One thing I would do differently next time I work with AI on a coding task is to read over the existing code more carefully before I start making my changes. Also to read all of the instructions carefuly before I start anything. This ensures that I am changing the right code and not making unnecessary/incorrect changes. This project changed the way I think about AI generated code because althought AI can help find the problems and suggest solutions, it is sdtill important to review the suggestions and test them. AI is not always correct in its suggestions, but most of the times it gives you a sense of direction at least. AI is like how I would approach asking others for help. I would ask for suggestions and advice instead of asking  for the answer.