---
title: Using PowerShell with FFmpeg
---

## PowerShell and FFmpeg

[FFmpeg](https://ffmpeg.org/) is the natural choice for almost any audio and video processing tasks.
As a cross-platform, open source tool, it can be run almost anywhere: Windows, MacOS, Linux, Kubernetes, Docker containers, cloud platforms, etc.

While FFmpeg is incredibly powerful on its own, the syntax can often be hard to remember.
[PowerShell](https://github.com/PowerShell/PowerShell) provides a more human-friendly interface to run code, thanks to function & parameter naming conventions, parameter types, and can be used to "wrap" FFmpeg commands.

### Concatenate Videos with PowerShell and FFmpeg

I had a specific need to concatenate video files together. I decided to use ffmpeg, naturally, wrapped in a PowerShell function.

```pwsh
function Join-VideoFiles {
  <#
  .SYNOPSIS
  Concatenates audio or video files together, sorted by the input file names.

  .EXAMPLE
  Let's say you have a directory containing a bunch of MKV video files, named YYYY-MM-DD HH-MM-SS.
  The following command would join them all together sequentially.

  Join-VideoFiles -Filter *mkv
  #>
  [CmdletBinding()]
  param (
    [Parameter(Mandatory = $false)]
    [string] $Filter,
    [Parameter(Mandatory = $false)]
    [string] $OutputPath
  )
  $FileList = Get-ChildItem -Path $Filter | Sort-Object -Property Name

  if (!$OutputPath) {
    $OutputPath = '{0}.concat{1}' -f $FileList[0].FullName.Substring(0, $FileList[0].FullName.Length - 1 - $FileList[0].Extension.Length), $FileList[0].Extension
  }

  $TargetFile = '{0}\ffmpeglist.txt' -f $FileList[0].Directory

  Set-Content -Path $TargetFile -Value ''
  foreach ($File in $FileList) {
    Add-Content -Path $TargetFile -Value ('file ''{0}''' -f $File.FullName)
  }

  ffmpeg -f concat -safe 0 -i $TargetFile -c copy $OutputPath
}
```
