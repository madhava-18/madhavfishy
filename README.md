1) worst case

import random

def linear_search(arr, target):
    ops = 0
    for x in arr:
        ops += 1
        if x == target:
            break
    return ops


print("n\tWorst\tAverage")

n_values = [10, 20, 40, 80, 160]

for n in n_values:
    arr = list(range(n))

    # Worst case: not found
    worst = linear_search(arr, -1)

    # Average case: random element
    total = 0
    for _ in range(20):
        total += linear_search(arr, random.choice(arr))
    average = total // 20

    print(f"{n}\t{worst}\t{average}")

print("\nOBSERVATION:")
print("Worst case increases linearly with n")
print("Average case increases linearly with n")
print("=> Time Complexity = O(n)")


    2)randomizedquicksort
	

    import random

def randomized_partition(arr, low, high):
    pivot_index = random.randint(low, high)
    arr[pivot_index], arr[high] = arr[high], arr[pivot_index]
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def randomized_quick_sort(arr, low, high):
    if low < high:
        pi = randomized_partition(arr, low, high)
        randomized_quick_sort(arr, low, pi - 1)
        randomized_quick_sort(arr, pi + 1, high)

if __name__ == "__main__":
    arr = [10, 7, 8, 9, 1, 5]
    n = len(arr)
    print("Original array:", arr)
    randomized_quick_sort(arr, 0, n - 1)
    print("Sorted array:  ", arr)

3)strassen multiplication

import numpy as np

def strassen(A, B):
    """Perform Strassen's Matrix Multiplication on A and B"""
 
    # Base case
    if len(A) == 1:
        return A * B

    # Split matrices
    mid = len(A) // 2

    A11 = A[:mid, :mid]
    A12 = A[:mid, mid:]
    A21 = A[mid:, :mid]
    A22 = A[mid:, mid:]

    B11 = B[:mid, :mid]
    B12 = B[:mid, mid:]
    B21 = B[mid:, :mid]
    B22 = B[mid:, mid:]

    # Strassen's 7 products
    M1 = strassen(A11 + A22, B11 + B22)
    M2 = strassen(A21 + A22, B11)
    M3 = strassen(A11, B12 - B22)
    M4 = strassen(A22, B21 - B11)
    M5 = strassen(A11 + A12, B22)
    M6 = strassen(A21 - A11, B11 + B12)
    M7 = strassen(A12 - A22, B21 + B22)

    # Calculate result submatrices
    C11 = M1 + M4 - M5 + M7
    C12 = M3 + M5
    C21 = M2 + M4
    C22 = M1 - M2 + M3 + M6

    # Combine submatrices
    C = np.zeros((len(A), len(A)), dtype=int)

    C[:mid, :mid] = C11
    C[:mid, mid:] = C12
    C[mid:, :mid] = C21
    C[mid:, mid:] = C22

    return C


# Example usage
if __name__ == "__main__":

    A = np.array([[1, 2],
                  [3, 4]])

    B = np.array([[5, 6],
                  [7, 8]])

    print("Matrix A:")
    print(A)

    print("\nMatrix B:")
    print(B)

    result = strassen(A, B)

    print("\nResult of Strassen's Matrix Multiplication:")
    print(result)

    4)mergesort

    def merge_sort(arr):
    # Base case
    if len(arr) <= 1:
        return arr

    # Find the middle index
    mid = len(arr) // 2

    # Divide the array
    left_half = arr[:mid]
    right_half = arr[mid:]

    # Recursively sort both halves
    left_sorted = merge_sort(left_half)
    right_sorted = merge_sort(right_half)

    # Merge the sorted halves
    return merge(left_sorted, right_sorted)


def merge(left, right):
    """Merge two sorted lists into one sorted list."""

    merged = []
    i = 0
    j = 0

    # Compare elements and merge
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1

    # Add remaining elements
    merged.extend(left[i:])
    merged.extend(right[j:])

    return merged


# Example usage
if __name__ == "__main__":
    arr = [38, 27, 43, 3, 9, 82, 10]

    print("Original array:", arr)

    sorted_arr = merge_sort(arr)

    print("Sorted array:", sorted_arr)

    5)knapsack
    
    def knapsack(weights, values, capacity):
    # Number of items
    n = len(weights)
	
    # Create DP table
    dp = [[0 for _ in range(capacity + 1)] for _ in range(n + 1)]

    # Fill DP table
    for i in range(1, n + 1):
        for w in range(1, capacity + 1):

            # If item weight is less than or equal to current capacity
            if weights[i - 1] <= w:
                dp[i][w] = max(
                    dp[i - 1][w],
                    dp[i - 1][w - weights[i - 1]] + values[i - 1]
                )
            else:
                dp[i][w] = dp[i - 1][w]

    # Maximum value possible
    return dp[n][capacity]


# Example usage
if __name__ == "__main__":
    # Weights and values of items
    weights = [2, 3, 4, 5]
    values = [3, 4, 5, 6]

    # Knapsack capacity
    capacity = 5

    # Call function
    max_value = knapsack(weights, values, capacity)

    print(f"Maximum value in knapsack of capacity {capacity}: {max_value}")

    6)dijkstra

    import sys

def min_dist(dist, visited):
    minimum = sys.maxsize
    ind = -1

    for k in range(len(dist)):
        if not visited[k] and dist[k] <= minimum:
            minimum = dist[k]
            ind = k

    return ind


def greedy_dijkstra(graph, src):
    n = len(graph)

    dist = [sys.maxsize] * n
    visited = [False] * n

    dist[src] = 0

    for _ in range(n):
        m = min_dist(dist, visited)
        visited[m] = True

        for k in range(n):
            if (not visited[k] and graph[m][k] != 0 and
                dist[m] != sys.maxsize and
                dist[m] + graph[m][k] < dist[k]):
                dist[k] = dist[m] + graph[m][k]

    print("Vertex\tDistance from Source")

    for k in range(6):
        print(chr(65 + k), "\t", dist[k])


graph = [
    [0, 1, 2, 0, 0, 0],
    [1, 0, 0, 5, 1, 0],
    [2, 0, 0, 2, 3, 0],
    [0, 5, 2, 0, 2, 2],
    [0, 1, 3, 2, 0, 1],
    [0, 0, 0, 2, 1, 0]
]

greedy_dijkstra(graph, 0)

7)warshall algorithm

def warshall(graph):
    # Number of vertices in the graph
    n = len(graph)

    # Copy of the graph to store the reachability matrix
    reach = [row[:] for row in graph]

    # Apply Warshall's Algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                # If there's a path from i to j through k, update the reachability matrix
                reach[i][j] = reach[i][j] or (reach[i][k] and reach[k][j])

    return reach


# Example usage
if __name__ == "__main__":
    # Graph represented as an adjacency matrix
    graph = [
        [0, 1, 0, 0],
        [0, 0, 1, 0],
        [0, 0, 0, 1],
        [1, 0, 0, 0]
    ]

    print("Adjacency Matrix:")
    for row in graph:
        print(row)

    # Call Warshall's algorithm
    reachability_matrix = warshall(graph)

    print("\nReachability Matrix (Transitive Closure):")
    for row in reachability_matrix:
        print(row)

  8)prims alogirthm

  import heapq

def prims_algorithm(graph, start):
    n = len(graph)

    # Minimum edge weight to each vertex
    min_edge = [float('inf')] * n
    min_edge[start] = 0

    # Parent array
    parent = [-1] * n

    # Priority Queue
    pq = [(0, start)]

    # Visited array
    in_mst = [False] * n

    mst_edges = []

    while pq:
        weight, u = heapq.heappop(pq)

        if in_mst[u]:
            continue

        in_mst[u] = True

        if parent[u] != -1:
            mst_edges.append((parent[u], u, weight))

        # Update adjacent vertices
        for v, edge_weight in enumerate(graph[u]):
            if edge_weight > 0 and not in_mst[v] and edge_weight < min_edge[v]:
                min_edge[v] = edge_weight
                parent[v] = u
                heapq.heappush(pq, (edge_weight, v))

    return mst_edges


# Example usage
if __name__ == "__main__":

    graph = [
        [0, 2, 0, 6, 0],
        [2, 0, 3, 8, 5],
        [0, 3, 0, 0, 7],
        [6, 8, 0, 0, 9],
        [0, 5, 7, 9, 0]
    ]

    start_node = 0

    mst = prims_algorithm(graph, start_node)

    print("Minimum Spanning Tree Edges:")

    total = 0
    for u, v, weight in mst:
        print(f"Edge: {u} - {v} with weight {weight}")
        total += weight

    print("Total Weight =", total)


9)eight queens

def is_safe(board, row, col):
    # Check column and diagonals for conflicts
    for i in range(row):
        if board[i] == col or board[i] - i == col - row or board[i] + i == col + row:
            return False
    return True

def solve_n_queens(board, row, solutions):
    # If all queens are placed, save a copy of the solution
    if row == len(board):
        solutions.append(board[:])
        return

    # Try placing a queen in each column of the current row
    for col in range(len(board)):
        if is_safe(board, row, col):
            board[row] = col  # Place the queen
            solve_n_queens(board, row + 1, solutions)  # Recur for next row
            board[row] = -1  # Backtrack (remove the queen)

def print_solution(board):
    # Convert board into a readable format
    n = len(board)
    for row in range(n):
        line = ['Q' if board[row] == col else '.' for col in range(n)]
        print(" ".join(line))

def clicks_eight_queens():
    n = 8  # Standard 8x8 chessboard
    board = [-1] * n  # Initialize the board (-1 means no queen placed)
    solutions = []  # To store all the possible solutions
    
    solve_n_queens(board, 0, solutions)
    
    # Print all solutions
    print(f"Total Solutions: {len(solutions)}\n")
    for solution in solutions:
        print_solution(solution)
        print()

# Call the function to solve the 8-Queens problem
clicks_eight_queens()


10)sum of subsetproblem

def sum_of_subsets(nums, target):

    result = []

    def backtrack(index, current_subset, current_sum):

        # If target is reached
        if current_sum == target:
            result.append(list(current_subset))
            return

        # Stop if sum exceeds target or index is out of range
        if current_sum > target or index >= len(nums):
            return

        # Include current element
        current_subset.append(nums[index])
        backtrack(index + 1, current_subset, current_sum + nums[index])

        # Backtrack
        current_subset.pop()

        # Exclude current element
        backtrack(index + 1, current_subset, current_sum)

    backtrack(0, [], 0)

    return result


# Example usage
if __name__ == "__main__":

    nums = [10, 7, 5, 18, 12, 20, 15]
    target = 35

    solutions = sum_of_subsets(nums, target)

    print(f"Subsets of {nums} that sum to {target}:\n")

    for s in solutions:
        print(s)

        11)travelling salesman

        import heapq,copy
INF=float('inf')

def reduce(m):
    n,c=len(m),0
    for i in range(n):
        r=min((x for x in m[i] if x!=INF),default=0)
        if r>0:c+=r;m[i]=[x-r if x!=INF else x for x in m[i]]
    for j in range(n):
        r=min((m[i][j] for i in range(n) if m[i][j]!=INF),default=0)
        if r>0:c+=r;[m[i].__setitem__(j,m[i][j]-r) for i in range(n) if m[i][j]!=INF]
    return c,m

def tsp(cost):
    n=len(cost);init,m=reduce(copy.deepcopy(cost))
    pq=[(init,0,[0],m)];best=INF;path=[]
    while pq:
        c,v,p,m=heapq.heappop(pq)
        if len(p)==n:
            tot=c+cost[v][0]
            if tot<best:best,path=tot,p+[0]
            continue
        for nxt in range(n):
            if nxt not in p and cost[v][nxt]!=INF:
                nm=copy.deepcopy(m)
                for k in range(n):nm[v][k]=nm[k][nxt]=INF
                nm[nxt][0]=INF if len(p)+1!=n else 0
                red,nm=reduce(nm)
                heapq.heappush(pq,(c+m[v][nxt]+red,nxt,p+[nxt],nm))
    return best,path

cm=[[INF,10,15,20],[10,INF,35,25],[15,35,INF,30],[20,25,30,INF]]
c,p=tsp(cm)
print("Minimum cost:",c,"Path:",p)
