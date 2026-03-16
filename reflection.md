# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

  The hints were wrong (didn't properly compare the input with the secret number). I expect the game to tell me to Go HIGHER when my guess is too low and Go LOWER when my guess is to high, but it hints to go in the wrong direction, further from the secret. 
  
  The game didn't check the guesses/inputs were in the appropriate range. I expected the game to only accept integers in the range of 1-50 for normal, 1-100 for hard, and 1-20 for easy, but it accepted numbers out of the respective ranges as well. 

  The number of guesses attempted doesn't reset between games, so a new game isn't possible without restarting the app since you start a new game with guesses already used up. I expected the attempts to reset between games.

  I also changed the number of guesses associated with each difficulty. 

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

I used GitHub Copilot as my primary AI tool for this project. It helped with code suggestions, debugging, and understanding Streamlit concepts.

One correct suggestion was when Copilot helped fix the inverted hint logic in the check_guess function. It suggested swapping the "Go LOWER" and "Go HIGHER" messages to match the correct outcomes. I verified this by running the tests in test_game_logic.py, which passed after the change, and manually testing the app to ensure hints now pointed in the right direction.

An incorrect suggestion occurred when Copilot proposed a way to reset attempts on new game that didn't account for session state properly. It suggested simply setting attempts to 0 without ensuring it was stored in st.session_state. I verified this was wrong by running the app and seeing that attempts still carried over between games, so I had to correct it by properly updating the session state.

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided a bug was fixed by running both automated tests and manual testing in the Streamlit app. If the tests passed and the app behaved correctly during gameplay, I considered it fixed.

One test I ran was the pytest suite in tests/test_game_logic.py, which included tests for parse_guess and check_guess functions. For example, the test_parse_guess_too_large test showed that inputs outside the range were properly rejected, confirming the range validation was working. This helped me see that the logic was correctly implemented without allowing invalid guesses.

AI (Copilot) helped me understand and design some tests by suggesting test cases for edge cases, like testing decimal inputs or None values in parse_guess. It provided code snippets for assertions, which I adapted to fit the existing test structure.

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

The secret number kept changing because it was generated anew on every rerun of the app without being stored persistently. Each time the user interacted, Streamlit reran the script, and since there was no session state, a new random number was picked each time.

I'd explain Streamlit reruns to a friend like this: Every time you click a button or enter something, Streamlit runs your entire Python script from top to bottom again, like refreshing a webpage but for your app. Session state is like a persistent storage box that remembers values between these reruns, so things like scores or secrets don't get reset unless you want them to.

The change I made was initializing and storing the secret number in st.session_state if it wasn't already there, ensuring it persists across reruns until a new game is started.

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse is writing and running automated tests early and often, especially for logic functions like parse_guess and check_guess, to catch bugs before manual testing.

Next time, I would verify AI suggestions more thoroughly by running tests immediately after implementing them, rather than assuming they're correct.

This project showed me that AI-generated code can be a great starting point but often needs careful review and testing, as it might miss edge cases or misunderstand requirements, making me more critical and hands-on in the development process.
