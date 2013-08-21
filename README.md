## What is it?
This script is pretty much a mix of various snippets from the web. It is meant to be called from your PowerShell ISE $profile and does a couple of things:

1. Lets you specify your preferred encoding. 

PowerShell 2.0 saves as UTF16 by default; PowerShell 3.0 saves as UTF8 by default. If no encoding is specified this script sets the preferred encoding to UTF8.

Why UTF8 as the preferred encoding? Because the script was originally born when I started using Git & Mercurial to manage my code and realized that PowerShell 2.0 saves files as UTF16 and that doesn't play well with these DVCSes. 

Later I decided to tidy it up and make it more generic, the result of which is before you now. I am learning PowerShell and making a big deal of simple stuff like this lets me play around with the language a bit. :)

2. Each time you open a file, if its encoding isn't the preferred one the script *automatically changes the encoding* to what you specify and *saves it*. 

I provide a switch -NoAutoSave in which case the encoding is set to the preferred one but the file isn't automatically saved. This way you can open and close files of a different encoding but they won't be changed. 

3. It creates a Sub menu under Add-ons called "Save & Close as [Encoding]..." within which you have items for each of the encodings supported by ISE. This way you can save a file in a different encoding as a one time thing. 

I decided to close the file after saving - else the script *could* automatically resave it later to the preferred encoding. 

## Help
The script includes a comment based help so `help .\Set-PSISEEncoding.ps1` (with any of the usual `help` switches) is a good idea. 

## Installation
1. Copy the script to some location. 

2. Open your PowerShell ISE `$profile`.
  
  If you don't know how, or are unsure whether you have a `$profile` copy-paste the following in the console pane/ command pane in PowerShell ISE and press enter:
  
  `if(!(Test-Path $profile)) { New-Item -ItemType File -Path $profile -Force }; $psISE.CurrentPowerShellTab.Files.Add($profile)`
  
  This will create the $profile file if it doesn't exist. And then open a new tab with this file loaded. 
  
3. Add a line such as the following to the `$profile` file: `\path\to\files\Set-PSISEEncoding.ps1`.

If you want a different encoding from the default UTF8, modify the line to be like this: `\path\to\files\Set-PSISEEncoding.ps1 -Encoding ASCII`

4. Close and open PowerShell ISE. 