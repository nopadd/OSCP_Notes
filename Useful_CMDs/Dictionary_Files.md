# Background (Vulnhub:Mr.Robot)
- Sometimes you encounter files with .dic at the end of them.  This means they are HUGE dictionary files.
- There's likely valuable content in these files as they are not that common on normal boxes but identifying what is valuable in all the data is an effort.
- You can quickly reduce the noise in these files through the following:
```
cat [original file] | sort | unique [output file name]
```
- You can then inspect this information.  It is likely this information will be used in a brute-force attack as the username or password would be hidden in the file text.
