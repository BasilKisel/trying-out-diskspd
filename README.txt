I use Microsoft's DISKSPD utility to test my computers.
There is useful links:
 * Main page: https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223
 * Good introduction guide: https://blogs.technet.microsoft.com/josebda/2014/10/13/diskspd-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares/

I've decided to make stress test choosing abundant random access like some sort of DDoS on hard drive. I think, it can reproduce active SWAP using when many apps try work simultaneously.

PS or CMD :> diskspd -w50 -W5 -b4K -c8G -F2 -o32 -Sh -L -r -d600 C:\testfile.foo
Where
 * “-w50” is 50% of write and 50% of read operations;
 * “-W5” is stands for “Wake Up in 5 seconds”;
 * “-b4K” means use 4K blocks;
 * “-c8G” tells to create each file in size of 8 gigabytes;
 * “-F2” tells to use exactly 2 threads;
 * “-o32” is 32 outstanding IO requests per file per thread;
 * “-Sh” tells no use of any caching ether hard or software;
 * “-L” tells to measure latency;
 * “-r” stands for “random” means use random access to file;
 * “-d600” stands for “duration is 10 minutes”.

PS or CMD :> del C:\testfile.foo
rem: Because Diskspd utility doesn’t remove file after work.
