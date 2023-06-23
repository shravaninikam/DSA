# Unit 6
--- 
### Pseudo codes/ Codes for Operations on a Sequential File

**1. Creation:**
```cpp
#include <fstream>

void createSequentialFile(const std::string& fileName) {
    std::ofstream file(fileName, std::ios::out); // Open the file in write mode
    file.close(); // Close the file
}
```

**2. Reading:**
```cpp
#include <fstream>
#include <iostream>
#include <string>

void readSequentialFile(const std::string& fileName) {
    std::ifstream file(fileName, std::ios::in); // Open the file in read mode
    std::string record;
    while (std::getline(file, record)) {
        std::cout << record << std::endl; // Display the record
    }
    file.close(); // Close the file
}
```

**3. Insertion:**
```cpp
#include <fstream>

void insertRecord(const std::string& fileName, const std::string& record) {
    std::ofstream file(fileName, std::ios::app); // Open the file in append mode
    file << record << std::endl; // Write the record to the file
    file.close(); // Close the file
}
```

**4. Deletion:**
```cpp
#include <fstream>
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

void deleteRecord(const std::string& fileName, const std::string& targetKey) {
    std::ifstream inputFile(fileName, std::ios::in); // Open the file in read mode
    std::vector<std::string> records;
    std::string record;
    while (std::getline(inputFile, record)) {
        records.push_back(record);
    }
    inputFile.close(); // Close the file

    std::ofstream outputFile(fileName, std::ios::out); // Open the file in write mode
    for (const auto& rec : records) {
        if (rec != targetKey) {
            outputFile << rec << std::endl; // Rewrite the record to the file
        }
    }
    outputFile.close(); // Close the file
}
```

**5. Updating:**
```cpp
#include <fstream>
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

void updateRecord(const std::string& fileName, const std::string& targetKey, const std::string& newRecord) {
    std::ifstream inputFile(fileName, std::ios::in); // Open the file in read mode
    std::vector<std::string> records;
    std::string record;
    while (std::getline(inputFile, record)) {
        records.push_back(record);
    }
    inputFile.close(); // Close the file

    std::ofstream outputFile(fileName, std::ios::out); // Open the file in write mode
    for (const auto& rec : records) {
        if (rec == targetKey) {
            outputFile << newRecord << std::endl; // Write the updated record to the file
        } else {
            outputFile << rec << std::endl; // Rewrite the record to the file
        }
    }
    outputFile.close(); // Close the file
}
```

**6. Searching:**
```cpp
#include <fstream>
#include <iostream>
#include <string>

bool searchRecord(const std::string& fileName, const std::string& targetKey) {
    std::ifstream file(fileName, std::ios::in); // Open the file in read mode
    std::string record;
    while (std::getline(file, record)) {
        if (record == targetKey) {
            file.close(); // Close the file
            return true;
        }
    }
    file.close(); // Close the file
    return false;
}
```

**7. Packing:**
```cpp
#include <fstream>
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

void packRecords(const std::string& fileName) {
    std::ifstream inputFile(fileName, std::ios::in); // Open the file in read mode
    std::vector<std::string> records;
    std::string record;
    while (std::getline(inputFile, record)) {
        records.push_back(record);
    }
    inputFile.close(); // Close the file

    std::ofstream outputFile(fileName, std::ios::out); // Open the file in write mode
    for (const auto& rec : records) {
        if (!rec.empty()) {
            outputFile << rec << std::endl; // Rewrite the non-empty record to the file
        }
    }
    outputFile.close(); // Close the file
}
```

### Write pseudo code for two way merge sort
Here's an implementation of the Two-Way Merge Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

// Function to merge two sorted subarrays into one sorted subarray
void merge(std::vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    std::vector<int> leftArr(n1);
    std::vector<int> rightArr(n2);

    // Copy data to temporary arrays
    for (int i = 0; i < n1; i++) {
        leftArr[i] = arr[left + i];
    }
    for (int j = 0; j < n2; j++) {
        rightArr[j] = arr[mid + 1 + j];
    }

    // Merge the temporary arrays back into arr[]
    int i = 0; // Initial index of first subarray
    int j = 0; // Initial index of second subarray
    int k = left; // Initial index of merged subarray

    while (i < n1 && j < n2) {
        if (leftArr[i] <= rightArr[j]) {
            arr[k] = leftArr[i];
            i++;
        } else {
            arr[k] = rightArr[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of leftArr[], if any
    while (i < n1) {
        arr[k] = leftArr[i];
        i++;
        k++;
    }

    // Copy the remaining elements of rightArr[], if any
    while (j < n2) {
        arr[k] = rightArr[j];
        j++;
        k++;
    }
}

// Function to perform two-way merge sort on the array
void twoWayMergeSort(std::vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        twoWayMergeSort(arr, left, mid);
        twoWayMergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

// Function to print the elements of the array
void printArray(const std::vector<int>& arr) {
    for (const auto& element : arr) {
        std::cout << element << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> arr = {9, 7, 5, 11, 12, 2, 14, 3, 10, 6};
    int n = arr.size();

    std::cout << "Original Array: ";
    printArray(arr);

    twoWayMergeSort(arr, 0, n - 1);

    std::cout << "Sorted Array: ";
    printArray(arr);

    return 0;
}
```

In this code, the `merge` function is responsible for merging two sorted subarrays into one sorted subarray. The `twoWayMergeSort` function performs the two-way merge sort recursively by dividing the array into smaller subarrays until each subarray has only one element. Finally, the `printArray` function is used to print the elements of the array. The main function demonstrates the usage of the merge sort algorithm by initializing an array, performing the sort, and printing the sorted array.

```cpp
 Actual Pseduo code

Procedure Merge(arr, left, mid, right)
    n1 = mid - left + 1
    n2 = right - mid

    Create temporary arrays leftArr[n1] and rightArr[n2]

    // Copy data to temporary arrays
    for i = 0 to n1
        leftArr[i] = arr[left + i]

    for j = 0 to n2
        rightArr[j] = arr[mid + 1 + j]

    // Merge the temporary arrays back into arr[]
    i = 0 // Initial index of first subarray
    j = 0 // Initial index of second subarray
    k = left // Initial index of merged subarray

    while i < n1 and j < n2
        if leftArr[i] <= rightArr[j]
            arr[k] = leftArr[i]
            i = i + 1
        else
            arr[k] = rightArr[j]
            j = j + 1
        k = k + 1

    // Copy the remaining elements of leftArr[], if any
    while i < n1
        arr[k] = leftArr[i]
        i = i + 1
        k = k + 1

    // Copy the remaining elements of rightArr[], if any
    while j < n2
        arr[k] = rightArr[j]
        j = j + 1
        k = k + 1
End Procedure

Procedure TwoWayMergeSort(arr, left, right)
    if left < right
        mid = left + (right - left) / 2

        // Sort first and second halves
        TwoWayMergeSort(arr, left, mid)
        TwoWayMergeSort(arr, mid + 1, right)

        // Merge the sorted halves
        Merge(arr, left, mid, right)
End Procedure

Procedure PrintArray(arr)
    for each element in arr
        print element
    print newline
End Procedure

main()
    arr = [9, 7, 5, 11, 12, 2, 14, 3, 10, 6]
    n = length of arr

    print "Original Array: "
    PrintArray(arr)

    TwoWayMergeSort(arr, 0, n - 1)

    print "Sorted Array: "
    PrintArray(arr)
End Procedure

```

### File Handling

```cpp
#include <iostream>
#include <fstream>
#include <string>

// Function to create a file
void createFile(const std::string& fileName) {
    std::ofstream file(fileName);  // Create a file with the specified fileName

    if (file) {
        std::cout << "File created successfully!" << std::endl;
        file.close();  // Close the file
    } else {
        std::cout << "Error creating file!" << std::endl;
    }
}

// Function to insert a record into the file in append mode
void insertRecord(const std::string& fileName, const std::string& record) {
    std::ofstream file(fileName, std::ios::app);  // Open the file in append mode

    if (file) {
        file << record << std::endl;  // Write the record to the file
        std::cout << "Record inserted successfully!" << std::endl;
        file.close();  // Close the file
    } else {
        std::cout << "Error inserting record!" << std::endl;
    }
}

// Function to search for a specific record in the file
bool searchRecord(const std::string& fileName, const std::string& targetRecord) {
    std::ifstream file(fileName);  // Open the file in read mode

    if (file) {
        std::string record;
        while (std::getline(file, record)) {
            if (record == targetRecord) {
                file.close();  // Close the file
                return true;   // Record found
            }
        }
        file.close();  // Close the file
    }

    return false;  // Record not found
}

int main() {
    std::string fileName = "records.txt";
    std::string record;

    // Create the file
    createFile(fileName);

    // Insert records
    insertRecord(fileName, "John Doe");
    insertRecord(fileName, "Jane Smith");
    insertRecord(fileName, "Mike Johnson");

    // Search for a record
    std::cout << "Enter a record to search: ";
    std::getline(std::cin, record);

    if (searchRecord(fileName, record)) {
        std::cout << "Record found in the file!" << std::endl;
    } else {
        std::cout << "Record not found in the file." << std::endl;
    }

    return 0;
}
```

In this code, the `createFile` function creates a file with the specified `fileName`. The `insertRecord` function opens the file in append mode and inserts a record into it. The `searchRecord` function opens the file in read mode and searches for a specific record. The `main` function demonstrates the usage of these functions by creating a file, inserting records, and searching for a record in the file.



