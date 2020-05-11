## 学习笔记
&emsp;&emsp;先上迭代模板  
``` python
def recursion(level, param1, param2, ...): 
    # recursion terminator 
    if level > MAX_LEVEL: 
	   process_result 
	   return 
    # process logic in current level 
    process(level, data...) 
    # drill down 
    self.recursion(level + 1, p1, ...) 
    # reverse the current level status if needed
```

&emsp;&emsp;分治也好，回溯也罢，都是基于递归，在process 那一步通过不同的代码实现不同的功能而已。都是基于递归的将原问题不断划分为一个个子问题的过程。  
&emsp;&emsp;尽管本周是回溯、分治专场，但是我依然学到了很多递归之外的解题方法。重点体现在 [leetcode_77_组合](https://leetcode-cn.com/problems/combinations/) 中,该题除了通过常规的回溯求解外，我还学到两种迭代的枚举方法，各有各的巧妙之处，时间上也要比单纯回溯要少。但正如一位大佬在 [**打酱油的**](https://leetcode-cn.com/u/wang-yan-19/) 在一道题解下评论的那样，“代码越少，往往说明思路trick的点越多”，递归的方法是很多问题的通解，其他很多方法虽然也有优势，但是一般人难以想到，而且只是单单适合于某种固定的问题。所以说，掌握问题还得从通法，在通法基础上，再做延申。