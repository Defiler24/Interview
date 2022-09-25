## Quick Sort
''' python
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
'''
