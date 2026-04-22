```c
Name: Ritika Bhoyar
PRN: 24070521225
```

# Experiment 6: Priority Based CPU Scheduling Algorithm

## Aim
To write a C program to implement Priority based CPU scheduling algorithm.

***

## Theory
Priority Scheduling is a CPU scheduling algorithm in which each process is assigned a priority value, and the CPU is allocated to the process with the highest priority.  
Two conventions are commonly used: lower number means higher priority, or higher number means higher priority.  
It can be preemptive or non-preemptive. In preemptive mode, a higher priority arriving process can interrupt the currently running process, while in non-preemptive mode, the running process completes first.

***

## Formulae
- Turnaround Time (TAT) = Completion Time - Arrival Time
- Waiting Time (WT) = TAT - Burst Time
- Throughput = Total Processes / Schedule Length

***

## Compilation & Execution (Linux):
```c
Step 1: Create file using vim
         vim priority_1225.c

Step 2: Compile the program
         gcc priority_1225.c

Step 3: Run the program
         ./a.out
```

## Code
```c
#include <stdio.h>
#include <stdbool.h>
#include <limits.h>

struct Process {
    int id, arrival, burst, priority, remaining;
    int completion, waiting, turnaround;
    bool completed;
};

void calculateStats(struct Process p[], int n) {
    float total_wt = 0, total_tat = 0;
    int min_arrival = INT_MAX, max_completion = 0;

    printf("\nID\tArr\tBurst\tPrio\tComp\tTAT\tWT\n");
    for (int i = 0; i < n; i++) {
        p[i].turnaround = p[i].completion - p[i].arrival;
        p[i].waiting    = p[i].turnaround - p[i].burst;
        total_wt  += p[i].waiting;
        total_tat += p[i].turnaround;

        if (p[i].arrival < min_arrival) min_arrival = p[i].arrival;
        if (p[i].completion > max_completion) max_completion = p[i].completion;

        printf("P%d\t%d\t%d\t%d\t%d\t%d\t%d\n",
               p[i].id, p[i].arrival, p[i].burst, p[i].priority,
               p[i].completion, p[i].turnaround, p[i].waiting);
    }

    int schedule_length = max_completion - min_arrival;
    printf("\nAverage Waiting Time:    %.2f\n", total_wt / n);
    printf("Average Turnaround Time: %.2f\n", total_tat / n);
    printf("Throughput: %.3f processes/unit time\n",
           (float)n / (schedule_length ? schedule_length : 1));
}

int main() {
    int n, mode, prio_type;
    printf("Enter number of processes: ");
    scanf("%d", &n);
    struct Process p[n];

    for (int i = 0; i < n; i++) {
        p[i].id = i + 1;
        printf("P%d [Arrival, Burst, Priority]: ", i + 1);
        scanf("%d %d %d", &p[i].arrival, &p[i].burst, &p[i].priority);
        p[i].remaining = p[i].burst;
        p[i].completed = false;
    }

    printf("\nPriority Logic:\n0. 0 is Highest Priority (Lower # is better)\n");
    printf("1. 0 is Lowest Priority (Higher # is better)\nChoice: ");
    scanf("%d", &prio_type);

    printf("Mode:\n1. Non-Preemptive\n2. Preemptive\nChoice: ");
    scanf("%d", &mode);

    int current_time = 0, completed_count = 0;
    int timeline[500];

    while (completed_count < n) {
        int idx = -1;
        int best_prio = (prio_type == 0) ? INT_MAX : INT_MIN;

        for (int i = 0; i < n; i++) {
            if (p[i].arrival <= current_time && !p[i].completed) {
                if (prio_type == 0) {
                    if (p[i].priority < best_prio) { best_prio = p[i].priority; idx = i; }
                } else {
                    if (p[i].priority > best_prio) { best_prio = p[i].priority; idx = i; }
                }
            }
        }

        if (idx != -1) {
            timeline[current_time] = p[idx].id;
            if (mode == 1) {
                for (int i = 0; i < p[idx].burst; i++) {
                    timeline[current_time++] = p[idx].id;
                }
                p[idx].completion = current_time;
                p[idx].completed = true;
                completed_count++;
                current_time--;
            } else {
                p[idx].remaining--;
                if (p[idx].remaining == 0) {
                    p[idx].completion = current_time + 1;
                    p[idx].completed = true;
                    completed_count++;
                }
            }
        } else {
            timeline[current_time] = -1;
        }
        current_time++;
    }

    printf("\nGantt Chart:\n");
    for (int i = 0; i < current_time; i++) {
        if (timeline[i] == -1) printf("| IDL ");
        else printf("| P%d  ", timeline[i]);
    }
    printf("|\n0");
    for (int i = 1; i <= current_time; i++) printf("%6d", i);
    printf("\n");

    calculateStats(p, n);
    return 0;
}
```

## Output
```c
Output:
Enter number of processes: 5
P1 [Arrival, Burst, Priority]: 0 6 4
P2 [Arrival, Burst, Priority]: 1 7 5
P3 [Arrival, Burst, Priority]: 2 2 8
P4 [Arrival, Burst, Priority]: 3 3 7
P5 [Arrival, Burst, Priority]: 5 5 6
Choice: 0
Choice: 1

Gantt Chart:
| P1  | P1  | P1  | P1  | P1  | P1  | P2  | P2  | P2  | P2  | P2  | P2  | P2  | P5  | P5  | P5  | P5  | P5  | P4  | P4  | P4  | P3  | P3  |
0     1     2     3     4     5     6     7     8     9    10    11    12    13    14    15    16    17    18    19    20    21    22    23

## Process Table

| Process ID | Arrival Time | Burst Time | Priority | Completion Time | Turnaround Time | Waiting Time |
|------------|--------------|------------|----------|-----------------|-----------------|--------------|
| P1         | 0            | 6          | 4        | 6               | 6               | 0            |
| P2         | 1            | 7          | 5        | 13              | 12              | 5            |
| P3         | 2            | 2          | 8        | 23              | 21              | 19           |
| P4         | 3            | 3          | 7        | 21              | 18              | 15           |
| P5         | 5            | 5          | 6        | 18              | 13              | 8            |

Average Waiting Time:    9.40
Average Turnaround Time: 14.00
Throughput: 0.217 processes/unit time
```
