its my first github project :D

HOW TO USE 

1. open kitty or other termail
2. to run the program just do ./supernumbergen and watch the numbers genarate

CHANGING THE NUMBERS 

go to line 11 and you should see max_num = 99999999999999999999999999999999999999999999999999 just edit that default number make sure the number ends with 1 for e.g if you put 1001 it would genarate 1000 numbers 

THE CODE 

#!/usr/bin/env python3

import multiprocessing

def print_numbers(start, end):
    for num in range(start, end):
        print(num, end=" ")

if __name__ == "__main__":
    num_cores = multiprocessing.cpu_count()  # Get the number of CPU cores
    max_num = 99999999999999999999999999999999999999999999999999  # Set the max number you want to generate
    range_per_process = max_num // num_cores  # Divide the range across cores
    
    processes = []

    # Create processes to handle different ranges of numbers
    for i in range(num_cores):
        start = i * range_per_process + 1
        end = (i + 1) * range_per_process + 1
        process = multiprocessing.Process(target=print_numbers, args=(start, end))
        processes.append(process)
        process.start()

    # Ensure all processes have completed
    for process in processes:
        process.join()
