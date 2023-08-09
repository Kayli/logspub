# random notes on powershell scripting

## basics

- show environment variable value
  > echo $env:path

- show groups that current user is member of
  > whoami /groups

- compress files in a folder (omg! can't handle files larger than 2GB)
  > Compress-Archive -Path C:\OtherStuff\*.txt -Update -DestinationPath archive.zip

- check for open ports
  > tnc <host> -Port <port>