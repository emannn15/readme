Priority-Based Threaded Process Scheduler
This Python script simulates a priority-based process scheduler using the threading module. Each process runs in a separate thread and has a priority that changes dynamically based on the scheduling logic. Processes are executed based on their priority, and the script continues to adjust priorities until all processes complete.

Table of Contents
Overview
How It Works
Code Walkthrough
Running the Code
Expected Output
Conclusion
Overview
This is a simple example of dynamic priority scheduling created in 2024. It creates multiple processes, each represented by a thread. Each process has:

ID: A unique identifier for the process.
Burst Time: Simulates the time taken to complete.
Priority: Determines the order of execution.
The scheduler chooses the process with the highest priority and simulates running it while increasing its priority over time.

How It Works
Process Creation: Each process has a burst time (simulated by time.sleep) and an initial priority.
Dynamic Scheduling: A scheduling loop continuously checks for the highest priority process. The process with the highest priority is run, and its priority is increased each time it is selected.
Completion: Once a process finishes execution, it is marked as completed and removed from the scheduler.
Code Walkthrough
"""

import threading import time

class Process(threading.Thread): def init(self, id, burst_time, priority): super().init() self.id = id self.burst_time = burst_time self.priority = priority self.completed = False

def run(self):
    """Simulates the execution of the process."""
    time.sleep(self.burst_time)
    self.completed = True
    print(f"Process ID: {self.id} completed execution.")
def schedule_processes(processes): """Schedules and runs processes based on their priority.""" for p in processes: p.start()

while processes:
    # Select the process with the highest priority
    p = max(processes, key=lambda p: p.priority)
    
    if p.completed:
        processes.remove(p)
    else:
        print(f"Running process ID: {p.id} (Priority: {p.priority})")
        p.priority += 1  # Increase priority of the running process
    time.sleep(1)  # Pause for a second before the next scheduling cycle
Entry point to schedule processes
if name == "main": # Create a list of processes with varying burst times and priorities process_list = [ Process(1, 4, 1), Process(2, 3, 2), Process(3, 2, 1) ] schedule_processes(process_list)

"""

Running the Code
To run the script, ensure you have Python installed on your machine. Save the script as scheduler.py and execute it using the command:

python scheduler.py
