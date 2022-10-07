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

## 搞脑子
``` python 
# 59
def generateMatrix(self, n: int) -> List[List[int]]:
    nums = [[0] * n for _ in range(n)]
    loop, mid, count, x, y = n // 2, n // 2, 1, 0, 0
    for lo in range(1, loop + 1):
        for i in range(y, n - lo):
            nums[x][i] = count
            count += 1
        for i in range(x, n - lo):
            nums[i][n - lo] = count
            count += 1
        for i in range(n - lo, y, -1):
            nums[n - lo][i] = count
            count += 1
        for i in range(n - lo, x, -1):
            nums[i][y] = count
            count += 1
        x += 1
        y += 1
    if n % 2 == 1:
        nums[mid][mid] = count
    return nums
```

## 双指针

``` python
# 27
def removeElement(self, nums: List[int], val: int) -> int:
    n = len(nums)
    slow, fast = 0, 0
    for i in range(n):
        if nums[i] != val:
            nums[slow] = nums[fast]
            fast += 1
            slow += 1
        else:
            fast += 1
    return slow
    
# 977
def sortedSquares(self, nums: List[int]) -> List[int]:
    left, right, k = 0, len(nums) - 1, len(nums) - 1
    res = [0] * len(nums)
    while left <= right:
        l, r = nums[left] * nums[left], nums[right] * nums[right]
        if l > r:
            res[k] = l
            left += 1
        else:
            res[k] = r
            right -= 1
        k -= 1
    return res
    
# 209
def minSubArrayLen(self, target: int, nums: List[int]) -> int:
    slow, fast, cur, length = 0, 0, 0, len(nums) + 1
    while fast < len(nums):
        cur += nums[fast]
        while cur >= target:
            t = fast - slow + 1
            length = min(t, length)
            cur -= nums[slow]
            slow += 1
        fast += 1
    return 0 if length == len(nums) + 1 else length
```

## 链表
``` python 
# 203
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
    virtual = ListNode(next=head)
    cur = virtual
    while cur.next != None:
        if cur.next.val == val:
            cur.next = cur.next.next
        else:
            cur = cur.next
    return virtual.next
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


