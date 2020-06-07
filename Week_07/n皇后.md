``` java
class Solution {
    public int numIslands(char[][] grid) {
        if (grid.length == 0)   return 0;
        int sum = 0;
        for (int i = 0; i < grid.length; ++i) {
            for (int j = 0; j < grid[0].length; ++j) {
                if (grid[i][j] == '1') {
                    ++sum;
                    DFS(grid, i, j);
                }
            }
        }
        return sum;
    }
    public void DFS(char[][] grid, int x, int y) {
        if (x < 0 || x >= grid.length || y < 0 || y >= grid[0].length || grid[x][y] == '0')
            return;
        
        grid[x][y] = '0';
        DFS(grid, x - 1, y);
        DFS(grid, x + 1, y);
        DFS(grid, x, y - 1);
        DFS(grid, x, y + 1);
    }
}
```