# Project1: File-Processing-System

Student Name: Tahira Malik

CMPSC 472: Operating Systems

Instructor: Janghoon Yang

## Project Overview:

This project is designed to develop a system for efficiently processing large text files and count the frequency of a specific word such as "the" or multiple words, for example most frequent 50 words, across multiple files, using multiprocessing and multithreading. By utilizing these parallel processing techniques, the system can maximize resource usage and reduce processing time. Additionally, the project employs Inter-Process Communication (IPC) mechanisms to pass results between child processes and the parent process. Through this approach, the project demonstrates the performance trade-offs between multiprocessing and multithreading in terms of resource consumption, complexity, and execution time.

## Problem Description:

The primary objective of the system is to count the frequency of a specific word or set of words within a directory of large text files. The system uses separate child processes to handle each file concurrently, created using fork(). Within each child process, multiple threads are spawned using POSIX threads to split and process sections of the file in parallel. This approach enables efficient word counting while reducing the load on system resources.

## Target Files:

The project utilizes the following files from the Calgary Corpus, each representing various categories of text data, from source code to technical paper.
These files are downloaded, extracted, and prepared by excluding unnecessary files before applying the word-count processing.

![image](https://github.com/user-attachments/assets/52c265cf-1cf2-488e-b620-d44c8f4f80a6)

## Technologies Used:

Programming Language: C

Libraries:
![image](https://github.com/user-attachments/assets/b45146e8-9a81-49ff-b796-e97936b96ddc)

Standard C libraries for file handling and memory management.

POSIX threads (pthreads) for multithreading (to be implemented).

System calls for process management and IPC (shared memory).

## Key Features:

### 1. Process Creation
   
Each file is handled in a dedicated process using fork(). This ensures that each file is processed independently, allowing for simultaneous file processing. This process separation enhances fault tolerance and allows for better resource management.

### 2. Multithreading
   
Inside each child process, multithreading is applied to split each file into chunks, which are processed in parallel. This significantly accelerates the word-counting task, as threads work on portions of the file independently. By comparing single-threaded and multi-threaded processing within each process, we can observe the efficiency gains from parallel execution.

### 3. Inter-Process Communication (IPC)

To enable communication between child processes and the parent process, shared memory is used as the IPC mechanism. The child processes store their word-count results in shared memory, allowing the parent process to aggregate the results once all children have completed execution. This shared memory approach minimizes the complexity of message passing while maintaining efficient communication.

### 4. Performance Comparison

The project measures key performance metrics, such as execution time, CPU usage, and memory consumption, to evaluate the effectiveness of multiprocessing and multithreading in this context. These metrics provide insights into the trade-offs between parallelism, memory overhead, and context-switching overhead.

## Implementation:

 Files: Calgary folder is saved in Google Drive, I used python to access it.

![image](https://github.com/user-attachments/assets/740cef80-37e6-4de9-9b8b-7f4fbccef2bb)

### Code Overview
The core functionality is implemented in C, utilizing fork() for process creation, POSIX threads for multithreading within each process, and shared memory for IPC. Below is an outline of the system's major components:

#### 1. File Processing: 

Each child process processes one file, creating multiple threads that count the occurrences of a target word within segments of the file.
A collection of 7 files from the Calgary Corpus was selected for processing. Each file was assigned to a separate process.
![image](https://github.com/user-attachments/assets/3be0251d-5e07-458b-b04b-d1595226f606)
![image](https://github.com/user-attachments/assets/4ff8a355-4140-40ee-9b2e-932a9e2d0199)
Function to count occurrences of a word in a given file, and Buffer to hold each word read
![image](https://github.com/user-attachments/assets/c7fb117d-59d6-4095-898f-d8fb1b822cec)
store and sort unique frequencies
![image](https://github.com/user-attachments/assets/49f7724a-8bb0-4c2c-abc3-828d35263cc1)
![image](https://github.com/user-attachments/assets/9a4694cf-f890-4d9a-9737-29133e9cc79f)

#### 2. Thread Creation:

Each thread processes a section of the file, performing word matching to count occurrences of the target word.
Multithreading
![image](https://github.com/user-attachments/assets/8b55fcb0-2274-4c3a-8927-85a5d8e44318)
![image](https://github.com/user-attachments/assets/8332e5d3-2fdd-4069-b1a0-38e39e6b2548)

#### 3. Shared Memory for IPC: 

After counting, each process writes its result to shared memory, which the parent process aggregates and displays.
#### 4. Multiprocess
![image](https://github.com/user-attachments/assets/76e64622-26cd-4114-af25-839596fc6c7f)
![image](https://github.com/user-attachments/assets/5045aead-546a-4ad7-86b5-22620bc90715)
#### 5. 
Function to measure perfomance of mulyithreading and multiprocessing
![image](https://github.com/user-attachments/assets/d68d5714-6953-4c83-9da2-37686ab1600c)

#### 6. Main function:
![image](https://github.com/user-attachments/assets/5a85c7e6-4d93-4b7b-a44b-7ef66e41b06e)

#### 7. Error Handling: 

The system includes checks for process creation, IPC setup, file access, and thread management errors.
 1. Error Handling in fork() for Process Creation: Error handling for fork() ensures that if the process creation fails, a message is printed, and appropriate action is taken.
![image](https://github.com/user-attachments/assets/7547675d-b6b1-4834-82fb-6d00df6926e5)


2. Error Handling in pthread_create() for Thread Creation
Error handling in pthread_create() verifies that each thread is successfully created, handling errors where thread creation fails:

![image](https://github.com/user-attachments/assets/d7379573-80be-408b-be81-3a47a6d7c61b)


3. Error Handling for File Access
Proper error handling for file access ensures that the file exists and is accessible. If not, the system should provide a helpful error message:
![image](https://github.com/user-attachments/assets/16bf9bb3-067a-42c7-9854-3e61f3138380)


## Performance Evaluation

The system performance is evaluated by measuring:

1. Execution Time: The time required to count words across all files with multiprocessing alone versus with multithreading within each process.
2. CPU Usage: Comparing CPU utilization with and without multithreading.
3. Memory Usage: Memory footprint for multiprocessing versus additional overhead from multiple threads.
#### Results

![image](https://github.com/user-attachments/assets/267cba10-cca3-47ca-82b4-1617d6e28d1e)

![image](https://github.com/user-attachments/assets/055be622-52f3-491a-8647-b8f8b27d637f)

![image](https://github.com/user-attachments/assets/6e0f71d8-2caf-490e-adc2-f94e87369176)

### Analysis

#### 1. Execution Time Analysis
Multiprocessing Only: Completed in 0.008 seconds which indicating high efficiency and fast processing time when only separate processes handle the files.
Multiprocessing and Multithreading: Took 2.929 seconds. This setup adds complexity, as it splits the task into threads within each process, which introduces overhead from managing multiple threads in parallel. For smaller tasks or I/O-bound processes, this overhead may negate the speed gains.

#### 2. CPU Usage Analysis
Multiprocessing Only: Reached 173.36% CPU usage, showing high parallelism and effectively utilizing multiple cores to handle independent processes.
Multiprocessing and Multithreading: Recorded 100.2% CPU usage. This suggests that the threading within each process may not be leveraging CPU resources fully, likely due to thread synchronization overhead or increased contention. This setup could be more advantageous for CPU-bound processes if file sizes were large enough to offset threading overhead.

#### 3. Memory Usage Analysis
Memory Usage for both methods was 127152 KB (about 127 MB). This suggests that while the memory footprint was significant, there was little to no additional memory requirement when using multithreading. In typical cases, multithreading within processes should result in lower memory overhead than multiprocessing alone because threads within a single process share memory space.
The same memory usage for both multiprocessing and multithreading modes could result from several factors, including the way shared memory is allocated and reported by getrusage. Here's a breakdown of key reasons:
Shared Data Structure: In both approaches, the program uses a SharedData structure to hold the word count data. Since the same data structure is accessed either via mmap for multiprocessing or directly in multithreading, the memory usage reflects the space required by this data structure rather than any overhead from additional threads or processes.
Shared Memory Efficiency: In multiprocessing, the mmap system call allocates memory accessible to all child processes. Thus, each child process shares the mapped region rather than duplicating it. Similarly, threads in multithreading inherently share memory within the process. Therefore, both approaches end up using roughly the same memory for shared data
#### 4. Performance Comparison: Advantages and Disadvantages
Multiprocessing Only
Advantages: Fast execution time, higher CPU utilization (parallelism across cores), and efficient handling of independent processes.
Disadvantages: Higher memory usage in scenarios with large numbers of files, as each process is memory-independent.

Multiprocessing and Multithreading
Advantages: Threads within processes share memory, potentially reducing overhead with larger data. This can improve scalability for CPU-bound tasks that need shared memory resources.
Disadvantages: Increased execution time and lower CPU efficiency. Overheads in managing threads, locking mechanisms, and inter-thread communication in I/O-bound processes could lead to inefficiencies.

In this project, Multiprocessing Only proved faster and more CPU-efficient, processing files in parallel with fewer overheads than Multiprocessing + Multithreading. While multithreading can benefit larger, CPU-bound tasks by sharing memory within processes, it added complexity and slowed performance here. Overall, for small to medium I/O-bound tasks, multiprocessing alone is more effective, though larger datasets might benefit from optimized multithreading in the future.

### Diagram :
#### Diagram 1: Process and Thread Creation Structure
This diagram depicts how the main (parent) process forks into multiple child processes, with each child handling a separate file. Within each child process, multiple threads are created to handle different segments of the file for parallel word counting.
Parent Process: Spawns child processes for each file using fork().
Child Processes: Each child process uses pthread_create() to spawn multiple threads.
Threads: Each thread processes a section (or "chunk") of the file to count word occurrences, increasing efficiency by processing segments concurrently.

![image](https://github.com/user-attachments/assets/37c8b3e2-dfb2-4242-a382-9d96281b35e5)

#### Diagram 2: Inter-Process Communication (IPC) via Shared Memory
The following diagram shows how IPC is set up using shared memory. Each child process writes its word count result to shared memory, which the parent process accesses after all child processes complete their execution. This approach provides efficient and synchronized communication of results back to the parent process.
Shared Memory Segment: A memory region accessible by all processes, allowing each child process to store its word count results.
Child Processes: After processing their assigned file segments, each child process writes its word count to shared memory.
Parent Process: Once all children complete execution, the parent process reads from shared memory and aggregates the results for a total word count.
![image](https://github.com/user-attachments/assets/6b3ce263-4877-47ad-82a3-cc3682a3b7dc)

## Conclusion
This project demonstrates the use of multiprocessing and multithreading in processing large files efficiently, highlighting the performance differences between the two approaches. In analyzing word frequency across multiple files, Multiprocessing Only emerged as the more efficient approach due to its faster execution time, higher CPU utilization, and simpler design, leveraging independent processes to maximize CPU resources.

### Key Takeaways
Multiprocessing Only offers fast, parallel execution with each process independently managing a file, which is beneficial for high CPU utilization and is less impacted by context-switching overhead. It resulted in faster processing (0.008 seconds) and higher CPU utilization (173.36%).
Multiprocessing + Multithreading introduces complexity by managing multiple threads within each process, leading to thread synchronization challenges and increased execution time (2.929 seconds). While potentially advantageous for larger, CPU-bound tasks, in this case, it provided no significant memory or CPU usage benefits for smaller, I/O-bound tasks.

### Performance Comparison
The study shows that for smaller-scale text processing tasks, Multiprocessing Only is preferable due to its simplicity, speed, and effective parallelism. Multithreading, while sharing memory within a process, can introduce thread management and synchronization overhead, potentially reducing efficiency in I/O-bound tasks.

### Future Considerations
For future I will consider to add error handling in shared memory usage and setup.
For larger datasets or tasks that are computationally intensive, further exploration of multiprocessing combined with optimized multithreading may yield better results. Additional optimizations, such as load balancing across threads and tuning thread management, could also improve efficiency in multithreading-based approaches.

This project has provided valuable insights into the trade-offs between multiprocessing and multithreading, especially in contexts where both CPU and I/O operations are involved.
