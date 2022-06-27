```golang
func strStr(haystack string, needle string) int {
    nextArr := make([]int,len(needle))
    for left,right := 0,1;right < len(needle);right++{
        for left >0&& needle[left] != needle[right]{
            left = nextArr[left-1]
        }
        if needle[left] == needle[right]{
            left += 1
        }
        nextArr[right] = left
    }
    for hayIndex,needleIndex := 0,0;hayIndex<len(haystack);hayIndex++{
        for needleIndex > 0 && haystack[hayIndex] != needle[needleIndex]{
            needleIndex = nextArr[needleIndex-1]
        }
        if haystack[hayIndex] == needle[needleIndex]{
            needleIndex+=1
        }
        if needleIndex == len(needle){
            return hayIndex - needleIndex + 1
        }
    }
    return -1
}
```