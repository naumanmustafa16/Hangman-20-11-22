# Hangman-20-11-22
Hangman-Hyperskill

# Write your code here
import random
import string
words_list = ['python', 'java', 'swift', 'javascript']
word = random.choice(words_list)
pattern = len(word) * '-'
guessed_list =[]
mistake = 0
losses = 0
wins = 0
def printer():
    print(f"H A N G M A N")

def random_word(x):
    global word
    word = random.choice(words_list)
    return word

def guess():
    global mistake
    global pattern
    pattern = len(word) * '-'
    global guessed_list
    guessed_list = []
    mistake = 0
    global wins
    while mistake < 8:
        print()
        print(pattern)
        letter = input('Input a letter:')

        if len(letter) > 1 or len(letter) == 0:
            print('Please, input a single letter.')
            continue
        elif letter not in string.ascii_lowercase:
            print('Please, enter a lowercase letter from the English alphabet.')
            continue

        # if letter in guessed_list:
        #     print("No improvements.")

            #mistake = mistake + 1
        else:
            if (letter in guessed_list) and (letter in word):
                print("You've already guessed this letter.")
            if letter not in guessed_list and letter in word:
                guessed_list.append(letter)
                # print(guessed_list)
                pos1 = word.find(letter)
                pos2 = word.rfind(letter)
                pattern_lis = list(pattern)
                # print(pattern_lis)
                # print(pattern)
                # print(pattern_lis)
                pattern_lis[pos1] = letter
                pattern_lis[pos2] = letter
                pattern = ''.join(pattern_lis)
                if pattern == word:
                    print(pattern)
                    print(f'You guessed the word {word}!\nYou survived!')
                    wins = wins + 1
                    break
                else:
                    continue

            else:

                # print(guessed_list)
                if (letter not in guessed_list) and (letter not in word):
                    print("That letter doesn't appear in the word")
                    mistake = mistake + 1
                    guessed_list.append(letter)
                    continue
                elif (letter in guessed_list) and (letter not in word):
                    print("You've already guessed this letter.")
                    continue
def menue():
    printer()
    while True:
        input1 = input('Type "play" to play the game, "results" to show the scoreboard, and "exit" to quit:')
        if input1 == 'play':
            run()
        elif input1 == 'results':
            print(f'You won: {wins} times.')
            print(f'You lost: {losses} times.')
        elif input1 == 'exit':
            break
        else:
            input1 = input('Type "play" to play the game, "results" to show the scoreboard, and "exit" to quit:')
def run():
    global losses

    random_word(words_list)
    guess()
    if mistake == 8 and pattern != word:
        print('You Lost!')
        losses = losses + 1
menue()
