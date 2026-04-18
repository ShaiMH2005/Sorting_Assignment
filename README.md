# Sorting_Assignment
Sorting_Assignment by Shai Meir Hershcovich and Yarin Zinger 

The selected algorithms are : 1- Bubble Sort
                              4- Merge Sort
                              5- Quick Sort
                                                            
Project Overview
This project provides a comprehensive experimental framework to analyze, measure, and compare the runtime of various sorting algorithms. The program evaluates how different algorithms behave under varying conditions, specifically testing completely random arrays versus nearly sorted arrays with controlled levels of "noise" (randomly swapped elements). The framework calculates statistical means and standard deviations over multiple iterations to ensure accurate benchmarking.


Code Structure & Implementation Details
The Python script (run_experiments.py) is divided into four distinct operational parts:
Part A: Algorithm Implementation and Checking it: This section contains the implementation of three sorting algorithms: Bubble_sort:The classic O(n^2) implementation. Quick_sort : A recursive divide-and-conquer approach. Merge_sort: An O(n *log n) implementation utilizing a helper _merge function to combine sub-arrays. Validation (test_sorting_algorithms): Before running any heavy experiments, the program automatically generates a random array of 20 elements, passes it through the implemented sorting algorithms, and verifies their correctness by comparing the outputs against Python's highly optimized, built-in sorted() function.

Part B: Comparative Experiment (Random Arrays)
The Experiment (run_experiments): Evaluates the performance of the core algorithms on completely random arrays of increasing sizes: (100, 500, 1000, 2000, 3000). 

Statistical Accuracy: To prevent abnormality, each array size is tested 5 times (Repeats). The script records the exact execution time (time.perf_counter()) and calculates the mathematical mean and standard deviation.

Output: The script prints a detailed report on a table to the console and generates a visual graph utilizing matplotlib. The graph includes shaded error margins representing the standard deviation and is automatically saved as result1.png.

Part C: Noise Experiment (Nearly Sorted Arrays)
Array Generation: This function simulates real-world scenarios where data is mostly sorted but contains minor errors. It creates a perfectly sorted array and then performs random element swaps based on a given percentage.

The Experiment, runned by run_part_c_experiment: Re-runs the benchmarking process from Part B, but applies it to nearly sorted arrays. It conducts two separate experimental phases:

Arrays with 5% noise (saved as result2_5_percent.png).

Arrays with 20% noise (saved as result2_20_percent.png).

Output: Generates comprehensive tabular console reports and saves the respective visual plots.

Part D: Command Line Interface (CLI) Custom Experiments
CLI Integration: Utilizes the Python argparse module to provide a flexible, interactive way to run custom sorting experiments directly from the terminal without modifying the code.

Expanded Algorithm Roster: Introduces two additional algorithms specifically for CLI testing: Selection Sort and Insertion Sort.

Dynamic Testing: Users can dynamically specify exact array sizes, algorithms to compare, noise levels, and the number of repetitions.

Output: The CLI experiment generates a customized statistical table in the terminal and exports the resulting plot as cli_result.png.


How to Run the Program:
The application supports two execution modes:

Mode 1: Full Automated Run (Parts A, B, and C)
If you simply execute the script without any parameters, the program will automatically run the sanity checks, the random array experiments, and both nearly-sorted experiments sequentially.

Mode 2: Custom CLI Execution (Part D)
To test specific algorithms and custom array sizes, use the command-line interface by providing the required flags. When flags are detected, the program will only run the custom experiment (Part D).

Command Syntax:
python run_experiments.py -a [Algorithms] -s [Sizes] -e [Experiment Type] -r [Repeats]

Example Command:
python run_experiments.py -a 1 4 5 -s 100 500 1000 -e 1 -r 5

Flags Explanation:

-a: The IDs of the algorithms to test. (1 = Bubble, 2 = Selection, 3 = Insertion, 4 = Merge, 5 = Quick)

-s: A list of array sizes to benchmark (e.g., 100 500 1000).

-e: Experiment type / Noise level. (1 = Nearly sorted with 5% noise, 2 = Nearly sorted with 20% noise)

-r: The number of repetitions per array size for statistical accuracy.

1. Short Explanations of the Results
Figure 1: result1.png (Random Arrays). This graph illustrates the runtime of the algorithms on completely randomized data. As expected, Bubble Sort demonstrates its average and worst-case time complexity of O(n^2). Its runtime grows quadratically as the array size increases, taking the longest time to complete (reaching over 0.5 seconds for an array size of 3000). Conversely, Quick Sort and Merge Sort are highly efficient divide-and-conquer algorithms that operate in O(n *log n) time. They handle the largest array sizes in mere fractions of a second, which is why their runtime lines remain completely flat and close to zero relative to the Y-axis scale dictated by Bubble Sort.

Figure 2: result2_5_percent.png, result2_20_percent.png. Nearly Sorted Arrays with Noise.
These graphs present the performance of the algorithms on arrays that are mostly sorted but contain a specific percentage of randomly swapped elements (noise). Visually, the overall trend remains similar to the random array experiment: Bubble Sort is still the bottleneck, while Quick Sort and Merge Sort remain incredibly fast. However, looking closely at the Y-axis values, Bubble Sort completes the sorting faster than it did in the completely random scenario, proving that the initial state of the data impacts its performance.


2. Analysis of Running Time Changes in Result 2 ,If and how the running times changed:
When comparing the results of the nearly sorted arrays (result2_5_percent, result2_20_percent) to the completely random arrays (Result 1), the running times of Merge Sort and Quick Sort remained largely unchanged (consistently near 0.0 seconds). However, the running time for Bubble Sort noticeably decreased. For an array of n=3000, Bubble Sort took approximately 0.53 seconds on a random array. In contrast, it took only approximately 0.35 seconds on the array with 5% noise, and approximately 0.41 seconds on the array with 20% noise. Why did this happen? The improvement in Bubble Sort: This decrease in runtime is a direct result of the swapped boolean flag optimization implemented in our bubble_sort function. In a completely random array, the algorithm is forced to perform almost all n iterations of the outer loop. However, when the array is nearly sorted, large sections of the data are already in their correct order. Once the algorithm finishes moving the randomly "noisy" elements to their proper places, it performs one final pass without making any swaps. The swapped flag remains False, triggering an early break from the loop, saving significant processing time. Naturally, the 5% noise array finished faster than the 20% noise array because there were fewer misplaced elements to fix. Why it is still slower than Quick/Merge: Despite the early exit optimization, Bubble Sort still shows a quadratic-like curve. This is due to a phenomenon known as "turtles"—small elements that were randomly swapped to the very end of the array. In Bubble Sort, large elements move to the right quickly, but small elements can only shift one position to the left per pass. Therefore, even a small percentage of noise forces the algorithm to make many passes to bring those "turtles" back to the start.The consistency of Quick and Merge Sort: Merge Sort and Quick Sort running times did not change noticeably because their time complexity is highly robust. Merge Sort always divides the array completely regardless of its content, maintaining a strict O(n *log n)time. Quick Sort (using the middle element as a pivot) also successfully avoids its O(n^2) worst-case scenario on these nearly sorted arrays, maintaining its O(n*log n) efficiency.
