# CS106A
Stanford_April-May2020
from karel.stanfordkarel import *

Problem#1
# File: triple.py
# -----------------------------
# Write a program, using only karel featuers,
# which solve the triple problem
def main():
   place_beepers_along_edges()
   put_beeper()
   turn_left()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_left()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_right()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_left()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_left()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_right()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_left()
   move()
   place_beepers_along_edges()
   put_beeper()
   turn_left()
   move()
   place_beepers_along_edges()
   
def place_beepers_along_edges():
 while left_is_blocked():
  put_beeper()
  move()
  
def turn_right():
 for i in range(3):
    turn_left()
 
   # karel needs to paint three outside
   # edges along the three buildings in 
   # any world
   # The dimensions may vary, but the number
   # and relative position will be same
   
Problem#2
# This is an editor! Write your solution here.
# Make karel create four columns of beepers
# Columns are exactly four squares apart
# Columns are not of any fixed height
# Final column will always have a wall 
# immediatelt after


def main():
 while front_is_clear():
   turn_left()
   build_column()
   finish_column()
   turn_around()
   return_to_row_one()
   turn_left()
   move_to_next_column()
 turn_left()
 build_column()
 finish_column()
 turn_around()
 return_to_row_one()
 turn_left()
   
def build_column():
   while front_is_clear():
      if beepers_present():
         move()
      else:
         put_beeper()
   
def finish_column():
   if front_is_blocked():
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
