# Project1: File-Processing-System

Student Name: Tahira Malik

CMPSC 472: Operating Systems

Instructor: Janghoon Yang

## Project Overview:

This project is designed to develop a system for efficiently processing large text files by counting the frequency of a specific word "the" using multiprocessing and multithreading. Each file is processed in a separate child process created using fork(). Inside each process, multiple threads are used to handle different portions of the file, which enables parallel processing of large data. The system also implements an inter-process communication (IPC) mechanism, allowing child processes to send their results to the parent process.

This project allows for comparing the efficiency and resource utilization of multiprocessing versus multithreading in file processing tasks. The results are evaluated based on execution time, CPU usage, and memory consumption, helping to understand the trade-offs between these two approaches.

## Implementation Process
### 1. File Setup:
Calgary folder is saved in Google Drive, I used python to access it.

![image](https://github.com/user-attachments/assets/740cef80-37e6-4de9-9b8b-7f4fbccef2bb)

A collection of 7 files from the Calgary Corpus was selected for processing. Each file was assigned to a separate process.

![image](https://github.com/user-attachments/assets/d5b53dc3-10f6-48fa-83ad-32f8238a1d8d)


### 2. Multiprocessing:

The parent process uses fork() to create a child process for each file which is to perform tasks concurrently
The parent process is the process that initiates and oversees the entire word counting operation.
The parent process itself does not directly count the words. Instead, it delegates this task to its child processes and waits for them by using wait() to finish.
After creating the child processes, the parent waits for all of them to finish using wait(NULL).

Child Processes:

Each child process is a separate process created by the parent to handle one specific task in this case, counting words in a file.
After a successful fork, the child process performs the word counting in the assigned file by calling count_word_in_file(&file_wc[i]).
After completing the word count task, the child process terminates itself by calling exit(0).
Example:
I have 7 files and the program is using multiprocessing, the parent process will create 7 child processes. Each child process will be responsible for reading one file and counting the occurrences of the specified word in that file.

In the code:




### 3. Multithreading:

Thread Function Definition:

void *thread_count_word(void *arg): This function is called for each thread created. It takes a pointer to a WordCount struct as an argument, which contains the filename and word to count.

count_word_in_file((WordCount *)arg): This line calls the count_word_in_file function, passing the argument which is cast to the correct type. This function counts the occurrences of the specified word in the corresponding file.

Creating Threads:

pthread_t threads[NUM_FILES]: This declares an array of thread identifiers to keep track of the threads created.
pthread_create(&threads[i], NULL, thread_count_word, &wc[i]): This line creates a new thread for each file. It passes the address of the thread identifier, specifies default thread attributes (NULL), points to the thread function (thread_count_word), and passes the corresponding WordCount struct (&wc[i]) as an argument.

Waiting for Threads to Complete:

pthread_join(threads[i], NULL): This line ensures that the main thread waits for each created thread to finish execution before continuing. This is important for proper synchronization and to ensure all word counts are completed before the program ends.
In this code, the parent or main thread creates multiple threads instead of child processes. It creates multiple threads using pthread_create(), each responsible for processing one file. Each thread invokes count_word_in_file, which handles the counting of the specified word in its assigned file.



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
