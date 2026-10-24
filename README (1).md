# Solving Max-Cut with QAOA

IQ Hack Fall 2026, Beginners Track: QAOA

**Group Name:** Chargers 3

**Group Members:** Divyesh Patel, University of Alabama in Huntsville (UAH), Cybersecurity Engineering, Undergraduate

**Submission Category:** Rising Star

**Notebook:** qaoa\_maxcut\_hackathon.ipynb

## What we did

* Picked the QAOA track and the Max-Cut problem. Max-Cut means splitting the nodes of a graph into two groups so that as many edges as possible go between the groups.
* Built the QAOA circuit in Qiskit and ran it on a simulator (no hardware noise).
* Found the true best answer for every graph by brute force, so we could see how close QAOA gets.
* Experiment 1: compared 4 optimizers (COBYLA, Powell, BFGS, L-BFGS-B).
* Experiment 2: changed the graph size (4 to 9 nodes).
* Experiment 3: changed the circuit depth (1 to 4 layers).

## Why we chose this

Max-Cut is one of the beginner-friendly projects for this challenge. It is very easy to understand because it is just a puzzle on a graph. The graphs we use are small, so we can find the exact answer and check how good QAOA really is. The ideas from the hackathon slides (optimizers and system size) also fit well with this problem.

## How the code works

1. Make a random graph and find its best cut by trying every possible split.
2. Write the problem as a cost function. A lower cost means more edges are cut.
3. Build the QAOA circuit with Qiskit. It has two knobs per layer (called beta and gamma).
4. Use a normal optimizer from SciPy to tune the knobs, starting from random values.
5. Read the final probabilities from the circuit and work out the average cut.
6. Repeat with different optimizers, graph sizes and circuit depths, and print the results.

## Results

We use two scores:

* **Quality score** = average cut found / best possible cut. A score of 1.0 is perfect.
* **Chance of a perfect answer** = the probability that one run of the circuit gives a best possible cut.


Going from 1 layer to 2 layers helped a lot. After that the scores stayed about the same, so extra layers did not help in our tests. One possible reason is that more layers means more knobs to tune, which is harder for the optimizer. We did not test this.

## Limits of our work

* We only used a simulator, so these results say nothing about real quantum hardware and its noise.
* The graphs are small (9 nodes at most).
* Experiments 1 and 3 use only one graph and 6 starts, so other graphs might give different results. Small differences should not be over-read.
* We did not try other mixers, weighted edges or real hardware.

## Conclusions

* QAOA found good answers on small graphs, with quality scores of about 0.7 to 0.9, but not always a perfect one.
* The starting point mattered about as much as the optimizer. Powell was the best in our test, but it was slower.
* Bigger graphs made a perfect answer less likely. Going from 1 to 2 layers helped, but more layers did not.
* Next we would try weighted graphs, a different mixer, and real hardware.

## How to run

1. Open qaoa\_maxcut\_hackathon.ipynb in Jupyter, VS Code or Google Colab.
2. Run all the cells from top to bottom. The first cell installs the packages it needs.
3. The results are printed under the code cell when it finishes.