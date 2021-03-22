```golang
func quickSort(arr []int, start, end int) {
	if start > end {
		return
	}
	temp := arr[start]
	left, right := start, end
	for {
		// 从后往前 找小于基准值的数
		for arr[right] >= temp && left < right {
			right -= 1
		}
		// 从前往后 找大于基准值的数
		for arr[left] <= temp && left < right {
			left += 1
		}
		if left >= right {
			break
		}
		// 交换
		arr[left], arr[right] = arr[right], arr[left]
	}
	// 基准点值 跟焦点减缓
	arr[start], arr[left] = arr[left], arr[start]
	quickSort(arr, start, left-1)
	quickSort(arr, left+1, end)
}

```