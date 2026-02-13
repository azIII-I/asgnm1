# # Description: a program that validates user input, proccesses data,
# draw random lines and displays result in the console.

# import libraries
# initialize turtle
import turtle
import random
import math

print('== Assignment 2 ==')

# function1 prompts the user to input valid integer 
def fun1(prompt, lower_bound = 1, upper_bound = 100):
    value = int(input(prompt))
    while value < lower_bound or value > upper_bound:
      print(f'Invalid input, must be between {lower_bound} and {upper_bound}.')
      value = int(input(prompt))
    return value
       
# function2 draws a single line 
def fun2(x1, y1, x2, y2, color = 'black'):
   dx = x2 - x1
   dy = y2 - y1
   turtle.color(color)
   turtle.penup()
   turtle.goto(x1, y1)
   turtle.pendown()
   turtle.goto(x2, y2)
   length = math.sqrt(dx * dx + dy * dy)
   return length

# function3 draws multiple random lines
# information about the random line
# calculate total/average/max length
def fun3(num_lines = 1, color_num = 0):
   if color_num == 1:
      color = 'red'
   elif color_num == 2:
      color = 'blue'
   elif color_num == 3: 
      color = 'green'
   else:
      color = 'black'
   max_index = 0
   total_length = 0 
   max_length = 0 
   for i in range(num_lines):
      x1 = random.randint(-200, 200)
      y1 = random.randint(-200, 200)
      x2 = random.randint(-200, 200)
      y2 = random.randint(-200, 200)
      length = fun2(x1, y1, x2, y2, color)
      total_length += length
      if length > max_length: 
          max_length = length
          max_index = i + 1
      print(f'Drawn line # {i + 1}: a {color} line'
             f' from {(x1,y1)} to {(x2,y2)} of length {length:.2f}')
   avg_length = total_length / num_lines
   print()
   print(f'Total length of all lines: {total_length:.2f}')
   print(f'Average length of all lines: {avg_length:.2f}')
   print(f'Longest line: No.#{max_index} with length {max_length:.2f}')
   return total_length, avg_length, max_length

# function4 that calls other functions 
# uses user inputs to read data
def main(): 
   while True:
      num_lines = fun1('Enter the number of random lines (5 to 20): ', 5, 20)
      color_num = fun1('Enter line color number '
      '(1-red; 2-blue; 3-green) (1 to 3): ', 1, 3)
      print()
      fun3(num_lines, color_num)
      print()
      play_again = fun1('Play Again (1-Yes; 2-No) (1 to 2): ', 1, 2)
      print()
      if play_again == 2:
         break
   print('Thank You! Goodbye!')

main()

turtle.done()
