# snatchsoul
helping those teenagers who has friendship issue and mental health
import datetime # To get the current date for journal entries
import random   # To pick random self-care ideas
import os       # To check if files exist

# --- File Names for Storing Data ---
# These files will be created in the same folder where you run the Python script.
MOOD_JOURNAL_FILE = "mood_journal.txt"
GOALS_FILE = "goals.txt"

# --- Function 1: Mood Journal ---
def record_mood():
    """Allows the user to record their mood and a short journal entry for the day."""
    current_date = datetime.date.today().strftime("%Y-%m-%d") # Format date like '2025-06-23'
    print("\n--- Mood Journal ---")
    print(f"Today's Date: {current_date}")

    # Loop until valid mood input is given
    while True:
        mood_input = input("On a scale of 1 to 5 (1=feeling really bad, 5=feeling great), how are you feeling today? ")
        if mood_input.isdigit() and 1 <= int(mood_input) <= 5:
            mood = int(mood_input)
            break
        else:
            print("Invalid input. Please enter a number between 1 and 5.")

    print("Now, write a few sentences about your day or what's on your mind regarding friendships or anything else.")
    print("(Press Enter twice to finish your entry)")
    
    lines = []
    while True:
        line = input()
        if not line: # If user presses Enter on an empty line, they're done
            break
        lines.append(line)
    entry = "\n".join(lines)

    # Open the journal file in 'append' mode ('a') so new entries are added to the end
    with open(MOOD_JOURNAL_FILE, "a") as f:
        f.write(f"Date: {current_date}\n")
        f.write(f"Mood: {mood} out of 5\n")
        f.write(f"Entry:\n{entry.strip()}\n") # .strip() removes any leading/trailing whitespace
        f.write("------------------------------------\n") # Separator for entries
    print("Your mood and entry have been saved successfully!")

def view_mood_history():
    """Displays all past mood journal entries."""
    print("\n--- Your Mood History ---")
    if not os.path.exists(MOOD_JOURNAL_FILE) or os.path.getsize(MOOD_JOURNAL_FILE) == 0:
        print("No mood journal entries found yet. Start by recording your mood!")
        return

    try:
        with open(MOOD_JOURNAL_FILE, "r") as f:
            content = f.read()
            print(content)
    except Exception as e:
        print(f"An error occurred while reading the journal: {e}")

# --- Function 2: Coping Tools ---
def coping_tools():
    """Offers simple coping mechanisms and self-care ideas."""
    print("\n--- Coping Tools ---")
    print("Sometimes, a small break or simple activity can help. Choose one:")
    print("1. Try a simple breathing exercise")
    print("2. Get a quick self-care idea")
    print("3. Go back to main menu")

    tool_choice = input("Enter your choice (1, 2, or 3): ")

    if tool_choice == '1':
        print("\n--- Simple Breathing Exercise ---")
        print("Let's try a 4-7-8 breathing exercise. Inhale for 4, hold for 7, exhale for 8.")
        print("Find a comfortable position. Breathe in through your nose, out through your mouth.")
        
        # Using time.sleep to pause the program for a simple guided effect
        import time 
        print("Ready? Breathe in slowly (1...2...3...4)")
        time.sleep(4)
        print("Hold that breath (1...2...3...4...5...6...7)")
        time.sleep(7)
        print("Exhale completely (1...2...3...4...5...6...7...8)")
        time.sleep(8)
        print("You can repeat this a few times if you like. Focus on the sensation of your breath.")
        print("Done. Take a moment to notice how you feel.")

    elif tool_choice == '2':
        self_care_ideas = [
            "Listen to your favorite song or an uplifting playlist.",
            "Take a short walk outside and notice 5 things you can see.",
            "Draw, doodle, or write freely for 10 minutes.",
            "Drink a glass of water slowly.",
            "Stretch your body gently for a few minutes.",
            "Watch
