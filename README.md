# Subarray-Sum-Target-Checker
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

// Function to check for subarray with a given sum and print it
bool findSubarrayWithSum(vector<int>& arr, int targetSum) {
    unordered_map<int, int> prefixSumIndex;
    int currentSum = 0;

    for (int i = 0; i < arr.size(); ++i) {
        currentSum += arr[i];

        // If currentSum itself equals the target
        if (currentSum == targetSum) {
            cout << "Subarray found from index 0 to " << i << ": ";
            for (int j = 0; j <= i; ++j)
                cout << arr[j] << " ";
            cout << endl;
            return true;
        }

        // If currentSum - targetSum is found in map
        if (prefixSumIndex.find(currentSum - targetSum) != prefixSumIndex.end()) {
            int start = prefixSumIndex[currentSum - targetSum] + 1;
            cout << "Subarray found from index " << start << " to " << i << ": ";
            for (int j = start; j <= i; ++j)
                cout << arr[j] << " ";
            cout << endl;
            return true;
        }

        // Store currentSum with index if not already present
        if (prefixSumIndex.find(currentSum) == prefixSumIndex.end())
            prefixSumIndex[currentSum] = i;
    }

    cout << "No subarray with the given sum found.\n";
    return false;
}

int main() {
    int n, target, choice;

    cout << " SUBARRAY SUM TARGET CHECKER \n";

    do {
        cout << "\nEnter the number of elements in the array: ";
        cin >> n;

        if (n <= 0) {
            cout << " Array size must be positive.\n";
            continue;
        }

        vector<int> array(n);
        cout << "Enter " << n << " elements:\n";
        for (int i = 0; i < n; ++i) {
            cout << "Element " << i + 1 << ": ";
            cin >> array[i];
        }

        cout << "Enter the target sum: ";
        cin >> target;

        // Check subarray
        findSubarrayWithSum(array, target);

        // Ask if the user wants to run again
        cout << "\nDo you want to check another array? (1 = Yes, 0 = No): ";
        cin >> choice;

    } while (choice == 1);

    cout << "\n Thank you for using the Subarray Sum Target Checker!\n";

    return 0;
}
