# Mini_task_scheduler
#Python simulation of CPU scheduling algorithms (FCFS, SJN, RR, Priority) with Gantt chart visualization.
processes = [
    {"pid": "P1", "arrival": 0, "burst": 5, "priority": 2},
    {"pid": "P2", "arrival": 1, "burst": 3, "priority": 1},
    {"pid": "P3", "arrival": 2, "burst": 8, "priority": 3},
]
def fcfs(processes):
    time = 0
    schedule = []
    waiting_time = 0
    turnaround_time = 0

    for p in sorted(processes, key=lambda x: x["arrival"]):
        if time < p["arrival"]:
            time = p["arrival"]
        start = time
        finish = start + p["burst"]
        schedule.append((p["pid"], start, finish))
        waiting_time += start - p["arrival"]
        turnaround_time += finish - p["arrival"]
        time = finish

    n = len(processes)
    return {
        "schedule": schedule,
        "avg_waiting": waiting_time / n,
        "avg_turnaround": turnaround_time / n
    }

print(fcfs(processes))


import matplotlib.pyplot as plt

def draw_gantt(schedule):
    for pid, start, finish in schedule:
        plt.barh(0, finish-start, left=start, edgecolor="black")
        plt.text((start+finish)/2, 0, pid, ha="center", va="center")
    plt.xlabel("Time")
    plt.ylabel("CPU")
    plt.show()

