# ntfsreader-powershell
Powershell script using the ntfsreader library (embedded into script).

Original ntfsreader source found here: https://sourceforge.net/projects/ntfsreader/

Updated source attached to this repo.


Example usage:

```
$Drives = "C:\","D:\"

$Results = $Null
ForEach ($Drive in $Drives) {
  $Results += NTFSReader -Drive $Drive
}

Write-Output "Top 10 Folders by sub file count:"
$Results | Where-Object {$_.Directory -eq $True} | Sort-Object SubFileCount -Descending | Select-Object FullName,SubFileCount -First 10 | FT

Write-Output "Top 10 Folders by total sub file size:"
$Results | Where-Object {$_.Directory -eq $True} | Sort-Object SubFileTotalSize -Descending | Select-Object FullName,SubFileTotalSize -First 10 | FT

Write-Output "Top 10 largest files:"
$Results | Where-Object {$_.Directory -eq $False} | Sort-Object Size -Descending | Select-Object FullName,Size -First 10 | FT
```
