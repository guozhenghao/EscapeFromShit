# Two Sum 两数之和
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

**说明：**你不能倾斜容器，且 n 的值至少为 2。

**示例:**
```
输入：[1,8,6,2,5,4,8,3,7]
输出：49
```

**题解:**
```golang
// 双指针
// 面积=距离*高度(短边) 将短边向内移动
func maxArea(height []int) int {
    if len(height) < 2 {
		return 0
	}
    startIndex, endIndex, result := 0, len(height) -1, 0
    for startIndex < endIndex {
        if height[startIndex] < height[endIndex]{
            result = max(result,height[startIndex] * (endIndex-startIndex))
            startIndex += 1
        }else{
            result = max(result,height[endIndex] * (endIndex-startIndex))
            endIndex -= 1
        }
    }
    return result
}
func max(area1, area2 int) int {
    if area1 < area2 {
        return area2
    }
    return area1
}
```