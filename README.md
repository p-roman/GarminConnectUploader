GarminConnectUploader
=====================

Uploads .tcx, .fit, and .gpx files (which have already been extracted from your Garmin device) to the Garmin Connect site.

This is a slightly modified version of David Lotton's uploader, which can be found here:
http://sourceforge.net/projects/gcpuploader/

Install
----------------------

Clone repository and optionally add to system path (if you want to run from any location)

Linux: 
Create a symbolic link (assuming you installed under /opt/pygupload/)  
sudo ln -s /opt/pygupload/gupload.py /usr/local/bin/gupload.py

Windows:
Add \<path_to_repository\> to your PATH environment variable.

If you want to run without specifying credentials or garmin file directory everytime, then create a config file, as specified below.


Help
-----------------------

*Usage:*  
`gupload.py [-h] [-a A] [-l L L] [-v {1,2,3,4,5}] filename [filename ...]`

*Positional arguments:*  
    filename Path and name of file(s) to upload.

*Optional arguments:*  
  -h, --help show this help message and exit  
  -a A Sets the activity name for the upload file. This option is ignored if multiple upload files are given.  
  -l L L Garmin Connect login credentials '-l username password'  
  -v {1,2,3,4,5} Verbose - select level of verbosity. 1=DEBUG(most verbose),2=INFO, 3=WARNING, 4=ERROR, 5=CRITICAL(least verbose). [default=3]

*Config file*  
Username and password credentials may be placed in a configuration file located either in the current working directory (directory you are in when you execute gupload.py), or in the user's home directory. In Linux, the home directory is usually something like '/home/\<username\>', while in Windows it is C:\Documents and Settings\\\<username\>\'.WARNING, THIS IS NOT SECURE. USE THIS OPTION AT YOUR OWN RISK. Username and password are stored as clear text in a file format that is consistent with Microsoft (r) INI files.

The configuration file must contain a [Credentials] section containing 'username' and 'password' entries. A [DefaultGarminDataDir] section containing a 'defaultDir' entry is optional.

The name of the config file is '.guploadrc' (gupload.ini for Windows users). 

*Example config file:*  
[Credentials]  
username=\<myusername\>  
password=\<mypassword\>  
[DefaultGarminDataDir]  
defaultDir=\<full_path_to_dir\>\\*

Replace \<myusername\> and \<mypassword\> above with your own login credentials. If you don't want to keep typing in your garmin file directory, add the last 2 OPTIONAL lines to the config file, replacing \<full_path_to_dir\> with the full path to the directory containing the Garmin files you would like to upload.

*Priority of credentials:*  
Command line credentials take priority over config files, current directory config file takes priority over a config file in the user's home directory.


How to Run
-------------------------

*Upload file and set activity name:*  
`gupload.py -l myusername mypassword -a 'Run at park - 12/23' myfile.tcx`

*Upload multiple files:*  
`gupload.py -l myusername mypassword myfile1.tcx myfile2.tcx myfile3.fit`

*Upload all FIT, GPX, or TCX files in a specified directory:*  
`gupload.py <directory_path>/*`

*Upload all FIT, GPX or TCX files in a directory specified in config file:*  
`gupload.py *`

*Upload file using config file for credentials, name file, verbose output:*  
`gupload.py -v 1 -a 'Run at park - 12/23' myfile.tcx`
