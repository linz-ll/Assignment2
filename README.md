# Assignment 2: Readers-Writers Problem

## 1. Design Explanation

This project implements a monitor-style solution to the classic Readers-Writers synchronization problem using Python's `threading` module. The core logic is encapsulated within the `ReadersWritersMonitor` class, which ensures thread safety and coordinates access to a simulated shared resource.

**Key Design Choices:**
* **Condition Variables:** The monitor uses a single `threading.Condition` bound to a `threading.Lock` to protect shared state variables (`active_readers`, `active_writers`, `waiting_writers`).
* **State Tracking:** * `active_readers` ensures multiple readers can access the resource simultaneously when no writer is active.
  * `active_writers` ensures strict mutual exclusion for writers.
* **Fairness / Writer Starvation Prevention:** To prevent writers from starving under a continuous stream of incoming readers, the monitor tracks `waiting_writers`. If a writer is queued (waiting to write), new readers are forced to wait.
* **Re-evaluation (While loops):** All condition waits (`self.condition.wait()`) are wrapped in `while` loops to safeguard against spurious wakeups and state changes that might occur between a thread waking up and re-acquiring the lock.

## 2. How to Run the Program

**Prerequisites:**
* Python 3.x installed on your system.

**Execution:**
1. Open your terminal.
2. Navigate to the directory containing the project files.
3. Run the Python script using the following command:

   python3 readers_writers.py

## 3. Sample Output
* Below is a sample execution trace demonstrating successful concurrent reads and exclusive writes.

Reader 2 wants to read
Reader 2 is waiting to read
Reader 2 starts reading. Active readers = 1
Reader 2 is READING
Reader 3 wants to read
Reader 3 is waiting to read
Reader 3 starts reading. Active readers = 2
Reader 3 is READING
Writer 1 wants to write
Writer 1 is waiting to write
Reader 1 wants to read
Reader 1 is waiting to read
Writer 2 wants to write
Writer 2 is waiting to write
Reader 2 stops reading. Active readers = 1
Reader 2 finished reading
Reader 2 wants to read
Reader 2 is waiting to read
Reader 3 stops reading. Active readers = 0
Reader 3 finished reading
Writer 1 starts writing
Writer 1 is WRITING
Reader 3 wants to read
Reader 3 is waiting to read
Writer 1 stops writing
Writer 1 finished writing
Writer 2 starts writing
Writer 2 is WRITING
Writer 1 wants to write
Writer 1 is waiting to write
Writer 2 stops writing
Writer 2 finished writing
Writer 1 starts writing
Writer 1 is WRITING
Writer 2 wants to write
Writer 2 is waiting to write
Writer 1 stops writing
Writer 1 finished writing
Writer 2 starts writing
Writer 2 is WRITING
Writer 2 stops writing
Writer 2 finished writing
Reader 3 starts reading. Active readers = 1
Reader 3 is READING
Reader 2 starts reading. Active readers = 2
Reader 2 is READING
Reader 1 starts reading. Active readers = 3
Reader 1 is READING
Reader 2 stops reading. Active readers = 2
Reader 2 finished reading
Reader 3 stops reading. Active readers = 1
Reader 3 finished reading
Reader 1 stops reading. Active readers = 0
Reader 1 finished reading
Reader 3 wants to read
Reader 3 is waiting to read
Reader 3 starts reading. Active readers = 1
Reader 3 is READING
Reader 2 wants to read
Reader 2 is waiting to read
Reader 2 starts reading. Active readers = 2
Reader 2 is READING
Reader 1 wants to read
Reader 1 is waiting to read
Reader 1 starts reading. Active readers = 3
Reader 1 is READING
Reader 3 stops reading. Active readers = 2
Reader 3 finished reading
Reader 2 stops reading. Active readers = 1
Reader 2 finished reading
Reader 1 stops reading. Active readers = 0
Reader 1 finished reading
Reader 1 wants to read
Reader 1 is waiting to read
Reader 1 starts reading. Active readers = 1
Reader 1 is READING
Reader 1 stops reading. Active readers = 0
Reader 1 finished reading

 Simulation Complete 
All reader and writers have successfully finished their tasks.