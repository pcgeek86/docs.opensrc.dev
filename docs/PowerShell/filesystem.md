---
sidebar_position: 2
title: Manage Local Filesystems with PowerShell
---

PowerShell is an excellent language to automate file system operations.
Because the language is verbose, it is easy for engineers to read other people's code and understand what it's doing.
Since PowerShell is built on .NET Core, it's easy to automate filesystems on major operating systems, including Windows, MacOS, and various Linux distributions.

## List Files & Directories

One of the most simple file system operations is to list files and directories, underneath a given directory path.
PowerShell also provides a `$HOME` variable that consistently points to a user's home directory, across different platforms.

```pwsh
Get-ChildItem -Path $HOME
```

You can also use this command to limit results to *just* directories or *just* files.

```pwsh
# List directories only
Get-ChildItem -Path $HOME -Directory

# List files only
Get-ChildItem -Path $HOME -File
```

## Delete File

One of the built-in PowerShell commands allows you to delete files from the local file system.
This command is called `Remove-Item`.
You can specify one or more file paths that you want to delete.
Use commas to delimit multiple file paths that you want to delete.

```pwsh
Remove-Item -Path file01.txt
Remove-Item -Path $HOME/file02.txt, /file03.txt
```

## Delete Directory

The same command that's used to delete files can also delete directories, along with all of their contents.
However, because directories can contain multiple items, you must affirmatively tell PowerShell to delete all recursive items.
The `-Recurse` parameter indicates to PowerShell that you want to delete everything *inside* the directory, along with the directory itself.
Using the `-Force` parameter prevents any interactive confirmation prompt from showing up.

```pwsh
Remove-Item -Path $HOME/testdir -Recurse -Force
```

## Create Text or Binary File

You can create a new text file with a single PowerShell command, while setting the contents of the file simultaneously.
The `Set-Content` command allows you to write data into a file.

```pwsh
Set-Content -Path $HOME/file01.txt -Value 'Trevor Sullivan'
```

If you want to write raw bytes into a file, you can use the `-AsByteStream` paramter for `Set-Content`.
The command below creates an array of individual byte values, and pipes it into the `-Value` parameter of the `Set-Content` command.

```pwsh
[Byte[]]@(50, 100, 150, 120, 125, 153) | Set-Content -Path $HOME/file01.bin -AsByteStream
```

