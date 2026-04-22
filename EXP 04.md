```c
Name: Ritika Bhoyar
PRN: 24070521225
```

# Experiment 4: FCFS CPU Scheduling Algorithm

## Aim
To write a C program to implement FCFS CPU scheduling algorithm.

---

## Theory
First Come First Served (FCFS) is the simplest CPU scheduling algorithm.
Processes are scheduled in the order they arrive in the ready queue.
It is a non-preemptive algorithm, meaning once a process starts execution, it continues until it finishes.

---

## Formulae
- Completion Time (CT) = Time at which process finishes execution
- Turnaround Time (TAT) = CT - Arrival Time (AT)
- Waiting Time (WT) = TAT - Burst Time (BT)
- Average Waiting Time = Sum of all WT / n
- Average Turnaround Time = Sum of all TAT / n
- Throughput = Total processes / Schedule Length

---

## Compilation & Execution (Linux):
```c
Step 1: Create file using vim
         vim fcfs_1225.c

Step 2: Compile the program
         gcc fcfs_1225.c

Step 3: Run the program
         ./a.out
```

## Code
```c
#include <stdio.h>

void calculateTimes(int n, int at[], int bt[]) {
    int wt[n], tat[n], ct[n];
    float total_wt = 0, total_tat = 0;

    ct[0] = at[0] + bt[0];
    for (int i = 1; i < n; i++) {
        if (at[i] > ct[i-1]) {
            ct[i] = at[i] + bt[i];
        } else {
            ct[i] = ct[i-1] + bt[i];
        }
    }

    for (int i = 0; i < n; i++) {
        tat[i] = ct[i] - at[i];
        wt[i]  = tat[i] - bt[i];
        total_wt  += wt[i];
        total_tat += tat[i];
    }

    int schedule_length = ct[n-1] - at[0];
    float throughput = (float)n / schedule_length;

    printf("\nProc\tAT\tBT\tCT\tTAT\tWT\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\t%d\n", i+1, at[i], bt[i], ct[i], tat[i], wt[i]);
    }

    printf("\n--- Performance Metrics ---\n");
    printf("Average Waiting Time:    %.2f\n", total_wt / n);
    printf("Average Turnaround Time: %.2f\n", total_tat / n);
    printf("Schedule Length:         %d units\n", schedule_length);
    printf("Throughput:              %.4f processes/unit time\n", throughput);

    printf("\n--- Gantt Chart ---\n");
    printf("%d", at[0]);
    for (int i = 0; i < n; i++) {
        printf(" --[ P%d ]-- %d", i+1, ct[i]);
    }
    printf("\n");
}

int main() {
    int n;
    printf("Enter number of processes: ");
    if (scanf("%d", &n) != 1 || n <= 0) return 1;

    int at[n], bt[n];
    for (int i = 0; i < n; i++) {
        printf("Enter Arrival Time and Burst Time for P%d: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
    }

    calculateTimes(n, at, bt);
    return 0;
}
```

## Output
```
Output:
 Enter number of processes: 5
 Enter Arrival Time and Burst Time for P1: 0 4
 Enter Arrival Time and Burst Time for P2: 1 5
 Enter Arrival Time and Burst Time for P3: 2 2
 Enter Arrival Time and Burst Time for P4: 3 3
 Enter Arrival Time and Burst Time for P5: 4 6

 Proc  AT  BT  CT  TAT  WT
 P1     0   4   4    4   0
 P2     1   5   9    8   3
 P3     2   2  11    9   7
 P4     3   3  14   11   8
 P5     4   6  20   16  10

 Average Waiting Time:    5.60
 Average Turnaround Time: 9.60
 Schedule Length:         20 units
 Throughput:              0.2500 processes/unit time

 Gantt Chart:
 0 --[ P1 ]-- 4 --[ P2 ]-- 9 --[ P3 ]-- 11 --[ P4 ]-- 14 --[ P5 ]-- 20
```
