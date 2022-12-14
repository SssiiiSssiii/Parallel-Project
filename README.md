## Description
* By starting at the top of the triangle below and moving to `adjacent` numbers on the row below, the maximum total from top to bottom is `23`.                                 
![Alt text](/Images/tr2.png)                 



* That is, 3 + 7 + 4 + 9 = 23.

* Find the maximum total from top to bottom of the triangle below   
![Alt text](/Images/tr.png)   

## Best Sequential Code using Dynamic Programming

```c
#include <bits/stdc++.h>
using namespace std;

int find_Max_Sum_Adjacent(int triangle[15][15]){
    for (int row = 13; row >= 0; row--) {
        for (int col = 0; col < 15; col++)
            triangle[row][col] += max(triangle[row + 1][col], triangle[row + 1][col + 1]);
    }
    return triangle[0][0];
}

int main() {
    int triangle[15][15] = {
        {75},
        {95,64},
        {17,47,82},
        {18,35,87,10},
        {20,4,82,47,65},
        {19,1,23,75,3,34},
        {88,2,77,73,7,63,67},
        {99,65,4,28,6,16,70,92},
        {41,41,26,56,83,40,80,70,33},
        {41,48,72,33,47,32,37,16,94,29},
        {53,71,44,65,25,43,91,52,97,51,14},
        {70,11,33,28,77,73,17,78,39,68,17,57},
        {91,71,52,38,17,14,91,43,58,50,27,29,48},
        {63,66, 4,68,89,53,67,30,73,16,69,87,40,31},
        {4,62,98,27,23,9,70,98,73,93,38,53,60,4,23}
    };

    cout << find_Max_Sum_Adjacent(triangle);

}
```
## Running Time for the best sequential solution 
* O(rows * cols) = O(rows<sup>2</sup>) 
* Where cols =  Number of of rows

# Parallel Code using OpenMP
```c
#include <bits/stdc++.h>
using namespace std;

int find_Max_Sum_Adjacent(int triangle[15][15]){

    #pragma omp parallel for
    for (int row = 13; row >= 0; row--) {
        for (int col = 0; col < 15; col++)
            triangle[row][col] += max(triangle[row + 1][col], triangle[row + 1][col + 1]);
    }
    return triangle[0][0];
}

int main() {
    int triangle[15][15] = {
        {75},
        {95,64},
        {17,47,82},
        {18,35,87,10},
        {20,4,82,47,65},
        {19,1,23,75,3,34},
        {88,2,77,73,7,63,67},
        {99,65,4,28,6,16,70,92},
        {41,41,26,56,83,40,80,70,33},
        {41,48,72,33,47,32,37,16,94,29},
        {53,71,44,65,25,43,91,52,97,51,14},
        {70,11,33,28,77,73,17,78,39,68,17,57},
        {91,71,52,38,17,14,91,43,58,50,27,29,48},
        {63,66,4,68,89,53,67,30,73,16,69,87,40,31},
        {4,62,98,27,23,9,70,98,73,93,38,53,60,4,23}
    };

    cout << find_Max_Sum_Adjacent(triangle);

}

```

### Answer
`1074`

## Running Time for the parallel solution 
* O(rows) = Number of rows


## Performance Measuring:
* Speedup =  Running time for the best sequential solution / Running time for the parallel solution = rows<sup>2</sup> / rows = `rows`
* Cost = Number of processors * Running time for the parallel solution = Number of columns * rows = rows * rows = `rows`<sup>2</sup>
* Efficiency = Speedup /  Number of processors = rows / cols = rows / rows = `1`                 
* It is cost optimal, because:      Cost <= Running time for the best sequential solution = `rows`<sup>2</sup> 
