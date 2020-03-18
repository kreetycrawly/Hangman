# Hangman
Visual hangman in Python 3. Tough, funny, 6 guesses max.

import random

guesses = 6   #max guesses is 6
letters_to_choose_from=['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']
words=('chrysanthemum','chihuahua','noice','jazzy','squabbing','puzzling','ragamuffin','sphynx','rhythm','easy') #list of words to guess from 
word=words[(random.randrange(0,10,1))] #randomly picks one word out of the words list
guessed_letters=[] #list of letters already tried

def show_Hangman(guesses):    #what hangman looks like after each guess
    print("\n")
    if guesses == 6: 
        print("_______");
        print("||    O");
        print("||   /|/");
        print("||   //");
    elif guesses == 5:
        print("_______");
        print("||    O");
        print("||   /|/");
        print("||   /");
    elif guesses == 4:
        print("_______");
        print("||    O");
        print("||   /|/");
        print("||   ");
    elif guesses == 3:
        print("_______");
        print("||    O");
        print("||   /|");
        print("||   ");
    elif guesses == 2:
        print("_______");
        print("||    O");
        print("||    |");
        print("||   ");
    elif guesses == 1:
        print("_______");
        print("||    O");
        print("||    ");
        print("||   ");
    else: 
        print("_______");
        print("||    ");
        print("||    ");
        print("||   ");
        print("You lose."); 
        exit(0)
        
def print_valid_letters():
    print("\nCHOOSE A LETTER FROM THE FOLLOWING:")
    for i in letters_to_choose_from:
        print(i, end=" ")
    print("\n")    

def print_state_of_word():
    for i in range(len(word)):
        if word[i] in guessed_letters:
            print(word[i], end=" ")
        else:
            print("_ ", end="")
                
def is_letter_in_word(letter):
    for i in range(len(word)):
        if word[i]==letter:
           return True
    return False
    
def has_player_guessed_all_letters():
    a=set(word)
    if(set(a).issubset(set(guessed_letters))):
        print("\nYou WIN !!!")
        exit(0)

#initial state 
show_Hangman(guesses)
print_state_of_word()
print_valid_letters()

#validating the player's guesses
while guesses>=0:
    g=input("\nEnter guess\n")
    if g not in guessed_letters:
        if not g.isalpha():
            print("Enter a letter, nothing else")
            continue
        else: 
            guessed_letters.append(g)
            letters_to_choose_from.remove(g)
            if (not is_letter_in_word(g)):
                guesses -=1
                print(g, "is INCORRECT!")
                show_Hangman(guesses)
                print_state_of_word()
                print_valid_letters()
            else:
                guessed_letters.append(g)   
                print(g, "is CORRECT!")
                show_Hangman(guesses)
                print_state_of_word()
                print_valid_letters()    
    else:
        print("You've already tried this. Enter a different letter")
        show_Hangman(guesses)
        print_state_of_word()
        print_valid_letters()
    
    has_player_guessed_all_letters()
    

