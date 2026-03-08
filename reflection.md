# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
  - The first time I ran it, it looked like a fun game of just guessing a random number.
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  - My first guess was 12 and the game told me to go lower. My next guess was 2 and it told me to      go lower again. I picked 1 and it still said go lower. For a game to say 1 - 100 and I still       had to go lower, there was something wrong. After using all of my guesses, the correct number      was 72. I thought I would've struck gold guessing 1 after it told me to go lower on 2 but the      game was broken.
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
  - Copilot, Claude, & ChatGPT
    
- Give one example of an AI suggestion that was correct (including what the AI suggested and how     you verified the result).
  - Claude correctly identified that the hints in `check_guess` were swapped — when the guess was      too high it said "Go HIGHER!" and when too low it said "Go LOWER!", which is the opposite of       what it should do. I verified this by playing the game myself (guessing 3, 2, and 1 all            returned "Go LOWER!") and then by running pytest with `test_too_high_hint_direction` and           `test_too_low_hint_direction`, which both passed after the fix.
    
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  - Claude initially edited files in the OneDrive path of the project, but the Streamlit app was       running from a separate local Documents copy of the folder. This meant the fixes appeared to       work (the code looked correct) but the running game still showed the old broken behavior. I        had to manually copy the fixed files to the correct folder before the game actually worked.
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  - Once both the automated tests passed and the live game played correctly.
    
- Describe at least one test you ran (manual or using pytest) and what it showed you about your      code.
  - For the hint direction bug, I ran `pytest tests/ -v` which showed all 5 tests passing,             including the two new tests I added specifically for that fix. I also played the game manually     after the fix, guessing a low number like 3 correctly showed "Go HIGHER!" instead of the wrong     "Go LOWER!".
    
- Did AI help you design or understand any tests? How?
  - Claude helped me design the tests by suggesting I write a focused test with a specific example     (guess 60, secret 50) rather than testing every possible case.
---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
  - The secret sat atop the code here intially. "st.session_state.secret = random.randint(low,         high)"
- How would you explain Streamlit "reruns" and session state to a friend who has never used          Streamlit?
  - Sessiom state is Streamlit's way of storing values that survive across reruns. I would ask         them to think of it as a notepad hat it keeps betweeen refreshes. 
- What change did you make that finally gave the game a stable secret number?
  - The fix was to only generare the secret if one doesn't already exist in session state: if          "secret" not in st.session_state:
    st.session_state.secret = random.randint(low, high)

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
    - I think I followed a pretty solid prompting strategy. I was very specific in what I was            looking for in communicating with Claude and have found myself to lean on it more over ChatGPT     as I use it. 
- What is one thing you would do differently next time you work with AI on a coding task?
  - Claude worked pretty well but going forward I'll probably use two AI's to confirm what I have      is correct and ensure all changes are documented.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  - I realized AI can write code that looks completely reasonable and still be wrong. The hint bug     wasn't obvious from reading the code and I had to run the game and try low numbers to notice       it was giving the wrong direction.
