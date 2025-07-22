# ADSA-PRAC-1
To Implement Merge Sort

#include <stdio.h>

#define MAX 100

int a[MAX], b[MAX];

void Merge(int a[], int lb, int mid, int ub) {
    int i = lb;
    int j = mid + 1;
    int k = lb;  // Corrected: start from lb, not ub

    while (i <= mid && j <= ub) {
        if (a[i] <= a[j]) {
            b[k] = a[i];
            i++;
        } else {
            b[k] = a[j];
            j++;
        }
        k++;
    }

    // Copy remaining elements
    if (i > mid) {
        while (j <= ub) {
            b[k] = a[j];
            j++;
            k++;
        }
    } else {
        while (i <= mid) {
            b[k] = a[i];
            i++;
            k++;
        }
    }

    // Copy back to original array
    for (k = lb; k <= ub; k++) {
        a[k] = b[k];
    }
}

void MergeSort(int a[], int lb, int ub) {
    if (lb < ub) {
        int mid = (lb + ub) / 2;
        MergeSort(a, lb, mid);
        MergeSort(a, mid + 1, ub);
        Merge(a, lb, mid, ub);
    }
}

int main() {
    int n, i;

    printf("Enter the number of elements: ");
    scanf("%d", &n);

    if (n > MAX) {
        printf("Limit exceeded. Max allowed is %d.\n", MAX);
        return 1;
    }

    printf("Enter %d elements:\n", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }

    MergeSort(a, 0, n - 1);

    printf("Sorted array:\n");
    for (i = 0; i < n; i++) {
        printf("%d ", a[i]);
    }
    printf("\n");

    return 0;
}
