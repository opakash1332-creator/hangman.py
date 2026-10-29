import random

def play_hangman():
    # Words ki list (Testing ke liye secret word 'python' fixed kiya gaya hai)
    word_list = ['python', 'developer', 'programming', 'computer']
    secret_word = 'python' # Fixed word for testing
    
    # Trackers
    guessed_letters = set()
    wrong_guesses_count = 0
    max_wrong_guesses = 6

    print("--- Hangman Game ---")

    while wrong_guesses_count < max_wrong_guesses:
        # User se input lein
        user_input = input("\nEnter a guess: ").strip()

        # Input Validation: sirf single letter (a-z, A-Z) allowed hai
        if len(user_input) != 1 or not user_input.isalpha():
            print("Invalid input: Enter a single letter")
            continue

        guess = user_input.lower()

        # Duplicate Guess Validation (no attempt lost)
        if guess in guessed_letters:
            print(f"You already guessed '{guess}'. Try another letter (no attempt lost)")
            continue

        # Guessed letter ko add karein
        guessed_letters.add(guess)

        # Guess check karein
        # Guess check karein
        if guess in secret_word:
            # Underscores aur letters ke beech space add karne ke liye " ".join() use karein
            current_progress = " ".join([letter if letter in guessed_letters else "_" for letter in secret_word])
            print(f"Progress {current_progress}")
            print(f"{guess}: Correct")
            
            # Agar poora word guess ho gaya
            if "_" not in current_progress:
                print("You won! The word was " + secret_word)
                print(f"Wrong guesses: {wrong_guesses_count}/{max_wrong_guesses}")
                break
        else:
            wrong_guesses_count += 1
            print(f"Wrong guess ({wrong_guesses_count}/{max_wrong_guesses})")

            # Agar max wrong guesses poore ho gaye
            if wrong_guesses_count == max_wrong_guesses:
                print("Game Over! The word was " + secret_word)
                break

if __name__ == "__main__":
    play_hangman()
