- Latency  is the time taken to complete the operation / Request 
- This usually measured in milliseconds (ms)
- Good System Design = Minimizing high-latency operations
- ![[Pasted image 20260407230817.png | 1000]]
## Latency Numbers Range:
### 1. 1ns
- ![[Pasted image 20260407231020.png | 1000]]
- Accessing CPU Registers is very fast 
- but there are only few of them
- CPU Clock cycle is also 1ns
##### CPU Registers:
- This is the tiny, ultra-fast memory units inside the CPU which hold the data that the process is working right now
- Register = CPU's working table
- used for calculations, instructions and temporary data
---
### 2. 1-10ns
- ![[Pasted image 20260407231458.png | 1000]]

##### L1 & L2 Cache:
- These are the small, super-fast memory layers inside/near the CPU that stores the frequently used data to speed things up.
- It is between CPU and RAM and used to avoid slow RAM access
	- **L1**:
		- Fastest
		- Smallest (few KBs)
		- Used for Immediate data
	- **L2:**
		- Slightly slower than L1
		- Bigger (hundreds of KBs to few MBs)
		- Still very fast
		- Stores data not found in L1
	CPU → L1 → L2 → RAM → Disk
---
### 3. 10-100ns
- ![[Pasted image 20260407232134.png | 1000]]

---
### 4. 100-1000ns (1 microsecond)
**System Call:** 
- It is a way for a program (user space) to request service from the operating system (kernel space)
- App can't directly access the hardware, so it asks the OS to do it -> that request = System call
- Making a simple System call in Linux takes hundreds nanoseconds
---
### 5. 1 - 10 Microsecond
**Context Switch:** 
- this is when CPU stops one process / thread and switches to another
- CPU is multitasking --> it keeps switching between tasks very fast
- ![[Pasted image 20260407233125.png | 1000]]
- Context Switching in Linux takes the few microsecond in best case.
- while switching thread if it involves handling data it might take more time

### 6. 10 - 100 microseconds
**Process a HTTP Request**
- It takes few microseconds to process the HTTP Request
- Reading 1 MB data sequentially typically takes about 15 micro seconds
- Reading SSD falls in this range, thinking about 100 microseconds to read an 8k page
- ![[Pasted image 20260407233619.png | 1000]]
---
### 7. 100 - 1000 microsecond (1 ms)
SSD written latency is 10 times slower than SSD read latency
- ![[Pasted image 20260407234016.png | 1000]]
- The typical Memcache/redis get operation takes about 1 ms
- **Intra-zone Networking:** communication within the same availability zone (same data center area in cloud like AWS, Azure)
### 8. 1-10ms
- ![[Pasted image 20260415220526.png | 800]]
### 9. 10-100ms
- l

### 10. 100-1000ms
- It takes 300ms to decrypt the password
- ![[Pasted image 20260415220754.png]]
- ![[Pasted image 20260415220836.png]]
- reading 1 GB from SSD takes 100-1000ms 

### 11. 1s
- ![[Pasted image 20260415221042.png]]

