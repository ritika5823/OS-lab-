```c
Name: Ritika Bhoyar
PRN: 24070521225
```

# Experiment 7: Banker's Algorithm for Deadlock Avoidance

## Aim
To implement Banker’s Algorithm to find the safe state for deadlock.

***

## Theory
The Banker's Algorithm is a deadlock avoidance method that checks whether allocating resources keeps the system in a safe state.
It uses the Allocation, Max, Available, and Need matrices, where Need is calculated as Max minus Allocation.
If a safe sequence exists, the system is in a safe state; otherwise, it is unsafe.

***

## Formulae
- Need[i][j] = Max[i][j] - Allocation[i][j]
- System is SAFE if a safe sequence exists. 
- System is UNSAFE if no safe sequence can be found. 

***

## Compilation & Execution (Linux):
```c
Step 1: Create file using vim
         vim bankers_1225.c

Step 2: Compile the program
         gcc bankers_1225.c -o bankers_1242

Step 3: Run the program
         ./bankers_1242
```

## Code
```c
#include <stdio.h>

int main() {
    int n, m, i, j, k;

    printf("Enter number of processes: ");
    scanf("%d", &n);
    printf("Enter number of resources: ");
    scanf("%d", &m);

    int alloc[n][m], max[n][m], avail[m], need[n][m];
    int finish[n], safeSeq[n];

    printf("Enter Allocation Matrix:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            scanf("%d", &alloc[i][j]);
        }
    }

    printf("Enter Max Matrix:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            scanf("%d", &max[i][j]);
        }
    }

    printf("Enter Available Resources:\n");
    for (i = 0; i < m; i++) {
        scanf("%d", &avail[i]);
    }

    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            need[i][j] = max[i][j] - alloc[i][j];
        }
    }

    printf("\nProcess\tAllocation\tMax\t\tNeed\n");
    for (i = 0; i < n; i++) {
        printf("P%d\t", i);
        for (j = 0; j < m; j++) {
            printf("%d ", alloc[i][j]);
        }
        printf("\t\t");
        for (j = 0; j < m; j++) {
            printf("%d ", max[i][j]);
        }
        printf("\t\t");
        for (j = 0; j < m; j++) {
            printf("%d ", need[i][j]);
        }
        printf("\n");
    }

    for (i = 0; i < n; i++) {
        finish[i] = 0;
    }

    int count = 0;
    while (count < n) {
        int found = 0;
        for (i = 0; i < n; i++) {
            if (finish[i] == 0) {
                int possible = 1;
                for (j = 0; j < m; j++) {
                    if (need[i][j] > avail[j]) {
                        possible = 0;
                        break;
                    }
                }

                if (possible) {
                    safeSeq[count++] = i;
                    for (k = 0; k < m; k++) {
                        avail[k] += alloc[i][k];
                    }
                    finish[i] = 1;
                    found = 1;
                }
            }
        }

        if (!found) {
            break;
        }
    }

    if (count == n) {
        printf("\nSystem is in SAFE state.\n");
        printf("Safe Sequence: ");
        for (i = 0; i < n; i++) {
            printf("P%d", safeSeq[i]);
            if (i != n - 1)
                printf(" -> ");
        }
        printf("\n");
    } else {
        printf("\nSystem is NOT in safe state.\n");
    }

    return 0;
}
```

## Output
```c
Output:

Enter number of processes: 5
Enter number of resources: 3
Enter Allocation Matrix:
0 1 0
2 0 0
3 0 2
2 1 1
0 0 2
Enter Max Matrix:
7 5 3
3 2 2
9 0 2
2 2 2
4 3 3
Enter Available Resources:
3 3 2

Process Allocation      Max             Need
P0      0 1 0           7 5 3           7 4 3
P1      2 0 0           3 2 2           1 2 2
P2      3 0 2           9 0 2           6 0 0
P3      2 1 1           2 2 2           0 1 1
P4      0 0 2           4 3 3           4 3 1

System is in SAFE state.
Safe Sequence: P1 -> P3 -> P4 -> P0 -> P2
```
