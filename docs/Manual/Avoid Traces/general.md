When you access a remote computer without authorization it is very likely that you will attract the attention of the system administrator.

If it finds the machine that started the hacking, it will inform the authorities.
Depending on the type of network you have accessed, administrators can be more or less permissive. 

A good administrator usually finds suspicious activity where others do not see it or simply ignore it.

In any case, it is highly recommended that you delete your tracks once you have finished an intrusion. 

All computers keep a log in /var/system.log. In it, system events are registered, such as incoming or outgoing connections, deletion of files, etc.

## Log File

To open the system.log file you need to use a visual program LogViewer.exe.

To do this from the terminal where you are connected to a remote computer, execute the command LogViewer.exe.
You can open graphic applications from the remote computer.

Next, launch the FileExplorer.exe application. Go to the /var folder and double click on the system.log file.

It is important to keep in mind that the deletion of the records is only useful when a passive trace occurs.

There are two types of traces an administrator can perform: Active trace and Passive trace.

## Active Trace

It occurs only when the administrator of a system is logged into the computer you have accessed. 
The way to stop this tracking if it has already started is to disconnect from the remote machine, at which point the passive trace will begin.

System administrators, like any other worker, have a work schedule.
It is usually advisable to access remote machines at times when the administrator is not working.

To know if an administrator or any other user is present in a system you can use the ps command. If there is a process called dsession it means that the user to whom the process belongs is active on the machine.

Programs like AdminMonitor notify you in an automated way when an administrator is present and the approximate time remaining until an active trace reaches you.

## Passive Trace

It occurs after a failed active trace, or when the administrator goes to work and checks the logs to find suspicious activity. 
The records of the systems by which the intruder has been jumping until arriving at the origin are analyzed.

It is advisable to break the chain of connections at any point so that the administrator can not reach you.
These types of traces are much slower than active traces.

## Bank Trace

It occurs when an NPC detects some unusual activity in their bank account, such as a transaction.

Each time a transaction is made, a log is saved in the bank of both the sender and the receiver of the money, in the path /server/transactions.log and can be opened with the LogViewer.exe program.

After making the transaction, the trace will begin in both accounts, and it is necessary to access the log files in the banks to delete the entries related to the transaction before the trace ends.

Keep in mind that even if you access an NPC's bank account, you need to know which bank registered this account, as that is where the logs are stored. You can see this information after accessing the NPC's bank account, in the upper right corner of the web page.

## How to avoid being caught

It is important that you remove any traces that may incriminate you in an unauthorized connection. In the current version of the game you just have to delete any entry in the file /var/system.log that is either shell obtained or file deleted along with your IP address.

If the AdminMonitor program warns you that a admin has started an active trace against you it is important that you try to delete the indicated entries and disconnect before the end of the countdown. 

Do not delete the entire log, since inevitably when you disconnect from the machine you will create an entry in the log with your disconnection, creating the file if you had deleted it.

If an administrator sees a log file with only a disconnect entry, he will suspect and start the trace against you.

## How to avoid being caught (Advanced)

Keep in mind that if you connect directly to the victim machine, you will not have much reaction time if an administrator starts tracking you. 

It is advisable to use at least one computer to connect to the victim. For example, if you have a rented computer, you can connect to it and from there to the victim machine. In that case you are using a bounce to connect to the remote machine.

You can use as many computers as you want to create these chains of connections (bounces) until you reach the victim.

In this way, the more bounces you use, the administrator who is tracking you more time will spend to reach you.

Then to eliminate your traces you can completely delete the file /var/system.log from any machine you have used as a bounce.

Or alternatively you can also remove from the log of any bounce the entry that indicates a redirection from one ip to the next bounce.