#include <iostream>
#include <vector>
#include <algorithm>
#include <cstdlib>
#include <ctime>
using namespace std;

// Generate random numbers and sort them
void generateRandomNumbers(vector<int> &arr, int N) {
    srand(time(0));
    for (int i = 0; i < N; i++) {
        arr.push_back(rand() % 1000);
    }
    sort(arr.begin(), arr.end());
}

// Binary Search Algorithm
int binarySearch(const vector<int>& arr, int key) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}

// Helper Binary Search used in Exponential Search
int binarySearchExp(const vector<int>& arr, int left, int right, int key) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key) return mid;
        else if (arr[mid] < key) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

// Exponential Search Algorithm
int exponentialSearch(const vector<int>& arr, int key) {
    if (arr[0] == key) return 0;
    int i = 1;
    while (i < arr.size() && arr[i] <= key)
        i *= 2;
    return binarySearchExp(arr, i / 2, min(i, (int)arr.size() - 1), key);
}

// Main function
int main() {
    int N, key;
    cout << "Enter the number of elements: ";
    cin >> N;
 vector<int> arr;
    generateRandomNumbers(arr, N);
cout << "Sorted Array:\n";
    for (int num : arr) cout << num << " ";
    cout << "\n\nEnter number to search: ";
    cin >> key;
    // Binary Search
    int binaryResult = binarySearch(arr, key);
    if (binaryResult != -1)
cout << "Binary Search: Found at index " << binaryResult << endl;
    else
        cout << "Binary Search: Not found\n";
    // Exponential Search
    int exponentialResult = exponentialSearch(arr, key);
    if (exponentialResult != -1)
cout << "Exponential Search: Found at index "<<exponentialResult<<endl;
    else
        cout << "Exponential Search: Not found\n";
    return 0;
}
