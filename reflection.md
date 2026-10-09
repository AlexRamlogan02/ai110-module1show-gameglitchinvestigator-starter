# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| A random number higher/lower than the target was input | The hint correctly shows if the guess was lower or higher than the target | If a guess is lower, the hint suggests lower. If it's higher the hint suggests higher| N/A
| New Game was clicked after failure | A new game starts and the user can play again | A new score is generated, but the user cannot play the game| "Game over. Start a new game to try again." |
| The easy difficulty is selected, restricting the game to a range of 1-20| The game generates a number between 1-20| The game generates a number outside of the range | (Easy mode) Secret: 89 |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

I used GitHub Copilot to help me debug my issues. Giving it my bug reproduction log, I instructed it to find where in app.py these bugs occur, and detail in FIXES.md what changes were made and how it fixes the behavior. When I tested the changes end to end and read the FIX log, I realized a bug was only partially fixed about difficulties. I wrote the criticism and gave it to Copilot to fix again. 

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  - I tested the behavior again and read the log in FIXES.md
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  - I did a manual test on selecting the difficulty in the game and analyzing the results. This allowed me to verify if the game difficulty was fixed. 
- Did AI help you design or understand any tests? How?
  - No, I didn't review the automated tests. 

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  - When an app launches, the app will keep a temporary memory of the session. This memory is held when the app starts, and is deleted when the app stops or restarts. This allows the game to remember things that happen while it runs, and remove it when it ends. 

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
    - In every commit, I detail what kind of changes are made (feature, fix, documentation), and shortly summarize what was changed. 
- What is one thing you would do differently next time you work with AI on a coding task?
  - Sometimes I think I can be more detailed when giving AI different tasks. This way, it can make less mistakes when changing code. 
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  - The changes are only as accurate as the instructions given to AI. A human should always test and review AI generated code before accepting it as fact. 
