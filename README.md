# Adventure-Game
"""
Sanyerlis Camacaro - CSC235 - Sancamac@uat.edu Assignment:
Creating and using Functions in Python.

"Adventure Game"

This code demonstrates how to:
Create a new console project.
 Create a Simulation. Look at the link above to see Interactive Fiction Simulations.
Your program must do something and be an interactive fiction game, it must not just demo functions.
Add at least 5 functions to your application in addition to the main.
Add at least one function which takes an argument.
Add at least one function which returns a value.
Your main function should control all the other functions.

The Game functions demonstrates:

- `start_game` is the main function that starts and controls the game.
- `hall`, `kitchen`, `library`, `garden` and `basement` are functions for different game scenarios.
They all take a game state as an argument and return an updated game state. This way, they can affect the game
and pass on the results of their actions.
- `if __name__ == "__main__":` is a special construct that checks if the script is being run directly. If it is,
it starts the game by calling the `start_game` function.

Each scenario function prints out a description of the current location and asks for input. Depending on the input
,the function may change the game state (for example, change the location or set `has_treasure` to `True`).
"""


def start_game():
    """
    The main function that starts the game. It uses other functions to control the flow of the game.
    """
    print("****** Welcome to the Adventure Game! ******")
    print("\nYour goal is to find the treasure.")
    print("\nIn this game, your goal is to find the hidden treasure.")
    print("\nYou will navigate through different rooms, each with its own options for actions.")
    print("\nThe game starts in a hall with doors leading to different rooms.")
    print("\nEach room is an opportunity to find where the treasure might be hidden,")
    print("or return to the hall.")
    print("\nTo make a choice, simply type your desired action when prompted.")
    print("\nAre you ready? Let's start the adventure!")

    # Setting initial game state
    game_state = {
        "location": "hall",
        "has_treasure": False
    }

    # Game loop
    while not game_state["has_treasure"]:
        if game_state["location"] == "hall":
            game_state = hall(game_state)
        elif game_state["location"] == "kitchen":
            game_state = kitchen(game_state)
        elif game_state["location"] == "library":
            game_state = library(game_state)
        elif game_state["location"] == "garden":
            game_state = garden(game_state)
        elif game_state["location"] == "basement":
            game_state = basement(game_state)

    print("Congratulations, you've found the treasure and won the game!")


def hall(game_state):
    """
    Function for the hall scenario. The player can go enter different doors.
    """
    print("\nYou're in the hall. There are four doors. These doors leads to the kitchen, library, garden and basement.")
    choice = input("Where do you want to go? (kitchen/library/garden/basement) ")

    if choice == "kitchen":
        game_state["location"] = "kitchen"
    elif choice == "library":
        game_state["location"] = "library"
    elif choice == "garden":
        game_state["location"] = "garden"
    elif choice == "basement":
        game_state["location"] = "basement"

    return game_state


def kitchen(game_state):
    """
    Function for the kitchen scenario. The player can return to the hall or open the fridge.
    The treasure is in the fridge.
    """
    print("\nYou're in the kitchen. You can see a fridge and a door leading back to the hall.")
    choice = input("What do you want to do? (open fridge/go back) ")

    if choice == "open fridge":
        game_state["has_treasure"] = True
    elif choice == "go back":
        game_state["location"] = "hall"

    return game_state


def library(game_state):
    """
    Function for the library scenario. The player can return to the hall or read a book. Reading a book does nothing.
    """
    print("\nYou're in the library. There are many books on the shelves and a door leading back to the hall.")
    choice = input("What do you want to do? (read book/go back) ")

    if choice == "read book":
        print("You pick up a book and start reading. It's interesting but doesn't help you find the treasure.")
    elif choice == "go back":
        game_state["location"] = "hall"

    return game_state


def garden(game_state):
    """
    Function for the garden scenario. The player can return to the hall or water the plants.
    Watering the plants does nothing.
    """
    print("\nYou're in the garden. There are many beautiful plants and a door leading back to the hall.")
    choice = input("What do you want to do? (water plants/go back) ")

    if choice == "water plants":
        print("You water the plants. They seem to appreciate it, but it doesn't help you find the treasure.")
    elif choice == "go back":
        game_state["location"] = "hall"

    return game_state


def basement(game_state):
    """
    Function for the basement scenario. The player can return to the hall or search the boxes.
    Searching the boxes might reveal the treasure.
    """
    print("\nYou're in the basement. It's dark and there are many boxes around.")
    print("There's also a staircase leading back to the hall.")
    choice = input("What do you want to do? (search boxes/go back) ")

    if choice == "search boxes":
        print("You found nothing in the boxes!")
    elif choice == "go back":
        game_state["location"] = "hall"

    return game_state


if __name__ == "__main__":
    start_game()
