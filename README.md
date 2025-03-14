#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define MAX_SIZE 1000

int binarySearch(int arr[], int left, int right, int key) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == key) {
            return mid;
        }
        
        if (arr[mid] < key) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

int main() {
    int key, n, i, result;
    clock_t start_time, end_time;
    double time_taken;

    printf("Enter the number of elements (up to %d): ", MAX_SIZE);
    scanf("%d", &n);

    if (n > MAX_SIZE) {
        printf("Number of elements exceeds the maximum size of %d\n", MAX_SIZE);
        return 1;
    }

    int a[MAX_SIZE];

    srand(time(0));
    for (i = 0; i < n; i++) {
        a[i] = rand() % 100;
    }

    printf("Array elements (sorted):\n");
    for (i = 0; i < n; i++) {
        printf("%d ", a[i]);
    }
    printf("\n");

    key = rand() % 100;
    printf("Random key to search for: %d\n", key);

    start_time = clock();
    result = binarySearch(a, 0, n - 1, key);
    end_time = clock();

    time_taken = ((double)(end_time - start_time)) / CLOCKS_PER_SEC;

    if (result != -1) {
        printf("Element %d is found at index %d.\n", key, result);
    } else {
        printf("Element not found\n");
    }

    printf("Time Taken in seconds: %f\n", time_taken);

    return 0;
}
