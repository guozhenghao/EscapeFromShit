```golang
func mergeSort(arr []int) []int {
	lenArr := len(arr)
	if lenArr == 1 {
		return arr
	}
	mid := lenArr / 2
	return merge(mergeSort(arr[:mid]), mergeSort(arr[mid:]))
}

func merge(arr1, arr2 []int) []int {
	result := make([]int, 0, len(arr1)+len(arr2))
	for len(arr1) != 0 && len(arr2) != 0 {
		if arr1[0] < arr2[0] {
			result = append(result, arr1[0])
			arr1 = arr1[1:]
		} else {
			result = append(result, arr2[0])
			arr2 = arr2[1:]
		}
	}
	if len(arr1) != 0 {
		result = append(result, arr1...)
	}
	if len(arr2) != 0 {
		result = append(result, arr2...)
	}
	return result
}

```