2014-10-07 Mixmaster 3.0.3a

There are a couple things you need to know about Mixmaster.

1) Mix will NOT send your messages. It requires an external SMTP service 
   for that purpose. If you have such a service you can pipe messages from 
   Mix to your SMTP server. The mix.cfg included with this distribution 
   places ready to send files in the mix 'pool' directory where you can 
   access them and send by other means.

2) When Mixmaster runs it looks for its home directory in this order:

   a) first checks it's environment for the variable: 
      MIX3PATH

   b) If that is not present, Mix will check the windows registry for:
      HKEY_CURRENT_USER\Software\Mixmaster\MixDir

   c) If still not present, Mix will create it's own data directory:
      c:\users\<you>\appdata\roaming\mixmaster

It's important to remember that however you choose to specify the Mix home 
dir, you need to put your mix.cfg in that directory.


PORTABLE INSTALLATION

If you'd like to set up Mix for portable use on a USB drive or other portable 
media, you need to use the MIX3PATH environment variable. You can set that in 
a batch file that runs mix.exe. Don't be concerned about changing the 
environment on the host computer. When setting the environment variable from 
the batch file, Mix is given a COPY of the environment and changes only effect 
Mix's copy.

For portable install, you want Mixmsaster to use the directory where it's 
binaries, etc are located--on the USB drive. In some cases you may not know 
the actual path to your drive on that computer. With your Mix files in the 
root directory of your drive, this batch file will do that for you. Create the 
file (mixm.bat), and these 2 lines are what's required:

   set MIX3PATH=.\
   mix.exe

This does run a chance of you forgetting to run mixm.bat and inadvertantly 
running mix.exe instead. Because of this possibility, I recommend you put Mix 
in a directoty of it's own on the USB drive. Maybe you call it the directory 
'mix3'. Leave the batch file in the root directory and use these lines:

   set MIX3PATH=.\mix3
   mix3\mix.exe

A mixm.bat using the first example above is included here. It will keep 
everything together.


IMPORTANT:
This distribution contains a simple mix.cfg file. If you have mixmaster 
installed and a mix.cfg already, don't extract this one.


richard@quicksilvermail.net