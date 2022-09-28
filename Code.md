## Quick Sort
``` python
def quick_sort(arr, left, right):
    if left >= right:
        return arr
    key = arr[left]
    i, j = left, right
    while i < j:
        while i < j and arr[j] >= key:
            j -= 1
        arr[i] = arr[j]
        while i < j and arr[i] <= key:
            i += 1
        arr[j] = arr[i]
    arr[i] = key
    quick_sort(arr, left, i - 1)
    quick_sort(arr, i + 1, right)
    return arr
```

## BackTrack
``` python
# 77
def combine(self, n: int, k: int) -> List[List[int]]:
    res, path = [], []
    def backtrack(n, k, start):
        if len(path) == k:
            res.append(path[:])
            return
        for i in range(start, n - (k - len(path)) + 2):
            path.append(i)
            backtrack(n, k, i + 1)
            path.pop()
    backtrack(n, k, 1)
    return res

# 216
def combinationSum3(self, k: int, n: int) -> List[List[int]]:
    res, path = [], []
    def backtrack(k, n, start):
        if sum(path) > n:
            return
        if len(path) == k:
            if sum(path) == n:
                res.append(path[:])
            return
        for i in range(start, 11 - k + len(path)):
            path.append(i)
            backtrack(k, n, i + 1)
            path.pop()
    backtrack(k, n, 1)
    return res
```

## DFS

``` python
# 797
def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
    res, path = [], [0]
    def dfs(x):
        if len(graph) - 1 == x:
            res.append(path[:])
        for i in graph[x]:
            path.append(i)
            dfs(i)
            path.pop()
    dfs(0)
    return res

# 200
def numIslands(self, grid: List[List[str]]) -> int:
    m, n, count = len(grid), len(grid[0]), 0
    def dfs(grid, i, j):
        if not 0 <= i < m or not 0 <= j < n: return # border
        if grid[i][j] != '1': return # value
        grid[i][j] = '2' # mark
        dfs(grid, i + 1, j)
        dfs(grid, i, j + 1)
        dfs(grid, i - 1, j)
        dfs(grid, i, j - 1)
    for i in range(m):
        for j in range(n):
            if grid[i][j] == '1':
                dfs(grid, i, j)
                count += 1          
    return count    

# 695
def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
    m, n, res = len(grid), len(grid[0]), 0
    def dfs(i, j):
        if not 0 <= i < m or not 0 <= j < n: return 0
        if grid[i][j] != 1: return 0
        grid[i][j] = 2
        return 1 + dfs(i - 1, j) + dfs(i + 1, j) + dfs(i, j - 1) + dfs(i, j + 1)

    for i in range(m):
        for j in range(n):
            if grid[i][j] == 1:
                a = dfs(i, j)
                res = max(a, res)
    return res
```


