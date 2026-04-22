```c
Name: Jash Chauhan
PRN: 24070521242
```

# Experiment 8: FIFO Page Replacement Algorithm

## Aim
To implement FIFO page replacement algorithm.

***

## Theory
Page replacement is required when a page fault occurs and all memory frames are already full.  
In FIFO (First In First Out) page replacement, the page that entered memory first is removed first.  
It is simple to implement using a circular queue or pointer, but it may suffer from Belady's Anomaly, where increasing the number of frames can sometimes increase page faults.

***

## Formulae
- Hit Ratio = Total Hits / Total Page References
- Page Fault Rate = Total Page Faults / Total Page References

***

## Compilation & Execution (Linux):
```c
Step 1: Create file using vim
         vim fifo_1242.c

Step 2: Compile the program
         gcc fifo_1242.c

Step 3: Run the program
         ./a.out
```

## Code
```c
#include <stdio.h>

int main() {
    int pages[50], frames[10];
    int n, f, i, j, k = 0;
    int page_faults = 0, hits = 0;
    int found;

    printf("Enter number of pages: ");
    scanf("%d", &n);

    printf("Enter page reference string:\n");
    for (i = 0; i < n; i++) {
        scanf("%d", &pages[i]);
    }

    printf("Enter number of frames: ");
    int temp;
    while ((temp = getchar()) != '\n' && temp != EOF);
    scanf("%d", &f);

    for (i = 0; i < f; i++) {
        frames[i] = -1;
    }

    printf("\nPage Replacement Process:\n");

    for (i = 0; i < n; i++) {
        found = 0;

        for (j = 0; j < f; j++) {
            if (frames[j] == pages[i]) {
                found = 1;
                break;
            }
        }

        if (found == 0) {
            frames[k] = pages[i];
            k = (k + 1) % f;
            page_faults++;
        } else {
            hits++;
        }

        printf("Page %d -> ", pages[i]);
        for (j = 0; j < f; j++) {
            if (frames[j] != -1)
                printf("%d ", frames[j]);
            else
                printf("- ");
        }

        if (found)
            printf(" (Hit)");
        else
            printf(" (Fault)");

        printf("\n");
    }

    printf("\nTotal Page Faults = %d\n", page_faults);
    printf("Total Hits = %d\n", hits);
    printf("Hit Ratio  = %.2f\n", (float)hits / n);
    printf("Fault Rate = %.2f\n", (float)page_faults / n);

    return 0;
}
```

## Output
```c
Output:
Enter number of pages: 20
Enter page reference string:
7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1
Enter number of frames: 3

## Page Replacement Process

Page           | 7 | 0 | 1 | 2 | 0 | 3 | 0 | 4 | 2 | 3  | 0  | 3  | 2  | 1  | 2  | 0  | 1  | 7  | 0  | 1  |

| Frame / Step | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
|--------------|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|
| Frame 1      | 7 | 7 | 7 | 2 | 2 | 2 | 2 | 4 | 4 | 4  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 7  | 7  | 7  |
| Frame 2      | - | 0 | 0 | 0 | 0 | 3 | 3 | 3 | 2 | 2  | 2  | 2  | 2  | 1  | 1  | 1  | 1  | 1  | 0  | 0  |
| Frame 3      | - | - | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 3  | 3  | 3  | 3  | 3  | 2  | 2  | 2  | 2  | 2  | 1  |
| Status       | F | F | F | F | H | F | F | F | F | F  | F  | H  | H  | F  | F  | H  | H  | F  | F  | F  |

Total Page Faults = 15
Total Hits = 5
Hit Ratio  = 0.25
Fault Rate = 0.75
```