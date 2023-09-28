## Sum of 2D Array elements Using pointer 
```cpp
 #include <iostream>
using namespace std;

int sum(int* ptr, int row, int col) {
    int total = 0;
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            total += *(ptr + i * col + j);
        }
    }
    return total;
}

int main() {
    int row, col;
    cout << "Enter the number of Rows and Columns: ";
    cin >> row >> col;

    int arr[row][col];

    cout << "Enter the array elements: ";
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            cin >> arr[i][j];
        }
    }

    cout << "Matrix: \n";
    for (int i = 0; i < row; i++) {
        cout << "{";
        for (int j = 0; j < col; j++) {
            cout << arr[i][j] << " ";
        }
        cout << "}";
        cout << endl;
    }

    int ans = sum(&arr[0][0], row, col);
    cout << "Sum of Array elements: " << ans;

    return 0;
}```
