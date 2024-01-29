2014-10-07 Mixmaster 3.0.3a

The batch file, mixm.bat, included with this mixmaster distribution, 
causes mixmaster to use the mix.exe directory as the mix's home directory. 
This keeps all files--binaries, config, stats/keys, mix pool--in a 
single location.

If you run mix.exe directly, without the batch file, mix will use either:

1) The directory specified by MIX3PATH environment variable, if it exists.
2) c:\users\[you]\appdata\roaming\mixmaster.


richard@quicksilvermail.net

