# Process-Hollowing

Process hollowing is commonly performed by creating a process in a suspended state then unmapping/hollowing its memory, which can then be replaced with malicious code.

How it’s done ?

The malicious process starts the target process in a “suspended state” Use -> CreateProcess

Replace or Unmap the victim process’s memory with the malicious executable.ZwUnmapViewOfSection or NtUnmapViewOfSection.

injected malicious code VirtualAllocEx, WriteProcessMemory.

Set the entry point of the main thread in the target process to the starting address of malicious code, then resume the thread. SetThreadContext, ResumeThread.

Demo: 

![image](https://github.com/user-attachments/assets/46e5cc8d-990c-4944-8829-2f2272b592d8)

rcx = 0xC4 → Handle to the target process.

rdx = 0x2A70BAE0000 → Target address in the remote process where shellcode is being written.

r8 = 0x1A084951420 → Pointer to the data being written.

r9 = 0x132 → Number of bytes being written (306 bytes).

![image](https://github.com/user-attachments/assets/c3cbcf34-6fbb-4edc-a377-cb53f0569883)
