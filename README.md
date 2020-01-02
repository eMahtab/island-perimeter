# Island Perimeter
## https://leetcode.com/problems/island-perimeter

You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

 

Example:

Input:
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

Output: 16

Explanation: The perimeter is the 16 yellow stripes in the image below:

![Island Perimeter](island.png?raw=true "Island Perimeter")

## Approach :
We can solve this problem, by iterating over each element of the 2D grid, and if we see a 1(land), we add its perimeter to the final result. Now to calculate the perimeter of a land, we see its 4 adjacent cells (left, right, up, down). 

Note that while calculating the perimeter of a land, only the adjacent cells that are water or if the land's surronding is outside the grid (remember outside the grid its all water), then only it will add to perimeter.

### Implementation

```java
public class App {

    public static void main(String[] args) {
		int[][] grid = {
				 {0,1,0,0},
				 {1,1,1,0},
				 {0,1,0,0},
				 {1,1,0,0}
		};
		System.out.println("Perimeter : "+islandPerimeter(grid));
    }
	
    public static int islandPerimeter(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        
        int perimeter = 0;
        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){
                if(grid[i][j] == 1){
                    perimeter += getPerimeter(grid, i, j);
                }
            }
        }
        return perimeter;
    }
    
    public static int getPerimeter(int[][] grid, int row, int column){
        int perimeter = 0;
        
        if( (column - 1) < 0 || grid[row][column - 1] == 0)
            perimeter++;
        if( (column + 1) == grid[0].length || grid[row][column + 1] == 0)
            perimeter++;
        if( (row - 1) < 0 || grid[row - 1][column] == 0)
            perimeter++;
        if( (row + 1) == grid.length || grid[row + 1][column] == 0)
            perimeter++;
      
        return perimeter;
    }
}

```
Above implementation have runtime complexity of O(m * n) and space complexity of O(1), where m is the number of rows in the input grid and n is the number of columns in the input grid.

```
Runtime Complexity = O(m * n)
Space Complexity   = O(1) 
```

## References :
https://massivealgorithms.blogspot.com/2016/11/leetcode-463-island-perimeter.html
