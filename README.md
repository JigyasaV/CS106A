# CS106A
Stanford_April-May2020
from karel.stanfordkarel import *

# Problem 1
from karel.stanfordkarel import *

"""
File: TripleKarel.py
--------------------
When you finish writing this file, TripleKarel should be
able to paint the exterior of three buildings in a given
world, as described in the Assignment 1 handout. You
should make sure that your program works for all of the 
Triple sample worlds supplied in the starter folder.
"""
"""
    Important conditions:
    1. Painting 3 exterior walls of the 3 buildings of any size in any world
    2. No paint(B) at the last spot where K is standing
    3. K will always start facing west at the upper right corner of the leftmost building
    4. Very important -  there will always be exactly three buildings, and their relative position to one another will
     always be the same
    :return:

    For the first 2 buildings, same set of code can be repeated as K will be moving in the same direction first 
    2 times and then in the opposite one last time
    As the number of buildings is constant too in any world, an IF loop rather than a WHILE loop can be used
"""
"""
Pre: K standing at the corner of a building with B already placed behind him
Post: Needs to place along the rest of the edges
"""
def main():
    for i in range(2):
        place_beepers_along_edges()
        turn_left()
        move()
        place_beepers_along_edges()
        turn_left()
        move()
        place_beepers_along_edges()
        put_beeper()
        turn_right()
        move()
    for i in range(2):
        place_beepers_along_edges()
        turn_left()
        move()
    place_beepers_along_edges()


"""
 For the third building, there will be a bit of an exception due to the placement along the third edge
 Pre: First 2 buildings have been painted
 Post: Third building needs to be painted with no B at the spot where K finally stands (next to the edge of
 the building)
 """

def place_beepers_along_edges():
    """
    Pre: K will always start facing west
    Post: K would have placed B along an edge of the building till left is blocked
    :return:
    """
    while left_is_blocked():
        put_beeper()
        move()


def turn_right():
    for i in range(3):
        turn_left()

# There is no need to edit code beyond this point

if __name__ == "__main__":
    run_karel_program()


   

# Problem2

from karel.stanfordkarel import *

"""
File: StoneMasonKarel.py
------------------------
When you finish writing code in this file, StoneMasonKarel should 
solve the "repair the quad" problem from Assignment 1. You
should make sure that your program works for all of the 
sample worlds supplied in the starter folder.
"""

def main():
    """
    1. Make karel create columns of beepers
    2. Columns are exactly four squares apart
    3. Columns are not of any fixed height
    4. Final column will always have a wall immediately after
    The problem can be broken down into 5 main steps:
    1. Building a column while ascending it (as K is always standing at the bottom)
    2. Finishing the column - very important for a condition when front is not clear but B is missing
    3. Returning to row one - Chris's combing technique
    4. Moving to next column (4 blocks apart ALWAYS)
    5. Continuing till front is clear - but to meet OFF BY 1 ERROR add extra steps for the last column - not part of the
     loop
     Got so badly stuck in the infinite loop where the column was only 1 high

    :return:
    """
    while front_is_clear():
        turn_left()
        """
        Pre: Facing east
        Post: Turn to the direction where the column needs to be built
        """
        build_column()
        """
        Pre: B present/absent
        Post: If not already present at the top stop, all but last will have a B
        """
        finish_column()
        """
        Introduced to cater to the condition when B not already present when front is blocked
        """
        turn_around()
        return_to_row_one()
        """
        Combing
        """
        turn_left()
        move_to_next_column()
    """
    To accommodate off by 1 error
    """
    turn_left()
    build_column()
    finish_column()
    turn_around()
    return_to_row_one()
    turn_left()


def build_column():
    """
    Pre: B present/absent
    Post: If not already present at the top stop, all but last will have a B
    :return:
    """
    while front_is_clear():
        if beepers_present():
            move()
        else:
            put_beeper()
            """
            To satisfy 1 column height
            """


def finish_column():
    if front_is_blocked():
        """
        If B not present at top
        """
        if no_beepers_present():
            put_beeper()


def turn_around():
    for i in range(2):
        turn_left()


def return_to_row_one():
    while front_is_clear():
        move()


def move_to_next_column():
    for i in range(4):
        move()



# There is no need to edit code beyond this point

if __name__ == "__main__":
    run_karel_program()



# Bonus problem 3
from karel.stanfordkarel import * 

"""
File: MidpointKarel.py
----------------------
When you finish writing it, MidpointKarel should
leave a beeper on the corner closest to the center of 1st Street
(or either of the two central corners if 1st Street has an even
number of corners).  Karel can put down additional beepers as it
looks for the midpoint, but must pick them up again before it
stops.  The world may be of any size, but you are allowed to
assume that it is at least as tall as it is wide.
"""

from karel.stanfordkarel import *


# File: midpoint.py
# -----------------------------
# Write a program, using only karel features,
# which allows Karel to put a beeper in the midpoint
# of a world of any width.

def main():
    """
    The problem can be solved by breaking it down into 4 main steps
    1. Filling up the bottom row with beepers
    2. Clearing the beepers off starting from the boundaries and going back and forth
    3. Reaching the mid-point (till no more beepers present)
    4. Placing a beeper at the mid point
    Unfortunately, my earlier code would work for all worlds except 1x1
    I realised the only way to make it work for 1x1 is to use an IF ELSE condition (and not WHILE)
    Only if the front is clear, should Karel follow the steps
    Else, put a beeper and rest
    With a WHILE (indefinite condition) it would have gone on forever

    Pre: Karel is facing east, no beepers in the world
    Post: Karel is standing at the mid-point of the 1st row in any world, with a beeper in the same position
    :return:
    """
    if front_is_clear():
        fill_bottom_row()
        """
        Pre: None
        Post: Karel is facing the opposite direction, and every step between Karel's old position and new position
        has a beeper added to it.
        """
        clear_boundaries()
        """
        Pre: Beepers are present in the entire first row
        Post: Karel has now reached next to the mid point of the world and removed all the beepers in the world
        """
        while beepers_present():
            find_midpoint()
            """
            Pre: Karel is sitting next to the mid-point and there are no beepers in the world
            The mid-point has been identified by the absence of any more beepers in the world
            Post: Karel identifies the midpoint
            """
        place_beeper_at_midpoint()
        """
        Pre: K has identified the mid-point
        Post: K moves 1 position and places a beeper. #Success
        """
    else:
        put_beeper()
        """
        Pre: If front is not clear
        Post: Put a beeper and rest in peace
        #This condition had to be added exclusively to cater to the demands of the smallest world (1x1)
        """


def fill_bottom_row():
    put_beeper()
    while front_is_clear():
        move()
        put_beeper()
    turn_around()


def turn_around():
    for i in range(2):
        turn_left()


def clear_boundaries():
    pick_beeper()
    move_to_wall()
    pick_beeper()
    turn_around()
    move()


def move_to_wall():
    while front_is_clear():
        move()


def find_midpoint():
    find_first_empty_spot()
    turn_around()
    move()
    pick_beeper()
    move()


def find_first_empty_spot():
    while beepers_present():
        move()


def place_beeper_at_midpoint():
    turn_around()
    move()
    put_beeper()

# There is no need to edit code beyond this point

if __name__ == "__main__":
    run_karel_program()


