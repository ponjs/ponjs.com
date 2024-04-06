---
title: JavaScript 实现基本排序算法
pubDatetime: 2023-03-29T03:21:00.000Z
tags:
  - 前端
---

> 这里的所有实现方法，都是原地算法进行升序（在原有数组上进行从小到大排序）。

## 冒泡排序

重复地走访过要排序的元素列，依次比较两个相邻的元素，如果顺序错误就把他们交换过来。走访元素的工作是重复地进行直到没有相邻元素需要交换，也就是说该元素列已经排序完成。

```JavaScript
function bubbleSort(arr) {
  for (let i = 0, l = arr.length; i < l; i++) {
    for (let j = i + 1; j < l; j++) {
      const a = arr[i]
      const b = arr[j]
      if (a - b > 0) {
        arr[j] = a
        arr[i] = b
      }
    }
  }

  return arr
}
```

## 选择排序

首先从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，然后再从剩余的未排序元素中寻找到最小（大）元素，然后放到已排序的序列的末尾。以此类推，直到全部待排序的数据元素的个数为零。

```JavaScript
function selectSort(arr) {
  for (let i = 0, l = arr.length; i < l; i++) {
    let index = i
    for (let j = i + 1; j < l; j++) {
      if (arr[j] < arr[index]) {
        index = j
      }
    }

    const temp = arr[index]
    arr[index] = arr[i]
    arr[i] = temp
  }

  return arr
}
```

## 插入排序

每次从待排序的数据元素中选取第一个元素，再依次向前逐一比较找到其位置，然后插入进去。形成前面为排好序的有序表，后面为待排序。直到全部待排序的数据元素的个数为零。

```JavaScript
function insertionSort(arr) {
  for (let i = 1, l = arr.length; i < l; i++) {
    const temp = arr[i]
    let j = i - 1
    while (j >= 0 && arr[j] > temp) {
      arr[j + 1] = arr[j]
      j--
    }
    arr[j + 1] = temp
  }

  return arr
}
```

## 快速排序

选择一个基准数，通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小。然后再按此方法对这两部分子数列数据分别进行快速排序，整个排序过程递归进行，直到所有所有的序列排序完成。

```JavaScript
function quickSort(arr) {
  const sort = (s, e) => {
    if (s >= e) {
      return
    }

    const base = arr[e]
    let i = s
    let j = e

    while (i < j) {
      while (i < j && arr[i] <= base) {
        i++
      }
      arr[j] = arr[i]

      while (j > i && arr[j] >= base) {
        j--
      }
      arr[i] = arr[j]
    }
    arr[j] = base

    sort(s, j - 1)
    sort(j + 1, e)
  }

  sort(0, arr.length - 1)

  return arr
}
```

## 希尔排序

希尔排序，也称递减增量排序算法，是插入排序的一种更高效的改进版本。先规定一个间隔，一般取长度的一半，按间隔组成多个子数组，分别对子数组进行排序。然后再依次缩小间隔值，直到间隔为 1 就是直接插入排序。

```JavaScript
function shellSort(arr) {
  const len = arr.length
  for (let gap = len >> 1; gap > 0; gap >>= 1) {
    for (let i = gap; i < len; i++) {
      const temp = arr[i]
      let j = i - gap
      while (j >= 0 && arr[j] > temp) {
        arr[j + gap] = arr[j]
        j -= gap
      }
      arr[j + gap] = temp
    }
  }

  return arr
}
```
