# Write a function that can print out a board



def display_board(board):
    print(board[7]+'|'+board[8]+'|'+board[9])
    print('-|-|-')
    print(board[4]+'|'+board[5]+'|'+board[6])  
    print('-|-|-')
    print(board[1]+'|'+board[2]+'|'+board[3])
    print('-|-|-')
test_board = ['#', 'X', 'O', 'X', 'O', 'X', 'O', 'X', 'O', 'X']
display_board(test_board)


# Step 2  write a function that can take in a player input and assign their 'X' or 'O'
def player_input():
    '''
    OUTPUT = (Player 1 marker, Player 2 marker)
    '''
    marker = ''
    while marker != 'X' and marker != 'O':
        marker = input('Player1: Choose X or O:. ').upper()
        if marker == 'X':
            
            return ('X','O')
        else:
            return('O','X')
player1_marker , player2_marker = player_input() # Tuple unpacking here
player2_marker

# Step 3- write a function thats takes in the board list object!

def place_marker(board, marker, position):
    
    board[position] = marker
place_marker(test_board,'$',8)
display_board(test_board)

# Step4- Write a function that takes in a board and a mark(X or O) and then--
# checks to see if that mark has won

def win_check(board, mark):
    
    # WIN TIC TAC TOE?
    # All ROWS, and check to see if they all share the same marker?
    
    # ALL COLUMNS, check to see if marker matches 
    # 2 diagonals, check to see match

    return ((board[7] == mark and board[8] == mark and board[9] == mark ) or # across the top 
    (board[4] == mark and board[5] == mark and board[6] == mark) or # across the middle
    (board[1] == mark and board[2] == mark and board[3] == mark) or # across the bottom
    (board[7] == mark and board[4] == mark and board[1] == mark) or # across the middle
    (board[8] == mark and board[5] == mark and board[2] == mark) or # Down the middle
    (board[9] == mark and board[6] == mark and board[3] == mark) or # Down the side
    (board[7] == mark and board[5] == mark and board[3] == mark) or # diagonal
    (board[9] == mark and board[5] == mark and board[1] == mark)) # diagonal
display_board(test_board)
win_check(test_board,'X')

# Step5- Write the function uses the random module to randomly decide which player goes
#first.You may want to lookup random.randint() Return a string of player went first


import random

def choose_first():
    
    flip = random.randint(0,1)
    
    if flip == 0:
        return 'Player 1'
    else:
        return 'Player 2'
    
# Step 6: Write a function that returns a boolean indicating whether a space the board is freely available

def space_check(board, position):
    
    return board[position] == ' '
 
    
# Write a function that checkes if the board is full and returns a boolean value.
# True if full, False Otherwise

def full_board_check(board):
    
    for i in range(1,10):
        if space_check(board,i):
            return False
    
    # BOARD IS FULL IS WE RETURN TRUE
    return True

# Step8- Write a function that asks for a player a next position(as a number 1-9)
# and then uses the function from step 6 to check if its a free position.
#If it is, then return the position for later use.


def player_choice(board):
    
    position = 0
    
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position = int(input('Chooose a position: (1-9) '))
    
    return position


# Step9-- Write a function that asks the player if they want to play again and returns
# a boolean True if they do want play again

def replay():
    
    choice = input("Play again? Enter Yes or No")
    return choice == 'Yes'

#Step10-- Here comes the hard part! Use while loops and the functions you have
#to run the game

# while loop to keep running the game

print('Welcome to Tic TAC TOE')

while True:
    
    
    # Play the GAME
    
    # set everything up(board, whos first, choose, markers X,O)
    the_board = [' ']*10
    player1_marker,player_marker = player_input()
    
    turn = choose_first()
    print(turn + 'will go first')
    
    play_game = input('Ready to play? y or n? ')
    
    if play_game == 'y':
        game_on = True
    
    else:
        game_on = False
        
    ## GAME PLAY
    
    while game_on:
        
        if turn == 'Player 1':
            
            # Show the board
            
            display_board(the_board)
            
            # choose a position
            position = player_choice(the_board)
            
            
            # Place the marker on the position
            
            place_marker(the_board,player1_marker,position)
            
            # check if they won
            
            if win_check(the_board,player1_marker):
                display_board(the_board)
                print('PLAYER 1 HAS WON!!')
                game_on = False
            
            else:
                
                #or check if there is a tie
                
                # no Tie and no win? Then next player's turn
                
                if full_board_check(the_board):
                    display_board(the_board)
                    print("TIE GAME!")
                    game_on = False
                else:
                    turn = 'Player2'
                    
        else:
            display_board(the_board)
            
            # choose a position
            position = player_choice(the_board)
            
            
            # Place the marker on the position
            
            place_marker(the_board,player2_marker,position)
            
            # check if they won
            
            if win_check(the_board,player2_marker):
                display_board(the_board)
                print('PLAYER 2 HAS WON!!')
                game_on = False
            
            else:
                
                #or check if there is a tie
                
                # no Tie and no win? Then next player's turn
                
                if full_board_check(the_board):
                    display_board(the_board)
                    print("TIE GAME!")
                    game_on = False
                else:
                    turn = 'Player1'
                    
    if not replay():
        break
            
        
            
           
