def nearest_multiple_of_4(num):
"""Returns the nearest multiple of 4 greater than or equal to the given number.""" return num + (4 - num % 4) if num % 4 != 0 else num

def check_consecutive(numbers):
"""Checks if the given list of numbers is consecutive."""
return all(numbers[i] - numbers[i - 1] == 1 for i in range(1, len(numbers)))


def you_lose():
"""Displays the losing message and exits the game.""" print("\nYOU LOSE!")
print("Better luck next time!") exit()

def player_turn(current_numbers, last_num): """Handles the player's turn.""" print("\nYour Turn.")
 
count = int(input("How many numbers do you want to enter (1-3)? "))


if count < 1 or count > 3:
print("Invalid input. You are disqualified from the game.") you_lose()

new_numbers = [] print("Enter your numbers:") for _ in range(count):
num = int(input("> ")) new_numbers.append(num)

if new_numbers[0] != last_num + 1 or not check_consecutive(new_numbers): print("The numbers are not consecutive or do not follow the sequence.") you_lose()

current_numbers.extend(new_numbers) return current_numbers

def computer_turn(current_numbers, last_num): """Handles the computer's turn.""" comp_count = 4 - (len(current_numbers) % 4)
comp_numbers = [last_num + i for i in range(1, comp_count + 1)] current_numbers.extend(comp_numbers)
print("\nComputer's Turn:") print("Computer chose:", comp_numbers) print("Numbers so far:", current_numbers)

if current_numbers[-1] >= 21:
 
print("\nCONGRATULATIONS! YOU WON!")
exit()
return current_numbers


def start_game():
"""Starts the 21 Number Game.""" print("Welcome to the 21 Number Game!") print("Rules:")
print("1. You can choose 1, 2, or 3 numbers in your turn.") print("2. The numbers must be consecutive.")
print("3. Whoever says 21 loses the game.\n")


current_numbers = [] last_num = 0

print("Do you want to go first or second? (F/S)") turn = input("> ").strip().upper()

if turn not in ["F", "S"]:
print("Invalid choice. Restart the game.") return

while True:
if turn == "F":
current_numbers = player_turn(current_numbers, last_num) last_num = current_numbers[-1]
if last_num >= 21: you_lose()
current_numbers = computer_turn(current_numbers, last_num)
 
last_num = current_numbers[-1] else:
current_numbers = computer_turn(current_numbers, last_num) last_num = current_numbers[-1]
if last_num >= 21: you_lose()
current_numbers = player_turn(current_numbers, last_num) last_num = current_numbers[-1]

# Run the game
if  name	== " main ": start_game()
