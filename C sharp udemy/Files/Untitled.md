## Technical Insights Gained

### Task 1 - File Data Processor

- Created a large file of size 1GB Approx using StreamWriter.
- SubTask 1, Read from the file using FileStream alone with BufferSize.
- In SubTask2, When Used Buffered stream along with FileStream able to see positive performance impact.
- Such as Less Time taken to read and process the data with help of buffered chunks.
- Able to See Mb/s speed difference in below images!

- Also when Manipulating Buffer Size of FileStream and buffered stream, got to know:

![File Stream High Buffer Than Buffered Stream](images/Task1-2_FileStreamHighBufferThanBufferedStream.png)
- Above image indicates when File Stream Buffer size is greater than buffered stream the speed of data read is 2582.06 mb/s.

![File Stream Buffer Equal BufferedStream](images/Task1-2_FileStreamEqualBufferOfBufferedStream.png)
- Above image indicates when File Stream Buffer size is Equal to buffered stream the speed of data read is 4217.13 mb/s.

![File Stream Low Buffer Than Buffered Stream](images/Task1-2_FileStreamLowBufferThanBufferedStream.png)
- Above image indicates when File Stream Buffer size is Lesser than buffered stream the speed of data read is 4048.59 mb/s.

- Shows, when buffer size of FileStream is equal or less, it has good performance than greater.
  - This is because the reading works like Disk -> OS cache -> FileStream internal buffer -> BufferedStream buffer -> local buffer.
  - When FileStream buffer is greater or equal, .NET optimize it by direct read by BufferStream  - Avoiding Double copy.
	
Note : Even used FileStream for text file handling as per requirement, its better to use StreamWriter Reader. One reason can be streamReader use automatic encoding and direct reading text, in filestream want to manually encode it as used in the code.

### Task 2 - File Data Processor with Asynchronous Methods

- Implemented the Task1 File Data Processor in Asynchronous way, such that multiple task can utilize the method parallel.

 ![Asynchronous File Handling](images/Task2_AsynchronousFileHandling.png)
- In Above Image, Reading and Process 3 Files, where each file take 5.19s, 5.89s & 7.20s
  - It Should have taken 18.28s to run all 3 files in synchronous one-by-one way.
  - But It took only 7.2 Seconds to Run Entire 3 File reading process when executed parallel with async await.
- Same happens for File Read -> Process -> Write.

### Task 3 - Investigate Issues in Basic File usage.

- The Issue Identified are commented as Insight's in below Image.

![Insights On File Handling Code Issue](images/Task3_InsightsOnFileHandlingCodeIssue.png)
- It can be fixed, by simply using StreamWriter and StreamReader which is specially used for Text based file handling.
- BinaryReader Writer for Binary is used. Internal Buffer in these are efficient for common case.

- Time Take by code with issue - using Memory Stream and File Stream - Refer Below Image

![Time Taken CodeWithIssue](images/Task3_TimeTakenCodeWithIssue.png)

- Time Take by code when issue fixed - using StreamWriter Reader - Refer Below Image

![Time Taken IssueFixedCode](images/Task3_TimeTakenIssueFixedCode.png)

- We could see the positive performance impact after using StreamWriter Reader. Though it may seem very less - for large file it would have huge impact.

### Task 4 - Logging System for Multiple Users. 

- Identified the issue in SubTask1 and commented along the code.
- Got to know about locking mechanism for accessing same file parallel by multiple threads.
- The performance difference is visible through time taken by code with issue and fixed.
- Below is the output of modified code.

![Thread Safe Logging](images/Task4-3_ThreadSafeLogging.png)

- When tried to run parallel processing for Given starter code or even updated synchronous code, We get exceptions.

![Thread UnSafe Logging with Old Code](images/Task4-3_ThreadSafeLogging_OldCode.png)

These are the Insights gained through these assignment, apart learned about buffers, stream, and Task Thread.