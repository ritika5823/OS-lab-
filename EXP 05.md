```c
Name: Jash Chauhan
PRN: 24070521242
```

# Experiment 5: SJF CPU Scheduling Algorithm

## Aim
To write a C program to implement SJF CPU scheduling algorithm.

## Theory
Shortest Job First (SJF) is a CPU scheduling algorithm in which the process with the smallest burst time is selected next.  
It can be used in two modes: non-preemptive SJF, where a process runs until completion, and preemptive SJF, also called SRTF, where a running process can be interrupted if a shorter remaining job arrives.  
SJF generally gives the minimum average waiting time among scheduling algorithms, but it requires burst time knowledge in advance.

## Formulae
- Turnaround Time (TAT) = Finish Time - Arrival Time
- Waiting Time (WT) = TAT - Burst Time
- Throughput = Total Processes / Schedule Length

## Compilation & Execution (Linux)
```c
Step 1: Create file using vim
         vim sjf_1242.c

Step 2: Compile the program
         gcc sjf_1242.c

Step 3: Run the program
         ./a.out
```

## Code
```c
#include <stdio.h>
#include <stdbool.h>
#include <limits.h>

struct Process {
    int pid, arrival, burst, remaining, finish, wait, tat;
    bool completed;
};

void calculateMetrics(struct Process p[], int n, int mode) {
    int completed = 0, curr_time = 0;
    float total_wait = 0, total_tat = 0;
    int gantt_p[100], gantt_t[100], g_idx = 0;

    while (completed != n) {
        int idx = -1;
        int min_val = INT_MAX;

        for (int i = 0; i < n; i++) {
            if (p[i].arrival <= curr_time && !p[i].completed) {
                if (p[i].remaining < min_val) {
                    min_val = p[i].remaining;
                    idx = i;
                }
                if (p[i].remaining == min_val) {
                    if (p[i].arrival < p[idx].arrival) idx = i;
                }
            }
        }

        if (idx != -1) {
            if (g_idx == 0 || gantt_p[g_idx - 1] != p[idx].pid) {
                gantt_p[g_idx] = p[idx].pid;
                gantt_t[g_idx] = curr_time;
                g_idx++;
            }

            if (mode == 1) {
                p[idx].remaining--;
                curr_time++;
                if (p[idx].remaining == 0) {
                    p[idx].finish = curr_time;
                    p[idx].tat = p[idx].finish - p[idx].arrival;
                    p[idx].wait = p[idx].tat - p[idx].burst;
                    p[idx].completed = true;
                    completed++;
                }
            } else {
                curr_time += p[idx].remaining;
                p[idx].remaining = 0;
                p[idx].finish = curr_time;
                p[idx].tat = p[idx].finish - p[idx].arrival;
                p[idx].wait = p[idx].tat - p[idx].burst;
                p[idx].completed = true;
                completed++;
            }
        } else {
            curr_time++;
        }
    }
    gantt_t[g_idx] = curr_time;

    printf("\n%-5s | %-8s | %-6s | %-7s | %-4s | %-4s\n",
           "PID", "Arrival", "Burst", "Finish", "TAT", "Wait");
    printf("--------------------------------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("P%-4d | %-8d | %-6d | %-7d | %-4d | %-4d\n",
               p[i].pid, p[i].arrival, p[i].burst, p[i].finish, p[i].tat, p[i].wait);
        total_wait += p[i].wait;
        total_tat += p[i].tat;
    }

    printf("\n--- Gantt Chart ---\n ");
    for (int i = 0; i < g_idx; i++) printf("------- ");
    printf("\n");
    for (int i = 0; i < g_idx; i++) printf("  P%-4d ", gantt_p[i]);
    printf("\n ");
    for (int i = 0; i < g_idx; i++) printf("------- ");
    printf("\n%-8d", gantt_t[0]);
    for (int i = 1; i <= g_idx; i++) printf("%8d", gantt_t[i]);

    printf("\n\nAverage Waiting Time: %.2f\n", total_wait / n);
    printf("Average Turnaround Time: %.2f\n", total_tat / n);
    printf("Schedule Length: %d units\n", curr_time);
    printf("Throughput: %.3f processes/unit\n", (float)n / curr_time);
}

int main() {
    int n, mode;
    printf("Enter number of processes: ");
    scanf("%d", &n);
    struct Process p[n];

    for (int i = 0; i < n; i++) {
        p[i].pid = i + 1;
        printf("Enter Arrival and Burst time for P%d: ", i + 1);
        scanf("%d %d", &p[i].arrival, &p[i].burst);
        p[i].remaining = p[i].burst;
        p[i].completed = false;
    }

    printf("\nChoose Mode:\n1. Preemptive (SRTF)\n2. Non-Preemptive (SJF)\nSelection: ");
    scanf("%d", &mode);

    calculateMetrics(p, n, mode);
    return 0;
}
```

## Output
```c
Output:
Enter number of processes: 6
Enter Arrival and Burst time for P1: 0 6
Enter Arrival and Burst time for P2: 1 2
Enter Arrival and Burst time for P3: 2 4
Enter Arrival and Burst time for P4: 3 1
Enter Arrival and Burst time for P5: 4 3
Enter Arrival and Burst time for P6: 6 5
Selection: 2

PID   | Arrival  | Burst  | Finish  | TAT  | Wait
--------------------------------------------------------
P1    | 0        | 6      | 6       | 6    | 0
P2    | 1        | 2      | 9       | 8    | 6
P3    | 2        | 4      | 16      | 14   | 10
P4    | 3        | 1      | 7       | 4    | 3
P5    | 4        | 3      | 12      | 8    | 5
P6    | 6        | 5      | 21      | 15   | 10

Average Waiting Time: 5.67
Average Turnaround Time: 9.17
Schedule Length: 21 units
Throughput: 0.286 processes/unit
```