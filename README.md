# snatchsoul
helping those teenagers who has friendship issue and mental health
def record_mood():
    """Allows the user to record their mood and a journal entry."""
    date_str = datetime.date.today().strftime("%Y%m%d")
    print("\n--- Mood Journal ---")
    mood = input("On a scale of 1-5 (1=bad, 5=great), how are you feeling today? ")
    entry = input("Write about your day or how you're feeling (press Enter twice to finish):\n")
    
    with open(MOOD_JOURNAL_FILE, "a") as f:
        f.write(f"Date: {date_str}\n")
        f.write(f"Mood: {mood}\n")
        f.write(f"Entry: {entry.strip()}\n")
        f.write("-" * 30 + "\n")
    print("Your mood and entry have been saved.")

def view_mood_history():
    """Displays past mood journal entries."""
    print("\n--- Mood History ---")
    try:
        with open(MOOD_JOURNAL_FILE, "r") as f:
            content = f.read()
            if not content:
                print("No entries yet. Start by recording your mood!")
            else:
                print(content)
    except FileNotFoundError:
        print("No mood journal entries found. Start by recording your mood!")

# --- Functions for Coping Tools ---
def coping_tools():
    """Offers various coping mechanisms."""
    print("\n--- Coping Tools ---")
    print("1. Guided Breathing Exercise")
    print("2. Quick Self-Care Ideas")
    choice = input("Choose a coping tool (1 or 2): ")

    if choice == '1':
        print("\n--- Guided Breathing Exercise ---")
        print("Let's do a simple square breathing exercise.")
        print("Inhale slowly for 4 seconds...")
        import time; time.sleep(4)
        print("Hold your breath for 4 seconds...")
        time.sleep(4)
        print("Exhale slowly for 4 seconds...")
        time.sleep(4)
        print("Hold your breath for 4 seconds...")
        time.sleep(4)
        print("Repeat if you like. Focus on your breath.")
    elif choice == '2':
        ideas = [
            "Listen to your favorite music.",
            "Take a short walk outside.",
            "Draw or doodle something.",
            "Spend 5 minutes stretching.",
            "Drink a glass of water.",
            "Talk to a trusted friend or family member.",
            "Watch a funny video."
        ]
        print("\n--- Quick Self-Care Idea ---")
        print(random.choice(ideas))
    else:
        print("Invalid choice.")

# --- Functions for Friendship Tips ---
def friendship_tips():
    """Provides advice on friendship scenarios."""
    print("\n--- Friendship Tips ---")
    print("1. Dealing with Arguments")
    print("2. Making New Friends")
    print("3. Setting Boundaries")
    choice = input("What kind of advice are you looking for (1-3)? ")

    if choice == '1':
        print("\n--- Dealing with Arguments ---")
        print("Try to understand their side: Listen actively without interrupting.")
        print("Use 'I' statements: 'I feel hurt when...' instead of 'You always...'")
        print("Suggest a break: If emotions are high, agree to talk later.")
        print("Be willing to compromise: Friendships involve give and take.")
    elif choice == '2':
        print("\n--- Making New Friends ---")
        print("Join clubs or activities you enjoy: You'll meet people with similar interests.")
        print("Be open and friendly: Smile and make eye contact.")
        print("Ask questions and listen: Show genuine interest in others.")
        print("Start small: A simple 'hi' or compliment can go a long way.")
    elif choice == '3':
        print("\n--- Setting Boundaries ---")
        print("Know your limits: What are you comfortable with and not?")
        print("Communicate clearly: Say 'no' kindly but firmly when needed.")
        print("Be consistent: Stick to your boundaries.")
        print("Boundaries protect your well-being and make friendships healthier.")
    else:
        print("Invalid choice.")

# --- Functions for Helpful Resources ---
def helpful_resources():
    """Provides crucial information for professional help."""
    print("\n--- Helpful Resources ---")
    print("If you are feeling overwhelmed or need immediate support, please reach out.")
    print("Remember, you are not alone, and help is available.")
    print("\nCrisis Hotlines:")
    print("  Befrienders Malaysia: 03-76272929 (24-hour, daily)") # Example for Malaysia
    print("  (Please search for local crisis hotlines in your area if outside Malaysia.)")
    print("\nRecommended Websites for Support:")
    print("  Mental Health Association of Malaysia (MHAM): https://mham.org.my/")
    print("  (Explore reputable mental health organizations for resources.)")
    print("\nAlways remember to speak to a trusted adult, parent, teacher, or counselor if you are struggling.")

# --- Functions for Small Goals ---
def add_goal():
    """Allows the user to add a new small goal."""
    print("\n--- Add a New Goal ---")
    goal = input("What small goal would you like to set for your well-being or friendships? ")
    with open(GOALS_FILE, "a") as f:
        f.write(f"UNCOMPLETED: {goal}\n")
    print("Goal added! Keep working towards it.")

def view_goals():
    """Displays current goals and allows marking them as completed."""
    print("\n--- Your Goals ---")
    try:
        with open(GOALS_FILE, "r") as f:
            lines = f.readlines()
            if not lines:
                print("No goals set yet. Time to add one!")
                return

            for i, line in enumerate(lines):
                print(f"{i+1}. {line.strip()}")

            while True:
                action = input("Enter the number of a goal to mark as COMPLETED, or 'b' to go back: ").lower()
                if action == 'b':
                    break
                try:
                    goal_index = int(action) - 1
                    if 0 <= goal_index < len(lines):
                        if "UNCOMPLETED" in lines[goal_index]:
                            lines[goal_index] = lines[goal_index].replace("UNCOMPLETED", "COMPLETED")
                            with open(GOALS_FILE, "w") as fw:
                                fw.writelines(lines)
                            print(f"Goal '{lines[goal_index].strip().replace('COMPLETED: ', '')}' marked as completed!")
                            # Redisplay updated goals
                            print("\n--- Your Goals (Updated) ---")
                            for i, line in enumerate(lines):
                                print(f"{i+1}. {line.strip()}")
                        else:
                            print("This goal is already completed.")
                    else:
                        print("Invalid goal number.")
                except ValueError:
                    print("Invalid input. Please enter a number or 'b'.")

    except FileNotFoundError:
        print("No goals found. Start by adding a goal!")

# --- Main Program Loop ---
def main_menu():
    """Displays the main menu and handles user choices."""
    while True:
        print("\n===== Teen Well-being Support Program =====")
        print("1. Mood Journal")
        print("2. Coping Tools")
        print("3. Friendship Tips")
        print("4. Helpful Resources")
        print("5. Set & Track Goals")
        print("6. Exit")

        choice = input("What would you like to do today? ")

        if choice == '1':
            print("\n--- Mood Journal Options ---")
            print("1. Record Today's Mood")
            print("2. View Mood History")
            journal_choice = input("Choose an option (1 or 2): ")
            if journal_choice == '1':
                record_mood()
            elif journal_choice == '2':
                view_mood_history()
            else:
                print("Invalid choice.")
        elif choice == '2':
            coping_tools()
        elif choice == '3':
            friendship_tips()
        elif choice == '4':
            helpful_resources()
        elif choice == '5':
            print("\n--- Goals Options ---")
            print("1. Add New Goal")
            print("2. View/Mark Goals")
            goal_choice = input("Choose an option (1 or 2): ")
            if goal_choice == '1':
                add_goal()
            elif goal_choice == '2':
                view_goals()
            else:
                print("Invalid choice.")
        elif choice == '6':
            print("Thanks for using the program! Take care.")
            break
        else:
            print("Invalid choice. Please select a number from 1 to 6.")

# Run the main program
if __name__ == "__main__":
    main_menu()
