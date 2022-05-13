# strace parser

`strace -a1 -s0 -f -C -tt -e trace=read,write,pread64,pwrite64,lseek,mmap,munmap,mremap,creat,open,openat,close,stat,fstat,lstat,fork,clone -o input.txt [program]`

**time** | **pid** | **op** | **cpid** | **fd** | **offset** | **length** | **mem\_addr** | **filename** | **inode**
---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ----
time | pid | **read** | | fd | | count | | | |
time | pid | **write** | | fd | | count | | | |
time | pid | **pread64** | | fd | offset | count | | | |
time | pid | **pwrite64** | | fd | offset | count | | | |
time | pid | **lseek** | | fd | offset | | | |
time | pid | **mmap** | | fd | offset | length | addr | |
time | pid | **munmap** | | | | length | addr | |
time | pid | **mremap** | | old\_addr | | new\_len | new\_addr | |
time | pid | **creat** | | fd | | | | \*pathname |
time | pid | **open** | | fd | | | | filename |
time | pid | **openat** | | fd | | | | \*pathname |
time | pid | **close** | | fd | | | | | |
time | pid | **stat** | | | | | | \*path | st\_ino |
time | pid | **fstat** | | fd | | | | | st\_ino |
time | pid | **lstat** | | | | | | \*path | st\_ino |
time | pid | **fork** | c\_pid | | | | | | |
time | pid | **clone** | c\_pid | | | | | | |


* sys\_read : read bytes for open file<br>
  `[time, pid, read, , fd, , (return)count]`
* sys\_write : write bytes for open file<br>
  `[time, pid, write, , fd, , (return)count]`
* sys\_pread64 : read from a file descriptor at a given offset<br>
  `[time, pid, pread64, , fd, offset(position), (return)count]`
* sys\_pwrite64 : write to a file descriptor at a given offset<br>
  `[time, pid, pwrite64, , fd, offset(position), (return)count]`
* sys\_lseek : move position of next read or write<br>
  `[time, pid, lseek, , fd, (return)offset]`
* sys\_mmap : map files or devices into memory<br>
  `[time, pid, mmap, , fd, offset, length, (return)addr]`
* sys\_munmap : unmap files or devices into memory<br>
  `[time, pid, munmap, , , , length, addr]`
* sys\_mremap : remap a virtual memory address<br>
  `[time, pid, mremap, , old_addr, , new_len, (return)addr]`
* sys\_creat : creates file and connect to open file (-1 on error)<br>
  `[time, pid, creat, , (return)fd, , , , *pathname]`
* sys\_open : connect to open file (-1 on error)<br>
  `[time, pid, open, , (return)fd, , , , *filename]`
* sys\_openat : open a file relative to a directory file descriptor (-1 on error)<br>
  `[time, pid, openat, , (return)fd, , , , *pathname]`
* sys\_close : disconnect open file (zero on success, -1 on error)<br>
  `[time, pid, close, , fd]`
* sys\_stat : get file status (zero on success, -1 on error)<br>
  `[time, pid, stat, , , , , , *path, st_ino]`
* sys\_fstat : get file status (zero on success, -1 on error)<br>
  `[time, pid, fstat, , fd, , , , , st_ino]`
* sys\_lstat : get file status(if path is a symbolic link, then the link itself is stat-ed, not the file that it refers to) (zero on success, -1 on error)<br>
  `[time, pid, lstat, , , , , , *path, st_ino]`
* sys\_fork : creat a child process<br>
  `[time, pid, fork, (return)c_pid]`
* sys\_clone : creat a child process<br>
  `[time, pid, clone, (return)c_pid]`

## execute code with 'run.sh'
`./run.sh [log_file] [output_directory]`
