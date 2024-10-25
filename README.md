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

### 1. File Setup:

Calgary folder is saved in Google Drive, I used python to access it.

![image](https://github.com/user-attachments/assets/740cef80-37e6-4de9-9b8b-7f4fbccef2bb)

A collection of 7 files from the Calgary Corpus was selected for processing. Each file was assigned to a separate process.

### Code Overview
The core functionality is implemented in C, utilizing fork() for process creation, POSIX threads for multithreading within each process, and shared memory for IPC. Below is an outline of the system's major components:

#### 1. File Processing: 

Each child process processes one file, creating multiple threads that count the occurrences of a target word within segments of the file.

#### 2. Thread Creation:

Each thread processes a section of the file, performing word matching to count occurrences of the target word.

#### 3. Shared Memory for IPC: 

After counting, each process writes its result to shared memory, which the parent process aggregates and displays.

#### 4. Error Handling: 

The system includes checks for process creation, IPC setup, file access, and thread management errors.

## Performance Evaluation

The system performance is evaluated by measuring:

1. Execution Time: The time required to count words across all files with multiprocessing alone versus with multithreading within each process.
2. CPU Usage: Comparing CPU utilization with and without multithreading.
3. Memory Usage: Memory footprint for multiprocessing versus additional overhead from multiple threads.
#### Results










