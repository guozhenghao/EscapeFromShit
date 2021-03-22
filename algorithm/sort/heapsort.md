```golang
func topK() {
	arr := []int{3, 7, 9, 8, 38, 93, 12, 222, 45, 93, 23, 84, 65, 2}
	k := 5
	for i := (k - 1)/2; i >= 0; i--{
		arr = adjustSmallRoot(arr, i, k-1)
	}
	for i := k; i < len(arr); i++{
		if arr[i] > arr[0]{
			arr[i], arr[0] = arr[0], arr[i]
			arr = adjustSmallRoot(arr, 0, k-1)
		}
	}
	fmt.Println(arr)
}

// 构建大根堆
func adjustBigRoot(arr []int, index, length int) []int {
	leftIndex := index*2 + 1
	rightIndex := index*2 + 2
	maxIndex := index
	if leftIndex <= length && arr[leftIndex] > arr[maxIndex] {
		maxIndex = leftIndex
	}
	if rightIndex <= length && arr[rightIndex] > arr[maxIndex] {
		maxIndex = rightIndex
	}
	if maxIndex == index {
		return arr
	}
	arr[index], arr[maxIndex] = arr[maxIndex], arr[index]
	return adjustBigRoot(arr, maxIndex, length)
}

// 构建小根队 topk
func adjustSmallRoot(arr []int, index, length int) []int {
	leftIndex, rightIndex := index * 2 + 1, index * 2 + 2
	smallIndex := index
	if leftIndex <= length && arr[smallIndex] > arr[leftIndex]{
		smallIndex = leftIndex
	}
	if rightIndex <= length && arr[smallIndex] > arr[rightIndex]{
		smallIndex = rightIndex
	}
	if smallIndex == index{
		return arr
	}
	arr[smallIndex], arr[index] = arr[index], arr[smallIndex]
	return adjustSmallRoot(arr, smallIndex, length)
}

func heapSort(arr []int, length int) []int {
	for i := (len(arr) - 1) / 2; i >= 0; i-- {
		arr = adjustBigRoot(arr, i, length)
	}
	// 根节点为最大值 将根节点与最后一个叶子节点交换 然后缩减长度 重新adjust
	for length > 0 {
		arr[0], arr[length] = arr[length], arr[0]
		length--
		arr = adjustBigRoot(arr, 0, length)
	}
	return arr
}
```