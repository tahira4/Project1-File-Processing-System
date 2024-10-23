# Project1: File-Processing-System

Student Name: Tahira Malik

CMPSC 472: Operating Systems

Instructor: Janghoon Yang

## Project Overview:

This project is designed to develop a system for efficiently processing large text files by counting the frequency of a specific word (or set of words) using multiprocessing and multithreading. Each file is processed in a separate child process created using fork(). Inside each process, multiple threads are used to handle different portions of the file, which enables parallel processing of large data. The system also implements an inter-process communication (IPC) mechanism, allowing child processes to send their results to the parent process.

This project allows for comparing the efficiency and resource utilization of multiprocessing versus multithreading in file processing tasks. The results are evaluated based on execution time, CPU usage, and memory consumption, helping to understand the trade-offs between these two approaches.

## Implementation Process
### 1. File Setup:

A collection of 9 files from the Calgary Corpus was selected for processing. Each file was assigned to a separate process.

### 2. Multiprocessing:

The parent process uses fork() to create a child process for each file.
Each child process is responsible for handling one file.

### 3. Multithreading:

Inside each child process, the file is divided into chunks, and multiple threads (using POSIX threads) are created to handle word counting on these chunks in parallel.

### 4. Inter-Process Communication (IPC):

Child processes use pipes to send the word count results back to the parent process, which aggregates the results.
### 5. Evaluation:

Both approaches were compared by measuring the time taken for word counting, as well as the CPU and memory usage for each approach.

## Implemented Features
### 1. Process Creation:

The system uses fork() to create separate child processes, with each process handling a single file from the Calgary Corpus.
### 2. Multithreading:

Each file is split into chunks and assigned to multiple threads within a process, allowing for parallel word counting within a file.
### 3. Inter-Process Communication (IPC):

The system implements an IPC mechanism using pipes to pass word count results from child processes to the parent process.
### 4. Error Handling:

The system includes error handling for process creation (fork()), thread creation, and IPC setup.
### 5. Performance Metrics:

Execution time, CPU usage, and memory consumption were recorded and compared for both multiprocessing and multithreading approaches.
### 6. Word Frequency Counting:

The system correctly counts the frequency of a specified word or set of words in each file.
![image](https://github.com/user-attachments/assets/63ec8bae-20de-431c-8f56-2b5ee3bb98de)
