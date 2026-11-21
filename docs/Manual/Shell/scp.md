[Parameters]
[1] string path_orig
[2] string path_dest
[3] shell remoteShell
[4] bool is_upload = false

[Description]
Copy a file over the network from one computer to another. The file is downloaded from the current shell to remoteShell or vice versa if is_upload is true. If remoteShell is null, the shell of the computer from which the connection to this shell was made will be used.

Returns true if the copy succeeds. Returns an error string if the operation cannot proceed. If files or folders are omitted, the operation continues with the items that can be copied and returns an error string. Returns null if a shell or computer is unavailable. Items already copied are kept. The return value reflects the initial validation: permissions may change while the transfer is in progress.

[Example] 
hostShell = get_shell
remoteShell = hostShell.connect_service ("120.123.12.12", 22, "username", "mypass")
hostShell.scp("/home/user1/file.txt", "/home/user2/downloads", remoteShell)