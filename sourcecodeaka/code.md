```
import time
import random
import matplotlib.pyplot as plt
from prettytable import PrettyTable

def linear_search_iterative(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

def linear_search_recursive(arr, target, index=0):
    if index >= len(arr):
        return -1
    if arr[index] == target:
        return index
    return linear_search_recursive(arr, target, index + 1)


n_values = []
iterative_times = []
recursive_times = []

table = PrettyTable()
table.field_names = ["Input (n)", "Iterative Time (s)", "Recursive Time (s)"]

while True:
    try:
        n = int(input("Masukkan jumlah data (atau -1 untuk keluar): "))
        if n == -1:
            print("Program selesai.")
            break
        if n <= 0:
            print("Masukkan nilai n yang valid!")
            continue

        data = list(range(n))
        random.shuffle(data)
        target = data[-1] 

        start = time.time()
        linear_search_iterative(data, target)
        iterative_time = time.time() - start

        start = time.time()
        linear_search_recursive(data, target)
        recursive_time = time.time() - start

        n_values.append(n)
        iterative_times.append(iterative_time)
        recursive_times.append(recursive_time)

        table.add_row([n, iterative_time, recursive_time])

        print("\nTabel Perbandingan Kinerja")
        print(table)

        plt.figure(figsize=(8, 5))
        plt.plot(n_values, recursive_times, label="Recursive", marker="o")
        plt.plot(n_values, iterative_times, label="Iterative", marker="o")
        plt.xlabel("Input (n)")
        plt.ylabel("Execution Time (seconds)")
        plt.title("Performance Comparison: Recursive vs Iterative")
        plt.legend()
        plt.grid(True)
        plt.show()

    except ValueError:
        print("Input tidak valid!")
```
